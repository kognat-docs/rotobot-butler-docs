Rotobot Butler
==============

Rotobot Butler will enable you to do what many people has asked for as a feature from the Rotobot OpenFX Plugin:

You can Rotobot with custom Rotoscoping as ground truth and use it within your OpenFX package.

There is no need to be a machine learning expert

Once the installation is complete by your systems' adminstration team, 
using Rotobot Butler is a matter of connecting a browser to the server
with NVIDIA GPU attached and training the deep convolutional neural network

Look how easy it is to use: ::

    docker-compose up 

Features
--------

- Create a Rotobot Butler set of trained weights for your data
- Create a node in your OpenFX host and browse to the weights

.. toctree::
   :maxdepth: 2

   groundtruth

Installation
------------

Install Rotobot Butler by running: ::

    chmod +x rotobot_butler_installer_Linux.sh
    sudo ./rotobot_butler_installer_Linux.sh
    cd /opt/Kognat/rotobot_butler
    docker load < rotobot-trainer-docker_kognatbutler_latest.tar.gz
    export kognat_LICENSE=2102@licenses.your-company.lan
    docker-compose up

Details of Using Docker
-----------------------

Initially getting the Docker image on your systems

Please refer to https://docs.docker.com/engine/reference/commandline/load/

The docker image is provided as a Gzip archive of a TAR file `rotobot-trainer-docker_kognatbutler_latest.tar.gz`

To check you do not already have the image use docker images: ::
    
    docker images | grep rotobot-trainer-docker_kognatbutler

The result should be an empty list if Rotobot Butler is not yet installed

To make this part of the Docker images available to your computer use `docker load` as follows from the install directory: ::

    cd /opt/Kognat/rotobotbutler-alpha
    docker load < rotobot-trainer-docker_kognatbutler_latest.tar.gz

Now the docker image should now be installed if the message above was without error: ::

    docker images

This will show the image for Rotobot Butler is installed: ::

    repository                             tag            image id      created       size
    rotobot-trainer-docker_kognatbutler    latest         1234abe67d    X weeks ago   9.8Gb 
   
Using Docker Compose is a matter of launching the Image above with some volume mounts and environment variables: ::

    services:
    train:
        image: rotobot-trainer-docker_kognatbutler:latest
        environment:
        - 'PYTHONPATH=$PYTHONPATH:/app/models/research:/app/models/research/slim'
        - 'kognat_LICENSE=${kognat_LICENSE}'
        volumes:
        - "${PWD}/data:/app/models/research/deeplab/data"
        runtime: nvidia
        tty: true
        mem_limit: 48GB
        expose:
            - "8888"
            - "7777"
        ports:
            - "8888:8888"
            - "7777:7777"
        deploy:
        resources:
            reservations:
            devices:
            - capabilities: [gpu]

So to make sure things work, make sure port `7777` and `8888` are free also ensure that you have a license server running on a port you can access.

After telling our shell environment where to find licenses with the `kognat_LICENSE` to `port@host` where the license server is running.


Lauching the Docker process with `docker-compose`: ::

   export kognat_LICENSE=2102@license.your-company.lan
   docker-compose up

RLM License server
------------------

You can download a Reprise License Manager server with the Kognat `.set` file from the following locations

Windows: https://bit.ly/linux-rlm-kognat-12-3

Mac OS: https://bit.ly/mac-osx-rlm-kognat-12-3

Windows: https://bit.ly/windows-rlm-kognat-12-3

Follow the detailed instructions about running a floating license, which is required to work a Docker container.

The important thing is that you hint to the Docker process about where to find a license by using the environment variable `kognat_LICENSE`

You need to set the value of `kognat_LICENSE` to `port@host` 

for example in a bash shell on Linux we would use

`export kognat_LICENSE=2102@licenses.kognat.com`
or 
`export kognat_LICENSE=9981@10.11.11.2`

Detailed instructions about running the RLM kognat server on your network: ::

   https://rotobot-docs.readthedocs.io/en/latest/licensing.html#floating-license-installation


Prerequisites
-------------
Prerequisites are NVIDIA Docker for GPU containers

Docker is pivotal to machine learning training, it allows a run time environment to be exactly 
as needed for the machine training to succeed. Adding support for GPU Hardware is role of the
NVIDIA Docker.

Follow the guides found here
https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html

Active RLM server with signed kognat license.


Contribute
----------

- Issue Tracker: https://github.com/kognat-docs/rotobot-butler-docs/issues
- Source Code: https://github.com/kognat-docs/rotobot-butler-docs

Support
-------

If you are having issues, please let us know.
We have a mailing list located at: sales@kognat.com

License
-------

The project is licensed under a custom EULA that is available from sales@kognat.com
