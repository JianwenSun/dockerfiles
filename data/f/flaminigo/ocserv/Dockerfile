FROM debian:jessie  
  
# Install runtime packages  
RUN apt-get update && apt-get install -y gnutls-bin iptables libnl-route-3-200
libseccomp2 libwrap0 openssl --no-install-recommends && rm -rf
/var/lib/apt/lists/*  
  
# NOT FOUND?  
# libfreeradius-client-dev liblz4-dev libsystemd-daemon-dev  
# Use included:  
# libhttp-parser-dev libpcl1-dev libprotobuf-c0-dev libtalloc-dev  
  
RUN buildDeps=" \  
autoconf \  
autogen \  
ca-certificates \  
curl \  
gcc \  
gperf \  
libgnutls28-dev \  
libnl-route-3-dev \  
libpam0g-dev \  
libreadline-dev \  
libseccomp-dev \  
libwrap0-dev \  
make \  
pkg-config \  
xz-utils \  
libprotobuf-c0-dev \  
libev-dev \  
libtalloc-dev \  
libhttp-parser-dev \  
"; \  
set -x \  
&& apt-get update && apt-get install -y $buildDeps --no-install-recommends \  
&& apt-get install libev4 libtalloc2 libhttp-parser2.1 \  
&& rm -rf /var/lib/apt/lists/* \  
&& LZ4_VERSION=`curl "https://github.com/Cyan4973/lz4/releases/latest" | sed
-n 's/^.*tag\/\(.*\)".*/\1/p'` \  
&& curl -SL "https://github.com/Cyan4973/lz4/archive/$LZ4_VERSION.tar.gz" -o
lz4.tar.gz \  
&& mkdir -p /usr/src/lz4 \  
&& tar -xf lz4.tar.gz -C /usr/src/lz4 --strip-components=1 \  
&& rm lz4.tar.gz \  
&& cd /usr/src/lz4 \  
&& make -j"$(nproc)" \  
&& make install \  
&& OC_VERSION=`curl "http://www.infradead.org/ocserv/download.html" | sed -n
's/^.*version is <b>\(.*$\)/\1/p'` \  
&& curl -SL "ftp://ftp.infradead.org/pub/ocserv/ocserv-$OC_VERSION.tar.xz" -o
ocserv.tar.xz \  
&& curl -SL "ftp://ftp.infradead.org/pub/ocserv/ocserv-$OC_VERSION.tar.xz.sig"
-o ocserv.tar.xz.sig \  
# && gpg --keyserver pgp.mit.edu --recv-key 96865171 \  
# && gpg --verify ocserv.tar.xz.sig \  
&& mkdir -p /usr/src/ocserv \  
&& tar -xf ocserv.tar.xz -C /usr/src/ocserv --strip-components=1 \  
&& rm ocserv.tar.xz* \  
&& cd /usr/src/ocserv \  
&& sed -i '/#define MAX_CONFIG_ENTRIES /{s/64/200/}' src/vpn.h \  
&& ./configure \  
&& make -j"$(nproc)" \  
&& make install \  
&& mkdir -p /etc/ocserv \  
&& cp /usr/src/ocserv/doc/sample.config /etc/ocserv/ocserv.conf \  
&& cd / \  
&& rm -fr /usr/src/lz4 \  
&& rm -fr /usr/src/ocserv \  
&& apt-get purge -y --auto-remove $buildDeps  
  
# Setup config  
COPY route.txt /tmp/  
RUN set -x \  
&& sed -i 's/^#\(auth.*optional.*\)/\1/' /etc/ocserv/ocserv.conf \  
&& sed -i 's/\.\/sample\.passwd/\/etc\/ocserv\/ocpasswd/'
/etc/ocserv/ocserv.conf \  
&& sed -i 's/\(max-same-clients = \)2/\110/' /etc/ocserv/ocserv.conf \  
&& sed -i 's/\(listen-clear-file.*\)/#\1/' /etc/ocserv/ocserv.conf \  
&& sed -i 's/\.\.\/tests/\/etc\/ocserv/' /etc/ocserv/ocserv.conf \  
&& sed -i 's/#\(ca-cert = \).*/\1\/etc\/ocserv\/ca-cert\.pem/'
/etc/ocserv/ocserv.conf \  
&& sed -i 's/#\(compression.*\)/\1/' /etc/ocserv/ocserv.conf \  
&& sed -i 's/#\(occtl.*\)/\1/' /etc/ocserv/ocserv.conf \  
&& sed -i '/^ipv4-network = /{s/192.168.1.0/192.168.0.0/}'
/etc/ocserv/ocserv.conf \  
&& sed -i 's/192.168.1.2/8.8.8.8/' /etc/ocserv/ocserv.conf \  
&& sed -i 's/^route/#route/' /etc/ocserv/ocserv.conf \  
&& sed -i 's/\(^cookie-timeout = \)300/\186400/' /etc/ocserv/ocserv.conf \  
&& sed -i 's/#\(cisco.*\)/\1/' /etc/ocserv/ocserv.conf \  
&& sed -i 's/#enable-auth = "certificate"/enable-auth = "certificate"/'
/etc/ocserv/ocserv.conf \  
&& sed -i 's|^[# \t]*\(ca-cert = \).*|\1/etc/ocserv/ca-cert.pem|'
/etc/ocserv/ocserv.conf \  
&& sed -i 's|^[# \t]*\(crl = \).*|\1/etc/ocserv/crl.pem|'
/etc/ocserv/ocserv.conf \  
&& sed -i 's|^[# \t]*\(cert-user-oid = \).*|\12\.5\.4\.3|'
/etc/ocserv/ocserv.conf  
# && cat /tmp/route.txt >> /etc/ocserv/ocserv.conf \  
# && rm -fr /tmp/route.txt  
  
WORKDIR /etc/ocserv  
  
#FIXME HERE Test if ocservauto works well  
COPY docker-entrypoint.sh /entrypoint.sh  
COPY ocservauto.sh /etc/ocserv/ocservauto.sh  
ENTRYPOINT ["/entrypoint.sh"]  
  
EXPOSE 443  
CMD ["ocserv", "-c", "/etc/ocserv/ocserv.conf", "-d 999", "-f"]  

