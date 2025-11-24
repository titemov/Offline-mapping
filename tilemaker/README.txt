docker run -it --rm -v "<absolute path>:/data" ghcr.io/systemed/tilemaker:master /data/hungary-251119.osm.pbf  --output /da
ta/hungary.mbtiles --config /data/config-openmaptiles.json --process /data/process-openmaptiles.lua

Use --merge to add another country to existing .mbtiles file:

docker run -it --rm -v "<absolute path>:/data" ghcr.io/systemed/tilemaker:master /data/slovakia-251115.osm.pbf  --output /da
ta/hungary.mbtiles --config /data/config-openmaptiles.json --process /data/process-openmaptiles.lua --merge

if limited RAM: --store

2GB .osm.pbf input file can be rendered within 16GB of RAM. If more it is necessary to run with "--store"

3.7GB .osm.pbf file with "--store" option needs ~110 GB of free disk memory


