---
layout: post
title: Create a custom webmap with custom raster overlay from multiples PNGs
comments: true
created: 1481890103
excerpt_separator: <!--more-->
---

This post will show how to built a custom webmaps from a massive amount of PNGs.

From this: 

![List of pngs](/public/images/webmap1/png-radio.png)

To this:

![List of pngs](/public/images/webmap1/lightmap-world.png)

To do that we will use __only free softwares__:

* [GDAL](http://www.gdal.org)
* [geoserver](http://geoserver.org)
* [mapproxy](https://mapproxy.org)
* [convert](https://www.imagemagick.org/script/convert.php)
* [composite](https://www.imagemagick.org/script/composite.php)
* [leaflet](http://leafletjs.com)

<!--more-->

<style  type="text/css">
.thumbnail {
  float:left;
  padding-right: 0.5em;
}
.screenshot, .thumbnail {
  text-align:center;
}
.thumbnail img, .screenshot img {
    width:210px;
    margin-bottom:0;
}
.screenshot img {
    margin-left: auto;
    margin-right: auto
}
.thumbnail .click, .screenshot .click {
    color:#000 !important;
    text-decoration:italic;
}
.thumbnail .title, .screenshot .click {
    font-weight:bold;
}
.clearfix:after {
  content:'';
  display:block;
  clear:both;
  padding-bottom:1em;
}
</style>

# Problem to solve

Basically, we have a lot of PNG files containing data in a one degree by one degree size.

Each PNG represent Sigfox radio coverage on a area of 1degree by one degree in GPS coordinate system.

Consequently, images does not have the same size :

<div class="clearfix">
<div class="thumbnail">
<a href="/public/images/webmap1/toulouse.png"><img src="/public/images/webmap1/toulouse.png"></a>
<span class="title">Toulouse coverage</span><br>
<a href="/public/images/webmap1/toulouse.png" class="click">(Clic to enlarge)</a>
</div>
<div class="thumbnail">
<a href="/public/images/webmap1/finland.png"><img src="/public/images/webmap1/finland.png"></a>
<span class="title">Finland coverage</span><br>
<a href="/public/images/webmap1/finland.png" class="click">(Clic to enlarge)</a>
</div>
<div class="thumbnail">
<a href="/public/images/webmap1/guyana.png"><img src="/public/images/webmap1/guyana.png"></a>
<span class="title">French Guyana coverage</span><br>
<a href="/public/images/webmap1/guyana.png" class="click">(Clic to enlarge)</a>
</div>
</div>

All these images are named with lat long corner information and spread accross several directories.

An additionnal difficulties is that coverage are stored by country and there is overlaping images on borders.
We will need to merge images near borders.

Colors are pure Red Green Blue representing several level of coverage which is not the subject here.

But as we want to build a simple public map, we will hide this complexity and change all color into a single "shinny" one.

## Goal to reach

We will create a webmap with outstanding performances:

__A fully cached web maps tiled and served within TMS urls.__

Url like this

```
http://.../Z/Y/X.png
```

Will return 256px x 256px PNG tile with alpha like this:

![256x256 tile](/public/images/webmap1/tile.png)

Finally we will put in on a webmap using leaflet and with a nice background:

![worl map on satellite background](/public/images/webmap1/satellite-map.png)

# Principle

The general principle follow several steps:

1. Change color bands to merge Red Green Blue into one band
2. Merge overlaping images
3. Change images into gray images with alpha
4. Add geographical data into images transforming PNGs into Geotiff
5. Change geotiff from RGB to RGBA
6. Build an _Image pyramid_ from Geotiff images
7. Loading images into Geoserver
8. Finalyse layer style: apply final color, merge with other layers
9. Build TMS directory tree with Mapproxy
10. Serve tile from this directory with NGINX
11. Built a leaflet map displaying the map in a webpage

_Note: Maybe it is possible to skip one step (especialy color manipulation) but the try I made all failed_

I won't present the python & bash script glue but only important commands and tools.
Some steps suppose that you'll save and sort temporary images with caution.

## Change color bands

This is a mandatory step because Geoserver is not able to style raster with data in several "band" (See Geoserver section further).

First change blue and red into green (to have a single color) with convert command:

```
convert input.png -fill "#00FF00" -opaque blue tmp.png
convert tmp.png -fill "#00FF00" -opaque red output.png
```

## Merge overlaping images

If two (or more images) overlap then we need to add coverages, which means to merge "green" areas:

```
convert -composite image1.png image2.png result.png
```

__When all merge are done, you need to

## Change image into gray with alpha

This is again a geoserver requirement.
Geoserver can style only images with one channel of data.

First step put all color to Green but Red and Blue Channel exist and need to be removed.

```
convert green.png -separate output%d.png
rm output0.png output2.png
```

As _composite_ command separate channeld Red/Green/Blue in three files and as image is full green we can remove black images for red and blue channels.

## Add Geographical data to image

This can be done with a single command as soon as you know the corners coordinates (here in WGS 84)

```
gdal_translate -of GTiff -a_ullr 1 47 2 46 -a_srs EPSG:4326  input.png output.tif
```

_If you want to be sure that image is correctly positionned use QGIS, add a raster layer and select output.gif._

## Change geotiff from RGB to RGBA

After all this operations you will have a RGB tiff (with black and white content) and we need to add the alpha channel.
Otherwise you can't build image pyramid (following section commands will fail with errors).

```
gdal_translate -expand rgb input.tif output.tif
```

## Build an _Image pyramid_ from Geotiff images

Geoserver raster input is quite basic: it can load a single geotiff in a data store.

I have hundreds of geotiff. I could merge them into a giant single one but loading it will eat a loooot of RAM and is not elegant or even practicable.

The way I load it into geoserver is using an "Image pyramid".
This require a geoserver plugin but this gives good results.

_If you know better methods please put it in the comment :-)_

The command for building a pyramid is _"gdal_retile"_, but there is some deformation if you use it directly if youre images are not contiguous.

To avoid deformation you'll need to prepare a clean GDAL referential (a VRT file):

_You can select tif files one by one or with *.tif but for a great number of image shell buffer will be overflowed_

```
gdalbuildvrt -input_file_list tilelist.txt world.vrt
```

Then you can build the pyramid from your the VRT.

```
gdal_retile.py -v -r bilinear -levels 1 -ps 2048 2048 -co "TILED=YES" -co "COMPRESS=JPEG" -targetDir ./coverage_tiles world.vrt
```

When done you have an image pyramid in the directory _"coverage_tiles"_.

## Loading images into Geoserver

## Finalyse layer style: apply final color, merge with other layers

## Build TMS directory tree with Mapproxy

## Serve tile from this directory with NGINX

## Built a leaflet map displaying the map in a webpage



