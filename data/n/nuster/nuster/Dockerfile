FROM debian:stretch-slim  
  
ARG NUSTER_VERSION=1.8.8.2  
ARG
NUSTER_DL_URL=https://github.com/jiangwenyuan/nuster/releases/download/v$NUSTER_VERSION/nuster-$NUSTER_VERSION.tar.gz  
ARG NUSTER_DL_FILE=nuster.tar.gz  
ARG NUSTER_SRC_DIR=/tmp/nuster  
  
RUN set -x \  
&& buildDeps=' \  
gcc \  
libc6-dev \  
liblua5.3-dev \  
libpcre3-dev \  
libssl-dev \  
zlib1g-dev \  
' \  
&& tools=' \  
ca-certificates \  
make \  
wget \  
' \  
&& runtimes=' \  
libpcre3 \  
libssl1.1 \  
liblua5.3-0 \  
' \  
&& apt-get update \  
&& apt-get install -y --no-install-recommends $buildDeps $tools $runtimes \  
&& rm -r /var/lib/apt/lists/* \  
\  
&& mkdir -p $NUSTER_SRC_DIR \  
&& wget -O /tmp/$NUSTER_DL_FILE $NUSTER_DL_URL \  
&& tar -xvf /tmp/$NUSTER_DL_FILE -C $NUSTER_SRC_DIR --strip-components=1 \  
\  
&& makeOpts=' \  
TARGET=linux2628 \  
USE_LUA=1 \  
LUA_INC=/usr/include/lua5.3 \  
USE_OPENSSL=1 \  
USE_PCRE=1 \  
PCREDIR= \  
USE_ZLIB=1 \  
' \  
&& make -C $NUSTER_SRC_DIR -j "$(nproc)" all $makeOpts \  
&& make -C $NUSTER_SRC_DIR install-bin $makeOpts \  
\  
&& mkdir -p /etc/nuster \  
&& cp -R $NUSTER_SRC_DIR/examples/errorfiles /etc/nuster/errors \  
&& rm -rf /tmp/nuster* \  
\  
&& apt-get purge -y --auto-remove $buildDeps  
  
COPY docker-entrypoint.sh /  
ENTRYPOINT ["/docker-entrypoint.sh"]  
CMD ["haproxy", "-f", "/etc/nuster/nuster.cfg"]  

