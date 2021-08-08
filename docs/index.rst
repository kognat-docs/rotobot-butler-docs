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
    docker-compose up

Prerequisites
-------------
Prerequisites are NVIDIA Docker for GPU containers

Docker is pivotal to machine learning training, it allows a run time environment to be exactly 
as needed for the machine training to succeed. Adding support for GPU Hardware is role of the
NVIDIA Docker.

Follow the guides found here
https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html



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
