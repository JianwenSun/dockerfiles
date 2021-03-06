FROM debian:stretch-
slim@sha256:ea42520331a55094b90f6f6663211d4f5a62c5781673935fe17a4dfced777029  
  
# add our user and group first to make sure their IDs get assigned
consistently, regardless of whatever dependencies get added  
#RUN groupadd -r www-data && useradd -r --create-home -g www-data www-data  
  
ENV HTTPD_PREFIX /usr/local/apache2  
ENV PATH $HTTPD_PREFIX/bin:$PATH  
RUN mkdir -p "$HTTPD_PREFIX" \  
&& chown www-data:www-data "$HTTPD_PREFIX"  
WORKDIR $HTTPD_PREFIX  
  
# library for mod_http2  
ENV NGHTTP2_VERSION 1.18.1-1  
ENV OPENSSL_VERSION 1.1.0f-3+deb9u1  
  
# install httpd runtime dependencies  
# https://httpd.apache.org/docs/2.4/install.html#requirements  
RUN export DEBIAN_FRONTEND=noninteractive \  
&& apt-get update \  
&& apt-get install -y --no-install-recommends \  
libapr1 \  
libaprutil1 \  
libaprutil1-ldap \  
libapr1-dev \  
libaprutil1-dev \  
liblua5.2-0 \  
libnghttp2-14=$NGHTTP2_VERSION \  
libpcre++0v5 \  
libssl1.1=$OPENSSL_VERSION \  
libxml2 \  
&& rm -r /var/lib/apt/lists/* \  
&& rm -rf /var/log/dpkg.log /var/log/alternatives.log /var/log/apt  
  
ENV HTTPD_VERSION 2.4.29  
ENV HTTPD_SHA256
777753a5a25568a2a27428b2214980564bc1c38c1abf9ccc7630b639991f7f00  
  
# https://httpd.apache.org/security/vulnerabilities_24.html  
ENV HTTPD_PATCHES=""  
#
https://issues.apache.org/jira/browse/INFRA-8753?focusedCommentId=14735394#comment-14735394  
# if the version is outdated (or we're grabbing the .asc file), we might have
to pull from the dist/archive :/  
ENV APACHE_DIST_URLS \  
https://www.apache.org/dyn/closer.cgi?action=download&filename= \  
https://www-us.apache.org/dist/ \  
https://www.apache.org/dist/ \  
https://archive.apache.org/dist/  
# see https://httpd.apache.org/docs/2.4/install.html#requirements  
# mod_http2 mod_lua mod_proxy_html mod_xml2enc  
# https://anonscm.debian.org/cgit/pkg-
apache/apache2.git/tree/debian/control?id=adb6f181257af28ee67af15fc49d2699a0080d4c  
RUN set -eux; \  
export DEBIAN_FRONTEND=noninteractive; \  
\  
buildDeps=" \  
bzip2 \  
ca-certificates \  
gnupg2 dirmngr \  
dpkg-dev \  
gcc \  
liblua5.2-dev \  
libnghttp2-dev=$NGHTTP2_VERSION \  
libpcre++-dev \  
libssl-dev=$OPENSSL_VERSION \  
libxml2-dev \  
zlib1g-dev \  
make \  
wget \  
"; \  
apt-get update; \  
apt-get install -y --no-install-recommends -V $buildDeps; \  
rm -r /var/lib/apt/lists/*; \  
\  
ddist() { \  
local f="$1"; shift; \  
local distFile="$1"; shift; \  
local success=; \  
local distUrl=; \  
for distUrl in $APACHE_DIST_URLS; do \  
if wget -O "$f" "$distUrl$distFile"; then \  
success=1; \  
break; \  
fi; \  
done; \  
[ -n "$success" ]; \  
}; \  
\  
ddist 'httpd.tar.bz2' "httpd/httpd-$HTTPD_VERSION.tar.bz2"; \  
echo "$HTTPD_SHA256 *httpd.tar.bz2" | sha256sum -c -; \  
\  
ddist 'httpd.tar.bz2.asc' "httpd/httpd-$HTTPD_VERSION.tar.bz2.asc"; \  
export GNUPGHOME="$(mktemp -d)"; \  
gpg --keyserver ha.pool.sks-keyservers.net --recv-keys
A93D62ECC3C8EA12DB220EC934EA76E6791485A8; \  
gpg --batch --verify httpd.tar.bz2.asc httpd.tar.bz2; \  
rm -rf "$GNUPGHOME" httpd.tar.bz2.asc; \  
\  
mkdir -p src; \  
tar -xf httpd.tar.bz2 -C src --strip-components=1; \  
rm httpd.tar.bz2; \  
cd src; \  
\  
patches() { \  
while [ "$#" -gt 0 ]; do \  
local patchFile="$1"; shift; \  
local patchSha256="$1"; shift; \  
ddist "$patchFile" "httpd/patches/apply_to_$HTTPD_VERSION/$patchFile"; \  
echo "$patchSha256 *$patchFile" | sha256sum -c -; \  
patch -p0 < "$patchFile"; \  
rm -f "$patchFile"; \  
done; \  
}; \  
patches $HTTPD_PATCHES; \  
\  
gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)"; \  
./configure \  
\--build="$gnuArch" \  
\--prefix="$HTTPD_PREFIX" \  
\--enable-mods-shared=reallyall \  
; \  
make -j "$(nproc)"; \  
make install; \  
\  
cd ..; \  
rm -r src man manual; \  
\  
sed -ri \  
-e 's!^(\s*CustomLog)\s+\S+!\1 /proc/self/fd/1!g' \  
-e 's!^(\s*ErrorLog)\s+\S+!\1 /proc/self/fd/2!g' \  
"$HTTPD_PREFIX/conf/httpd.conf"; \  
\  
apt-get purge -y --auto-remove $buildDeps; \  
rm -rf /var/log/dpkg.log /var/log/alternatives.log /var/log/apt; \  
rm -f /usr/local/apache2/logs/httpd.pid  
  
EXPOSE 80  
ENTRYPOINT ["httpd","-DFOREGROUND"]  

