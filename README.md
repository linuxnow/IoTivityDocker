# IoTivityDocker

IoTivity build environment based on Ubuntu.
Sample thermostat device included.

How to use these Dockerfiles

To build a base image, with IoTivity built and installed:

    git clone git@github.com:datasnap-io/IoTivityDocker.git
    cd IoTivityDocker
    docker build ./base_image -t datasnap-io/iotivity-full

By default, the image is built with the following functionality flags defined:

    SECURED=1
    RELEASE=true
    LOGGING=true

Specialized versions with different values for these flags can be created as well:

    docker build ./base_image -t datasnap-io/iotivity-quiet --build-arg LOGGING=false

If you are interested in invoking Thermostat...

    docker build ./example -t thermostat
    docker run -it thermostat ./Thermostat
