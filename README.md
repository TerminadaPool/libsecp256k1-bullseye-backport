# How to backport libsecp256k1
This document explains how to backport libsecp256k1 yourself for a Debian
stable (Bullseye) system using the source files from testing (Bookworm).

### Install the build dependencies
As root:  
```
apt build-dep libsecp256k1
```

### Create build working directory
As user:  
```
basedir="${HOME}/src/bookworm-source/libsecp256k1"; \
mkdir -p "${basedir}"; \
cd "${basedir}"; \
unset basedir;
```

### Lookup package in Debian Bookworm package repository
Search for libsecp256k1 at: https://www.debian.org/distrib/packages  
Example search: https://packages.debian.org/search?keywords=libsecp256k1&searchon=sourcenames&suite=all&section=all  
Then Click 'bookworm' link  

Download the debian package source files  
```
wget http://deb.debian.org/debian/pool/main/libs/libsecp256k1/libsecp256k1_0.2.0-2.dsc; \
wget http://deb.debian.org/debian/pool/main/libs/libsecp256k1/libsecp256k1_0.2.0.orig.tar.xz; \
wget http://deb.debian.org/debian/pool/main/libs/libsecp256k1/libsecp256k1_0.2.0-2.debian.tar.xz
```

Extract the package files  
```
dpkg-source -x libsecp256k1_0.2.0-2.dsc
```

Change into newly created directory and build the packages  
```
cd libsecp256k1-0.2.0; \
debuild -us -uc -b;
```

Install the packages with  
```
dpkg -i libsecp256k1-1_0.2.0-2_amd64.deb libsecp256k1-dev_0.2.0-2_amd64.deb
```


https://www.debian.org/distrib/packages  
Example search: https://packages.debian.org/search?keywords=libsecp256k1&searchon=sourcenames&suite=all&section=all  
Then Click 'bookworm' link  

Download the debian package source files  
```
wget http://deb.debian.org/debian/pool/main/libs/libsecp256k1/libsecp256k1_0.2.0-2.dsc; \
wget http://deb.debian.org/debian/pool/main/libs/libsecp256k1/libsecp256k1_0.2.0.orig.tar.xz; \
wget http://deb.debian.org/debian/pool/main/libs/libsecp256k1/libsecp256k1_0.2.0-2.debian.tar.xz
```

Extract the package files  
```
dpkg-source -x libsecp256k1_0.2.0-2.dsc
```

Change into newly created directory and build the packages  
```
cd libsecp256k1-0.2.0; \
debuild -us -uc -b;
```

Install the packages with  
```
dpkg -i libsecp256k1-1_0.2.0-2_amd64.deb libsecp256k1-dev_0.2.0-2_amd64.deb
```




****
### Alternative method
****
This method involves adding Bookworm source to your /etc/apt/sources.list  

Add Debian bookworm (testing) source  
```
deb-src http://ftp.au.debian.org/debian bookworm main
```

Install build dependencies  
As root  
```
apt update; \
apt build-dep libsecp256k1;
```

Download and build the debs  
As builder user  
```
basedir="${HOME}/src/bookworm-source/libsecp256k1"; \
mkdir -p "${basedir}"; \
cd "${basedir}"; \
unset basedir; \

apt -b source libsecp256k1
```

You might want to remove the bookworm source line from your sources.list now so you don't mistakenly use the bookworm repository for other source packages.
