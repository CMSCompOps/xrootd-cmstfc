ARG IMAGE=almalinux:8
FROM $IMAGE

MAINTAINER Sarun Nuntaviriyakul <sarun.nuntaviriyakul@cern.ch>
LABEL org.opencontainers.image.source https://github.com/guyzsarun/xrootd-cmsjson

WORKDIR /xrootd

ARG IMAGE=almalinux:8
RUN yum -y update && \
    yum install -y --skip-broken \
        dnf \
        https://repo.opensciencegrid.org/osg/3.6/osg-3.6-el$(echo $IMAGE | cut -d ":" -f 2)-release-latest.rpm \
        epel-release    \
        centos-release-scl

RUN dnf group install -y "Development Tools"

# CMS TFC dependency
RUN yum install -y  --enablerepo=osg-contrib  \
                    cmake3                   \
                    xrootd                   \
                    python3-devel            \
                    python3-xrootd           \
                    xrootd-devel             \
                    pcre-devel               \
                    xerces-c-devel           \
                    jsoncpp                  \
                    jsoncpp-devel


# For Centos 7
RUN if [[ $(echo $IMAGE | cut -d ":" -f 2) = "7" ]]; then \
    yum install -y devtoolset-7; \
    fi


RUN pip3 install pytest

COPY . .

RUN mkdir -p build                   &&  \
       cd build                      &&  \
       cmake .. -DBUILD_TEST=true    &&  \
       make                          &&  \
       make install

