# Offline-mapping
Offline mapping guide

# Guide
## Software
1. Docker
2. QGIS version 3.8 or higher
3. tilemaker
4. tileserver-gl

## Step 1
First of all you need to install Docker. To install it use official Docker website or my [cheatsheet](https://github.com/titemov/Offline-mapping/blob/main/Docker_installation.md)
After successful installation pull following images:
- `ghcr.io/systemed/tilemaker:master`
- `maptiler/tileserver-gl:latest`

To pull Docker image use `docker pull <image_name>`
> [!NOTE]
> If you are using linux: `sudo docker pull <image_name>`

# References:
1. [OpenStreetWiki](openstreetwiki.org)
2. [Tilemaker](https://github.com/systemed/tilemaker) ([Licence](https://github.com/systemed/tilemaker/blob/master/LICENCE.txt))
3. [tileserver-gl](https://github.com/maptiler/tileserver-gl) ([Licence](https://github.com/maptiler/tileserver-gl/blob/master/LICENSE.md))
4. [OSM-Liberty](https://github.com/maputnik/osm-liberty) ([Licence](https://github.com/maputnik/osm-liberty/blob/gh-pages/LICENSE.md))

All rights belongs to it authors.
