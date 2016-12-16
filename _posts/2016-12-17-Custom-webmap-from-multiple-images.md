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

1. Add geographical data into images transforming PNGs into Geotiff
2. Change color bands to merge Red Green Blue into one band
3. Build an _Image pyramid_ from Geotiff images
4. Loading images into Geoserver
5. Finalyse layer style: apply final color, merge with other layers
6. Build TMS directory tree with Mapproxy
7. Serve tile from this directory with NGINX
8. Built a leaflet map displaying the map in a webpage

## Add Geographical data to PNG

This can be done with a simple command as soon as you know the corners coordinates (here in WGS 84)

```
gdal_translate -of GTiff -a_ullr 1 47 2 46 -a_srs EPSG:4326  input.png output.tif
```

_If you want to be sure that image is correctly positionned use QGIS, add a raster layer and select output.gif._









