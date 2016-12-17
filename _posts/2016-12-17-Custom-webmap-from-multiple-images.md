layout: post
title: Create a custom webmap with custom raster overlay from multiples PNGs
comments: true
created: 1481890103
excerpt_separator: <!--more-->
---

<style  type="text/css">
.thumbnail, .thumbnail-med{
  float:left;
  padding-right: 0.5em;
}
.screenshot, .thumbnail {
  text-align:center;
}
.thumbnail-big img, .screenshot-big img {
    width:600px;
    margin-bottom:0;
}
.thumbnail-med img, .screenshot-med img {
    width:350px;
    margin-bottom:0;
}
.thumbnail img, .screenshot img {
    width:210px;
    margin-bottom:0;
}
.screenshot img {
    margin-left: auto;
    margin-right: auto
}
.thumbnail .click, .thumbnail-med .click, .screenshot .click {
    color:#000 !important;
    text-decoration:italic;
}
.thumbnail .title, .thumbnail-med .click,.screenshot .click {
    font-weight:bold;
}
.clearfix:after {
  content:'';
  display:block;
  clear:both;
  padding-bottom:1em;
}
</style>

This post will show how to built a custom webmaps from a massive amount of PNGs.

<div class="clearfix">
<div class="thumbnail-med">
<a href="/public/images/webmap1/png-radio.png"><img src="/public/images/webmap1/png-radio.png"></a>
<span class="title">from this</span><br>
<a href="/public/images/webmap1/png-radio.png" class="click">(Clic to enlarge)</a>
</div>
<div class="thumbnail-med">
<a href="/public/images/webmap1/lightmap-world.png"><img src="/public/images/webmap1/lightmap-world.png"></a>
<span class="title">to this</span><br>
<a href="/public/images/webmap1/lightmap-world.png" class="click">(Clic to enlarge)</a>
</div>
</div>

To do that we will use __only free softwares__:

