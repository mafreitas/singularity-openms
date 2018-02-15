BootStrap: docker
From: ubuntu:16.04

%labels
MAINTAINER Michael A. Freitas

%setup

%environment
PATH=/usr/local/openms_thirdparty/All/:$PATH
PATH=/usr/local/openms_thirdparty/All/LuciPHOr2:$PATH
PATH=/usr/local/openms_thirdparty/All/MSGFPlus:$PATH
PATH=/usr/local/openms_thirdparty/All/Sirius:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/Comet:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/Fido:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/MyriMatch:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/OMSSA:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/Percolator:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/Sirius:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/SpectraST:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/XTandem:$PATH
PATH=/usr/local/bin/:$PATH
LD_LIBRARY_PATH=/usr/local/lib/:$LD_LIBRARY_PATH

%runscript

%post
apt-get -y update
apt-get install -y g++ autoconf patch libtool make git g++ automake
apt-get install -y software-properties-common python-software-properties
apt-get clean
apt-get purge
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


apt-get -y update
apt-get install -y cmake
apt-get install -y qt4-dev-tools qt4-default qt4-qtconfig qt4-qmake
apt-get install -y libqt4-dev libqt4-opengl-dev libqt4-svg
apt-get install -y libqtwebkit4 libqtwebkit-dev
apt-get install -y libsvm-dev libglpk-dev \
                    libzip-dev zlib1g-dev \
                    libxerces-c-dev \
                    libbz2-dev
apt-get install -y libboost-date-time-dev \
                    libboost-iostreams-dev \
                    libboost-regex-dev \
                    libboost-math-dev \
                    libboost-random-dev
apt-get clean
apt-get purge
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
add-apt-repository -y ppa:webupd8team/java
apt-get -y update
apt-get install -y oracle-java8-installer
apt-get clean
apt-get purge
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

mkdir /build_tmp
cd /build_tmp
git clone https://github.com/OpenMS/contrib.git
rm -rf contrib/.git/
mkdir contrib-build
cd contrib-build

cmake -DBUILD_TYPE=SEQAN ../contrib && rm -rf archives src
cmake -DBUILD_TYPE=WILDMAGIC ../contrib && rm -rf archives src
cmake -DBUILD_TYPE=EIGEN ../contrib && rm -rf archives src
cmake -DBUILD_TYPE=COINOR ../contrib && rm -rf archives src
cmake -DBUILD_TYPE=SQLITE ../contrib && rm -rf archives src

cd /build_tmp
git clone https://github.com/OpenMS/OpenMS.git
cd OpenMS
git checkout tags/Release2.3.0
hash=`git log | head -n 1 | cut -f 2 -d ' '`
sed -i "s/OPENMS_GIT_SHA1/\"$hash\"/" src/openms/source/CONCEPT/VersionInfo.cpp
rm -rf .git/ share/OpenMS/examples/

cd /usr/local/

git clone https://github.com/OpenMS/THIRDPARTY.git openms_thirdparty
rm -rf .git Windows MacOS Linux/32bit

cd /build_tmp
mkdir openms-build
cd openms-build

cmake -DCMAKE_PREFIX_PATH="/home/biodocker/contrib-build/;/usr/;/usr/local" \
        -DCMAKE_INSTALL_PREFIX=/usr/local/ \
        -DBOOST_USE_STATIC=OFF \
        -DHAS_XSERVER=Off ../OpenMS
make TOPP -j6
make UTILS -j6
make install -j6
rm -rf src doc CMakeFiles

cd /usr/local/
zip -r openms2.3.0.zip lib/lib* share/OpenMS/* bin/*
cd /
rm -rf /build_tmp
