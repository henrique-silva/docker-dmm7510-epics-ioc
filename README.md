# Docker image for Keithley DMM7510 EPICS IOC

This repository contains the Dockerfile used to create the Docker image with the
[EPICS IOC for the Keithley DMM7510](https://github.com/lnls-dig/dmm7510-epics-ioc).
It also contains two other IOCs that use it for a higher level application, more
specifically the ICT and the DCCT IOCs.

## Running the IOCs

The simples way to run the IOC is to run:

    docker run --rm -it --net host lnlsdig/dmm7510-epics-ioc -i IPADDR

where `IPADDR` is the IP address of the device to connect to. The options you
can specify (after `lnlsdig/dmm7510-epics-ioc`):

- `-i IPADDR`: device IP address to connect to (required)
- `-p IPPORT`: device IP port number to connect to (default: 5025)
- `-d DEVICE`: device identifier ([DCCT<number>|ICT<number>|DMM<number>]) (required)
- `-P PREFIX1`: the value of the EPICS `$(P)` macro used to prefix the PV names
- `-R PREFIX2`: the value of the EPICS `$(R)` macro used to prefix the PV names

## Creating a Persistent Container

If you want to create a persistent container to run the IOC, you can run a
command similar to:

    docker run -it --net host --restart always --name CONTAINER_NAME lnlsdig/dmm7510-epics-ioc -i IPADDR

where `IPADDR` is as in the previous section and `CONTAINER_NAME` is the name
given to the container. You can also use the same options as described in the
previous section.

## Building the Image Manually

To build the image locally without downloading it from Docker Hub, clone the
repository and run the `docker build` command:

    git clone https://github.com/lnls-dig/docker-dmm7510-epics-ioc
    docker build -t lnlsdig/dmm7510-epics-ioc docker-dmm7510-epics-ioc
