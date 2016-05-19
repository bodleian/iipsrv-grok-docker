Docker build of IIP Image Server 1.0 with Grok 1.0
==============================================

A Dockfile deployment of IIP image server with OPENJPEG @ https://github.com/GrokImageCompression/grok and https://github.com/stweil/iipsrv/tree/openjpeg

Docker hub respository @ https://hub.docker.com/r/bdlss/iipsrv-grok-docker/

Build successes are logged @ https://hub.docker.com/r/bdlss/iipsrv-grok-docker/builds/

IIIF validator v 1.0.0 @ https://pypi.python.org/pypi/iiif-validator/1.0.0

Please also refer to https://github.com/moravianlibrary/iipsrv-openjpeg/issues/2

### Use  pre-built image
Download image from docker hub. Defaults to `latest` tag. Docker will normally run as root unless otherwise configured.

    $ sudo docker pull bdlss/iipsrv-grok-docker

To run the docker command without sudo, you need to add your user (who must have root privileges) to the docker group. To do this run following command:

	$ sudo usermod -aG docker <user_name>

### Build from scratch (optional)
Use local Dockerfile to build image. Defaults to `latest` tag.

    $ sudo docker build -t bdlss/iipsrv-grok-docker .

### Start the container
Defaults to `latest` tag.

    $ sudo docker run -d -p 80:80 bdlss/iipsrv-grok-docker

This will push the docker container port 80 to your localhost port 80. Change the first parameter to 8080 if required (i.e. you already have a webserver running on your local machine).

### Images

The Dockerfile creates a `/var/www/localhost/images/` directory and downloads a test JPEG2000 from http://iiif-test.stanford.edu/67352ccc-d1b0-11e1-89ae-279075081939.jp2 and a test TIF from http://merovingio.c2rmf.cnrs.fr/iipimage/PalaisDuLouvre.tif.

### Test

Point your browser to `http://localhost/fcgi-bin/iipsrv.fcgi?IIIF=67352ccc-d1b0-11e1-89ae-279075081939.jp2/full/full/0/default.jpg`

Or `http://localhost/fcgi-bin/iipsrv.fcgi?IIIF=PalaisDuLouvre.tif/full/full/0/default.jpg`

After starting the container, you can IIIF validate your images from the container command line:

To get to the container command line use:

```bash
docker ps
docker exec -it <container ID> /bin/bash
```

Then for an image served at `http://localhost:8080/prefix/image_id` the validator can be run with:

    $ /tmp/iiif-validate.py -s localhost:8080 -p prefix -i image_id --version=2.0 -v

e.g.

    $ /tmp/iiif-validator-0.9.1/iiif-validate.py -s localhost:80 -p "fcgi-bin/iipsrv.fcgi?IIIF=" -i var/www/localhost/images/67352ccc-d1b0-11e1-89ae-279075081939.jp2 --version=2.0 -v

### Documentation and examples

Further documentation and examples are available here http://iipimage.sourceforge.net/.
