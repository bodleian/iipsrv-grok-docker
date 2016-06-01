Docker build of IIP Image Server 1.0 with Grok 1.0 on Ubuntu 14.04
==============================================

A Dockfile deployment of IIP image server with optimized OPENJPEG, Grok @ https://github.com/GrokImageCompression/grok and  https://github.com/stweil/iipsrv/tree/openjpeg

Docker hub respository @ https://hub.docker.com/r/bdlss/iipsrv-grok-docker/

Build successes are logged @ https://hub.docker.com/r/bdlss/iipsrv-grok-docker/builds/

IIIF validator v 1.0.0 @ https://pypi.python.org/pypi/iiif-validator/1.0.0

Please also refer to https://github.com/moravianlibrary/iipsrv-openjpeg/issues/2 and https://github.com/ruven/iipsrv/pull/61#issuecomment-222381601

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

To get to the container command line use:

```bash
docker ps
docker exec -it <container ID> /bin/bash
```

Removed validator as Pillow currently not compiling w/ Grok 1.0.

### Documentation and examples

Further documentation and examples are available here http://iipimage.sourceforge.net/.
