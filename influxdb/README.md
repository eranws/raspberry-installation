## Influxdb files explained

influxdb.conf - The configuration file for the influxdb docker  

scripts/influxdb-init.iql - An influxdb init script to create a 'kivsee' database with no auth required

The script can be used to create the database file using docker:  
`docker run --rm -v $PWD:/var/lib/influxdb -v $PWD/scripts:/docker-entrypoint-initdb.d influxdb:1.8 /init-influxdb.sh`

meta/meta.db - The influxdb database file. The checked in version was created using the init script, meaning the 'kivsee' database is already created.  
This file is under .gitignore so to not be committed with ongoing database changes