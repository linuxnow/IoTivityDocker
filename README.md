# IoTivityDocker
Secure IoTivity build environment based on Ubuntu.
Sample thermostat device included.

How to use these Dockerfiles

To build a base image, with IoTivity built and installed:

    git clone git@github.com:datasnap-io/IoTivityDocker.git
    docker build -t='datasnap-io/iotivity-full' IoTivityDocker/base_image

If you are interested in invoking Thermostat...

    docker build -t='thermostat' IoTivityDocker/example
    docker run -it thermostat /root/runThermostat.sh
