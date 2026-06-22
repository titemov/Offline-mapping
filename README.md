# Offline-mapping
Offline mapping guide

![Wien](https://github.com/LazySloth322/Offline-mapping/blob/main/Wien.png)

# Guide
## Software
1. Docker
2. tilemaker
3. tileserver-gl
4. Any browser
5. QGIS version 3.8 or higher (optional)

## Step #1
First of all you need to install Docker. To install use official [Docker website](https://www.docker.com/get-started/) or my [cheatsheet](https://github.com/LazySloth322/Offline-mapping/blob/main/Docker_installation.md)

After successful installation pull following images to use them offline:
- `ghcr.io/systemed/tilemaker:master`
- `maptiler/tileserver-gl:latest`

To pull Docker image use `docker pull <image_name>`
> [!NOTE]
> If you are using linux: `sudo docker pull <image_name>`

> [!TIP]
> Downloading Docker images as `.tar` files: `docker save -o <path for generated tar file> <image name>`
>
> To load Docker image from `.tar` file run `docker load --input <image_name>.tar`

## Step #2
Download this repository!

Download `.osm.pbf` file of country or region you want from [Geofabrik](https://download.geofabrik.de/index.html)

Now it is obligatory needed to convert `.osm.pbf` to `.mbtiles` using `tilemaker`. Just move to folder, where `config-openmaptiles.json` and `process-openmaptiles.lua` are located, copy your `.osm.pbf` file there and simply run:

`docker run -it --rm -v "<Path to folder you in>:/data" ghcr.io/systemed/tilemaker:master /data/<name>.osm.pbf --output /data/<output_name>.mbtiles --config /data/config-openmaptiles.json --process /data/process-openmaptiles.lua`

**Merging**

Just add `--merge` and the end of the command above. Note: output `.mbtiles` file must already exist for a successful merge.

>[!NOTE]
> It is recommended to download the smallest object possible and then merging it up to something bigger (i.e. from different regions to whole country) if you have lower than 16GB of RAM.
>
>16GB of RAM will easily process `.osm.pbf` files up to ~1.5GB

## Step #3

- Move your `.mbtiles` file to `tileserver` folder
- Open `config.json` and change `*.mbtiles` to your `<output_name>.mbtiles` file name.
- Move to `tileserver` folder and then execute `docker run -it --rm -v "<Path to folder you in>:/data" -p 8080:8080 maptiler/tileserver-gl:latest`
- Open web-browser and enter `http://localhost:8080` link
- Select "Viewer"
- Zoom out until you see something on a map.
- Enjoy!

> [!NOTE]
> If any issuses seen (something not loading on different levels) please clear your browser cache within last day

## Optional step: setting up world ocean

- Install QGIS version 3.8 or higher
- Download [simplifed water polygons (Mercator)](https://osmdata.openstreetmap.de/data/water-polygons.html)
- Open QGIS. Select `Toolbox` in `Processing` tab
- Select `Raster tools` and click `Generating XYZ (mbtiles)`
- In opened menu select your `.shp` file, min zoom level `0` and max zoom level `10`. Change background color to `Blue` and select `PNG` format.
- Start processing. You will get `.mbtiles` file ~1GB size. Rename it to `worldocean.mbtiles`
- Add `"worldocean": { "mbtiles": "water-png.mbtiles" }` to `v3` in `config.json`
- Add `"worldocean":{ "type": "raster",	"url": "mbtiles://{worldocean}"	}` to `sources` in `style-local.json`
- Add `{ "id": "ocean-fill", "type": "raster", "source": "worldocean", "source-layer": "water-png", "layout": { "visibility": "visible" } },` to `layers` in `style-local.json`
- Watch step #3

# References:
1. [OpenStreetWiki](https://openstreetwiki.org)
2. [Tilemaker](https://github.com/systemed/tilemaker) ([Licence](https://github.com/systemed/tilemaker/blob/master/LICENCE.txt))
3. [tileserver-gl](https://github.com/maptiler/tileserver-gl) ([Licence](https://github.com/maptiler/tileserver-gl/blob/master/LICENSE.md))
4. [OSM-Liberty](https://github.com/maputnik/osm-liberty) ([Licence](https://github.com/maputnik/osm-liberty/blob/gh-pages/LICENSE.md))

All rights belongs to it authors.