* [GDAL](http://www.gdal.org)
* [geoserver](http://geoserver.org)
* [mapproxy](https://mapproxy.org)
* [convert](https://www.imagemagick.org/script/convert.php)
* [composite](https://www.imagemagick.org/script/composite.php)
* [leaflet](http://leafletjs.com)

<!--more-->

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

One more difficulty is that coverage are stored by country and there is overlaping images on borders.
We will need to merge images near borders.

Colors are pure Red Green Blue representing several levels of radio coverage.
We will change all colors into a single one for a less complex and more aesthetic map.

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

1. Change color channels to merge Red Green Blue into one channels
2. Merge overlapping images
3. Add geographical data into images transforming PNGs into geotiff
4. Change geotiff from RGB to RGBA
5. Build an _Image pyramid_ from Geotiff images
6. Loading images into Geoserver
7. Finalize layer style: apply final color, merge with other layers
8. Build TMS directory tree with Mapproxy
9. Serve tile from this directory with NGINX
10. Built a leaflet map on a webpage

_Note: Maybe it is possible to skip one step (especialy color manipulation) but all attempts I made failed_

I won't present the python & bash script glue but only important commands and tools.

## Change color channels

This is a mandatory step because Geoserver is not able to style raster with data in several "band" (See Geoserver section further).

First change blue and red into green (to have a single color) with convert command:

```
convert input.png -fill "#00FF00" -opaque blue tmp.png
convert tmp.png -fill "#00FF00" -opaque red output.png
```

<div class="clearfix">
<div class="thumbnail">
<a href="/public/images/webmap1/source2.png"><img src="/public/images/webmap1/source2.png"></a>
<span class="title">Original image</span><br>
<a href="/public/images/webmap1/source2.png" class="click">(Clic to enlarge)</a>
</div>
<div class="thumbnail">
<a href="/public/images/webmap1/green2.png"><img src="/public/images/webmap1/green2.png"></a>
<span class="title">All green image</span><br>
<a href="/public/images/webmap1/green2.png" class="click">(Clic to enlarge)</a>
</div>
</div>

## Merge overlapping images

If two (or more images) overlap then we need to add coverages, which means to merge "green" areas:

```
convert -composite image1.png image2.png result.png
```

<div class="clearfix">
<div class="thumbnail">
<a href="/public/images/webmap1/green1.png"><img src="/public/images/webmap1/green1.png"></a>
<span class="title">Image 1</span><br>
<a href="/public/images/webmap1/green1.png" class="click">(Clic to enlarge)</a>
</div>
<div class="thumbnail">
<a href="/public/images/webmap1/green2.png"><img src="/public/images/webmap1/green2.png"></a>
<span class="title">Image 2</span><br>
<a href="/public/images/webmap1/green2.png" class="click">(Clic to enlarge)</a>
</div>
<div class="thumbnail">
<a href="/public/images/webmap1/cumul.png"><img src="/public/images/webmap1/cumul.png"></a>
<span class="title">Cumulated image</span><br>
<a href="/public/images/webmap1/cumul.png" class="click">(Clic to enlarge)</a>
</div>
</div>


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

I won't detail here how to do this but basically:
1. Load pyramid into a store (you need the image pyramid plugin)
2. Create a layer from that store
3. Create a style for that layer
4. Merge the layer with other one in a layer group (if you need it)
5. Youre WMS service is ready

Here it is the SLD style I use:

```
<?xml version="1.0" encoding="UTF-8"?>
<StyledLayerDescriptor version="1.0.0" 
 xsi:schemaLocation="http://www.opengis.net/sld StyledLayerDescriptor.xsd" 
 xmlns="http://www.opengis.net/sld" 
 xmlns:ogc="http://www.opengis.net/ogc" 
 xmlns:xlink="http://www.w3.org/1999/xlink" 
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <NamedLayer>
    <Name>Sigfox coverage</Name>
    <UserStyle>
      <Title>Fantastic Raster</Title>
      <Abstract>A kickass style</Abstract>
      <FeatureTypeStyle>
        <Rule>
          <Name>Coverage colorisation</Name>
          <Title>Opaque Raster</Title>
          <RasterSymbolizer>
            <ChannelSelection>
              <GreenChannel>
                 <SourceChannelName>1</SourceChannelName>
              </GreenChannel>
            </ChannelSelection>
            <ColorMap>
              <ColorMapEntry color="#000000" quantity="0" opacity="0"/>
              <ColorMapEntry color="#00DFFF" quantity="250" opacity="1"/> <!-- there is some noise in images and I need to display only plain color areas -->
              <ColorMapEntry color="#00DFFF" quantity="256" opacity="1"/>
            </ColorMap>
            <Opacity>0.7</Opacity> <!-- you can tune transparency here -->
          </RasterSymbolizer>
        </Rule>
      </FeatureTypeStyle>
    </UserStyle>
  </NamedLayer>
</StyledLayerDescriptor>
```

Before merging, the is the OpenLayer preview:

<div class="clearfix">
<div class="thumbnail-big">
<a href="/public/images/webmap1/coverage-layer-preview.png"><img src="/public/images/webmap1/coverage-layer-preview.png"></a>
<span class="title">Coverage layer preview in geoserver with Openlayers</span><br>
<a href="/public/images/webmap1/coverage-layer-preview.png" class="click">(Clic to enlarge)</a>
</div>
</div>


## Finalize layer style: apply final color, merge with other layers

After merging with a country layer, this is the preview in OpenLayers :

<div class="clearfix">
<div class="thumbnail-big">
<a href="/public/images/webmap1/coverage-group-layer-preview.png"><img src="/public/images/webmap1/coverage-group-layer-preview.png"></a>
<span class="title">Final aggregated layer preview in geoserver with Openlayers</span><br>
<a href="/public/images/webmap1/coverage-group-layer-preview.png" class="click">(Clic to enlarge)</a>
</div>
</div>


## Build TMS directory tree with Mapproxy

Now my favorite part (I am a mapproxy fan!), create TMS directory with mapproxy.

You need to define WMS source from geoserver previous URL and define a cache.

This is my config file :

```
services:
  demo:
  tms:
    use_grid_names: true
    # origin for /tiles service
    origin: 'sw'
  wmts:
    kvp: false
    restful: true

layers:
  - name: sigfox_cached
    title: Layer of coverage map www.sigfox.com
    sources: [sigfox_cache]

caches:
  sigfox_cache:
    grids: [g]
    sources: [geoserver]
    meta_size: [2, 2]
    meta_buffer: 1
    image:
      resampling_method: bilinear
      encoding_options:
        quantizer: mediancut
    cache:
      type: file
      directory_layout: tms

sources:
  geoserver:
    type: wms
    supported_srs: ['EPSG:4326']
    coverage:
      bbox: [-180,-90, 180,90]
      srs: 'EPSG:4326'
    req:
      url: http://127.0.0.1:8080/geoserver/sigfox-www/wms?
      layers: www.sigfox.com
      transparent: true
      format: image/png

grids:
    webmercator:
        base: GLOBAL_WEBMERCATOR
    g:
        base: GLOBAL_WEBMERCATOR
        srs: 'EPSG:900913'
        origin: 'nw'
globals:
  cache:
    # where to store the cached images
    base_dir: '/home/mapproxy/data'
  image:
    # without this mapproxy will simplify colors
    paletted: false

```

You can try your configuration launching mapproxy with integrated demo:

```
mapproxy-util serve-develop -b 127.0.0.1:7070 mapproxy.yaml
```

If OK, you need to use seeding to fill your data directory.

My seed file

```
seeds:
  sigfox.com:
    caches: [sigfox_cachei_light]
    levels:
      to: 8
```

Launch seeding (this could be very long).

```
mapproxy-seed -f mapproxy.yaml -c 1 sigfox-seed.yml
```

_I restrict mapproxy to one core only because I need to code during this time and I won't freeze my laptop_

## Serve tile from this directory with NGINX

Copy your TMS directory into your NGINX server.

_Self evident step : no need for comment_

## Built a leaflet map displaying the map in a webpage

Here it i a sample source code with a background and our layer: (I put leaflet fullscreen to impress girls)

```
<!doctype html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="initial-scale=1,user-scalable=no,maximum-scale=1,width=device-width">
        <meta name="mobile-web-app-capable" content="yes">
        <meta name="apple-mobile-web-app-capable" content="yes">
        <link rel="stylesheet" href="css/leaflet.css" />
        <script src="js/leaflet.js"></script>
	<script src="js/fullscreen.js"></script>
	<link href="fullscreen.css" rel='stylesheet' />	
        <style>
        #map {
            width: 1495px; /* no comment please :-) */
            height: 946px;
        }
        </style>
        <title>Sigfox Coverage Map</title>
    </head>
    <body style="margin:0">
        <div id="map">
        </div>
        <script>
        var map = L.map('map', {
	    fullscreenControl: true,
            zoomControl:true, maxZoom:11, minZoom:2
        }).fitBounds([[-86.1470045707,-25.4178198294],[85.3557580817,96.7495531352]]);

        bgLayer = L.tileLayer('https://whatyouwant.com/{z}/{x}/{y}');
        bgLayer.addTo(map);

	overlay = L.tileLayer('http://my/nginx/server/url/{z}/{x}/{y}.png',{maxNativeZoom:8});
	overlay.setOpacity(0.6);
        overlay.addTo(map);
        </script>
    </body>
</html>

```

And youre done :

![Wonderfull map](/public/images/webmap1/lightmap-world.png)

