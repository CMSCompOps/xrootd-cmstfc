ARG IMAGE=almalinux:8
FROM $IMAGE

MAINTAINER Sarun Nuntaviriyakul <sarun.nuntaviriyakul@cern.ch>
LABEL org.opencontainers.image.source https://github.com/guyzsarun/xrootd-cmsjson

WORKDIR /xrootd

ARG IMAGE=almalinux:8
RUN yum -y update && \
    yum install -y \
        dnf \
        https://repo.opensciencegrid.org/osg/3.6/osg-3.6-el$(echo $IMAGE | cut -d ":" -f 2)-release-latest.rpm \
        epel-release

RUN dnf group install -y "Development Tools"

# CMS TFC dependency
RUN yum install -y  --enablerepo=osg-contrib \
                    cmake                    \
                    xrootd                   \
                    python3-devel            \
                    python3-xrootd           \
                    xrootd-devel             \
                    pcre-devel               \
                    xerces-c-devel           \
                    jsoncpp                  \
                    jsoncpp-devel

COPY . .

RUN mkdir -p build                   &&  \
       cd build                      &&  \
       cmake .. -DBUILD_TEST=true    &&  \
       make                          &&  \
       make install

