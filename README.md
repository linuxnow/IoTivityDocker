# IoTivityDocker

IoTivity build environment for Fedora and Ubuntu.
Sample thermostat device included.

How to use these Dockerfiles

To build a base image, with IoTivity built and installed:

    git clone git@github.com:datasnap-io/IoTivityDocker.git
    cd IoTivityDocker

For Ubuntu:

    docker build -t linuxnow/iotivity-ubuntu:1.2-rel ubuntu

For Fedora:

    docker build -t linuxnow/iotivity-fedora:1.2-rel fedora

By default, the image is built with the following functionality flags defined:

    SECURED=1
    RELEASE=true
    LOGGING=true

Specialized versions with different values for these flags can be created as well:

    docker build -t linuxnow/iotivity-ubuntu-quiet --build-arg LOGGING=false ubuntu

If you are interested in invoking Thermostat...

    docker build ./example -t thermostat
    docker run -it thermostat ./Thermostat
