# xrootd-cmstfc

[![pipeline](https://github.com/CMSCompOps/xrootd-cmstfc/actions/workflows/main.yaml/badge.svg?branch=master)](https://github.com/CMSCompOps/xrootd-cmstfc/actions/workflows/main.yaml)

## Description

CMS JSON and XML module for [Open Storage System]() using XRootD Name2Name interface 


## Installation


### Building from Source
```
git clone https://github.com/CMSCompOps/xrootd-cmstfc
```

```
mkdir build && cd build
cmake .. 
make install
```

### Building XML and JSON Test

Build executable to test the xml and json module conversion
```
mkdir build && cd build
cmake .. -DBUILD_TEST=true
make
```
Test storage.xml 
```
./test_xml.o   /store/temp/1 'file:/path_to/storage.xml?protocol=root'
```
Test storage.json

```
./test_json.o  /store/temp/1 'file:/path_to/storage.json?volume=TX_XX_XXX&protocol=root'
```

## Usage

Add the shared library ( libXrdCmsTfc.so or libXrdCmsJson.so ) to [oss.namelib](https://xrootd.slac.stanford.edu/doc/dev50/ofs_config.htm#_Toc43842855) section in the xrootd configuration file


```
# xrootd-configuration.cfg

oss.namelib /usr/lib64/libXrdCmsTfc.so  file:/path_to/storage.xml?protocol=root

or 

oss.namelib /usr/lib64/libXrdCmsJson.so file:/path_to/storage.json?volume=TX_XX_XXX&protocol=root

```