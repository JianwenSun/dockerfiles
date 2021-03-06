FROM alpine  
MAINTAINER Guy Pascarella <guy.pascarella@gmail.com>  
  
ENV HOME /root  
ENV OSM2PGSQL_VERSION 0.90.1  
  
RUN echo "@testing http://dl-cdn.alpinelinux.org/alpine/edge/testing" >>
/etc/apk/repositories && \  
apk update  
  
# Install the things we want to stick around  
RUN apk add --no-cache \  
libgcc \  
libstdc++ \  
boost-filesystem \  
boost-system \  
boost-thread \  
expat \  
libbz2 \  
postgresql-libs \  
libpq \  
geos@testing \  
proj4@testing \  
lua5.2  
  
# Install develop tools and dependencies, build osm2pgsql and remove develop
tools and dependencies  
RUN apk add --no-cache \  
make \  
cmake \  
expat-dev \  
g++ \  
git \  
boost-dev \  
zlib-dev \  
bzip2-dev \  
proj4-dev@testing \  
geos-dev@testing \  
lua5.2-dev \  
postgresql-dev && \  
mkdir src &&\  
cd src &&\  
git clone --depth 1 --branch $OSM2PGSQL_VERSION
https://github.com/openstreetmap/osm2pgsql.git &&\  
cd osm2pgsql &&\  
mkdir build &&\  
cd build &&\  
cmake .. &&\  
make &&\  
make install &&\  
cd /root &&\  
rm -rf src &&\  
apk --purge del \  
make \  
cmake \  
git \  
g++ \  
boost-dev \  
gdbm \  
python3 \  
boost-python3 \  
python \  
binutils \  
gcc \  
lua5.2-dev \  
bzip2-dev \  
expat-dev \  
musl-dev \  
libc-dev \  
zlib-dev \  
openssl-dev \  
postgresql-dev \  
proj4-dev  
  
ENTRYPOINT ["/bin/sh"]  

