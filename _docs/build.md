---
layout: docs
title: Build Soufflé
permalink: /docs/build/
---
## Pre-Build Packages

Soufflé has pre-built packages for Debian and MAC OS X. You find the pre-built packages [here](http://github.com/souffle-lang/souffle/releases/latest).

## Debian Systems

For Debian systems, the latest development version of Soufflé can be installed from the Bintray PPA,

[Bintray PPA](https://bintray.com/souffle-lang/deb-unstable)


You can update your system with unsupported packages from this untrusted PPA by adding https://dl.bintray.com/souffle-lang/deb-unstable to your system's Software Sources using the following instructions:

```
sudo apt-add-repository https://dl.bintray.com/souffle-lang/deb-unstable
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 379CE192D401AB61
sudo apt-get update
```


## Software Requirements

To build and install Souffle, the following software must be installed:

* Make, Autoconf tools, GNU G++ supporting C++11 and OpenMP (from version 4.8), Bison (from version 3.0.2), Flex, DoxyGen

CLANG++ with OpenMP support can be used as an alternative for G++.

### Ubuntu/Debian Build

On a Ubuntu/Debian system, following command installs the necessary developer tools to compile and build Soufflé:

```
sudo apt-get install autoconf automake bison build-essential clang doxygen flex g++ git libncurses5-dev libtool libsqlite3-dev make mcpp python sqlite zlib1g-dev
```

Support for C++11 is required, which is partly available in Ubuntu 16.04 with g++-4.8. More recent versions of Ubuntu, and Debian 8 and newer, have full support of C++11 with g++-5.0 on.

The Soufflé project follows automake/autoconf conventions for configuring, installing and building software. To configure, build, test, and install the project, type:
```
 cd souffle
 sh ./bootstrap
 ./configure
 make
```


### MAC OS X Build

MAC OS X does not have OpenMP/C++ nor a bison version 3.0.2 or higher installed. We recommend [brew](http://brew.sh) to install the required tools to build Soufflé. Run the following commands prior to executing `./configure`:
```
brew update
brew install autoconf automake bison libffi libtool mcpp pkg-config
brew reinstall gcc
brew link bison --force
brew link libffi --force
export PKG_CONFIG_PATH=/usr/local/opt/libffi/lib/pkgconfig/
```

Note: Be careful with the search path for bison, so it points to the correct one. By default, macOS includes bison 2.3 at `/usr/bin/bison`, however brew installs the newer version to `/usr/local/bin/bison`. This can be done by prepending this directory to the path, however, this can break other systems - `PATH=/usr/local/bin:$PATH`.

Soufflé is built by 

```
cd souffle
export CXX=g++-8
export CC=gcc-8
./bootstrap
./configure
make
```

### Testing Soufflé

With 
```
 make check
```
numerous unit tests and regression tests are performed. This may take up to 45min.
However, this may be sped up with, for instance:
```
TESTSUITEFLAGS=-j8 make check
```
which will run 8 jobs at a time.

### Installing Soufflé 

If you would like to install Soufflé in your system, specify an installation directory with `./configure --prefix=<install-dir>`. The executable, scripts, and header files will be stored in the directory ```<install-dir>```. Use an absolute path for ```<install-dir>```. Type 
```
 make install
```
to install Soufflé. By setting the path variable 
```
 PATH=$PATH:<install-dir>/bin
``` 
the Soufflé commands ```souffle``` and ```souffle-profile``` are available to the users.

