# Dockerfile - alpine  
# https://github.com/openresty/docker-openresty  
  
FROM alpine:3.4  
  
LABEL maintainer="Evan Wies <evan@neomantra.net>"  
LABEL maintainer="Dmitry Kireev <dmitry@kireev.co>"  
  
# Docker Build Arguments  
ARG RESTY_VERSION="1.11.2.5"  
ARG RESTY_OPENSSL_VERSION="1.0.2k"  
ARG RESTY_PCRE_VERSION="8.40"  
ARG RESTY_PAGESPEED_VERSION="1.11.33.3"  
ARG LIBPNG_VERSION="1.2.56"  
ARG RESTY_J="1"  
ARG RESTY_CONFIG_OPTIONS="\  
\--with-file-aio \  
\--with-http_addition_module \  
\--with-http_auth_request_module \  
\--with-http_dav_module \  
\--with-http_flv_module \  
\--with-http_geoip_module=dynamic \  
\--with-http_gunzip_module \  
\--with-http_gzip_static_module \  
\--with-http_image_filter_module=dynamic \  
\--with-http_mp4_module \  
\--with-http_random_index_module \  
\--with-http_realip_module \  
\--with-http_secure_link_module \  
\--with-http_slice_module \  
\--with-http_ssl_module \  
\--with-http_stub_status_module \  
\--with-http_sub_module \  
\--with-http_v2_module \  
\--with-http_xslt_module=dynamic \  
\--with-ipv6 \  
\--with-mail \  
\--with-mail_ssl_module \  
\--with-md5-asm \  
\--with-pcre-jit \  
\--with-sha1-asm \  
\--with-stream \  
\--with-stream_ssl_module \  
\--with-threads \  
\--with-cc-opt=-fPIC \  
\--with-cc-opt=-I/usr/include/apr-1 \  
\--with-ld-opt=-luuid \  
\--with-ld-opt=-lapr-1 \  
\--with-ld-opt=-laprutil-1 \  
\--with-ld-opt=-licudata \  
\--with-ld-opt=-licuuc \  
\--with-ld-opt=-L/tmp/modpagespeed-${RESTY_PAGESPEED_VERSION}/usr/lib \  
\--with-ld-opt=-lpng12 \  
\--with-ld-opt=-lturbojpeg \  
\--with-ld-opt=-ljpeg \  
"  
  
ARG RESTY_CONFIG_OPTIONS_MORE=""  
  
# These are not intended to be user-specified  
ARG _RESTY_PAGESPEED_RELEASE="beta"  
ARG _RESTY_CONFIG_DEPS="--with-openssl=/tmp/openssl-${RESTY_OPENSSL_VERSION}
--add-
module=/tmp/ngx_pagespeed-${RESTY_PAGESPEED_VERSION}-${_RESTY_PAGESPEED_RELEASE}
--with-pcre=/tmp/pcre-${RESTY_PCRE_VERSION} "  
  
# 1) Install apk dependencies  
# 2) Download and untar OpenSSL, PCRE, and OpenResty  
# 3) Build OpenResty  
# 4) Cleanup  
  
RUN apk add --no-cache --virtual .build-deps \  
build-base \  
curl \  
gd-dev \  
geoip-dev \  
libxslt-dev \  
linux-headers \  
make \  
perl-dev \  
readline-dev \  
zlib-dev \  
python \  
icu icu-libs icu-dev \  
bash \  
gperf \  
libjpeg-turbo \  
apr \  
apr-util \  
apr-dev \  
apr-util-dev \  
libjpeg-turbo-dev \  
apache2-dev \  
zlib-dev \  
gperf \  
git \  
&& apk add --no-cache \  
gd \  
geoip \  
libgcc \  
libxslt \  
zlib \  
\  
&& cd /tmp \  
&& curl -fSL
https://www.openssl.org/source/openssl-${RESTY_OPENSSL_VERSION}.tar.gz | tar
-zx \  
&& curl -fSL https://ftp.pcre.org/pub/pcre/pcre-${RESTY_PCRE_VERSION}.tar.gz |
tar -zx \  
&& curl -fSL https://openresty.org/download/openresty-${RESTY_VERSION}.tar.gz
| tar -zx \  
&& curl -fSL https://dl.google.com/dl/linux/mod-
pagespeed/tar/${_RESTY_PAGESPEED_RELEASE}/mod-
pagespeed-${_RESTY_PAGESPEED_RELEASE}-${RESTY_PAGESPEED_VERSION}-r0.tar.bz2 |
tar -jx \  
&& curl -fSL
https://github.com/pagespeed/ngx_pagespeed/archive/v${RESTY_PAGESPEED_VERSION}-${_RESTY_PAGESPEED_RELEASE}.tar.gz
| tar -zx \  
&& curl -fSL
https://github.com/glennrp/libpng/archive/v${LIBPNG_VERSION}.tar.gz | tar -zx
\  
\  
&& cd /tmp/libpng-${LIBPNG_VERSION} \  
&& ./configure --build=$CBUILD --host=$CHOST --prefix=/usr --enable-shared
--with-libpng-compat \  
&& make install V=0 \  
&& cd /tmp/modpagespeed-${RESTY_PAGESPEED_VERSION} \  
  
&& curl -L https://raw.githubusercontent.com/kireevco/docker-
openresty/master/alpine/patches/automatic_makefile.patch | patch -p1 \  
&& curl -L https://raw.githubusercontent.com/kireevco/docker-
openresty/master/alpine/patches/libpng_cflags.patch | patch -p1 \  
&& curl -L https://raw.githubusercontent.com/kireevco/docker-
openresty/master/alpine/patches/pthread_nonrecursive_np.patch | patch -p1 \  
&& curl -L https://raw.githubusercontent.com/kireevco/docker-
openresty/master/alpine/patches/rename_c_symbols.patch | patch -p1 \  
&& curl -L https://raw.githubusercontent.com/kireevco/docker-
openresty/master/alpine/patches/stack_trace_posix.patch | patch -p1 \  
\  
&& ./generate.sh -D use_system_libs=1 -D _GLIBCXX_USE_CXX11_ABI=0 -D
use_system_icu=1 \  
&& cd /tmp/modpagespeed-${RESTY_PAGESPEED_VERSION}/src \  
&& make BUILDTYPE=Release CXXFLAGS=" -I/usr/include/apr-1
-I/tmp/libpng-${LIBPNG_VERSION} -fPIC -D_GLIBCXX_USE_CXX11_ABI=0" CFLAGS="
-I/usr/include/apr-1 -I/tmp/libpng-${LIBPNG_VERSION} -fPIC
-D_GLIBCXX_USE_CXX11_ABI=0" \  
&& cd /tmp/modpagespeed-${RESTY_PAGESPEED_VERSION}/src/pagespeed/automatic/ \  
&& make psol BUILDTYPE=Release CXXFLAGS=" -I/usr/include/apr-1
-I/tmp/libpng-${LIBPNG_VERSION} -fPIC -D_GLIBCXX_USE_CXX11_ABI=0" CFLAGS="
-I/usr/include/apr-1 -I/tmp/libpng-${LIBPNG_VERSION} -fPIC
-D_GLIBCXX_USE_CXX11_ABI=0" \  
&& mkdir -p /tmp/ngx_pagespeed-${RESTY_PAGESPEED_VERSION}-beta/psol \  
&& mkdir -p
/tmp/ngx_pagespeed-${RESTY_PAGESPEED_VERSION}-beta/psol/lib/Release/linux/x64
\  
&& mkdir -p
/tmp/ngx_pagespeed-${RESTY_PAGESPEED_VERSION}-beta/psol/include/out/Release \  
&& cp -r /tmp/modpagespeed-${RESTY_PAGESPEED_VERSION}/src/out/Release/obj
/tmp/ngx_pagespeed-${RESTY_PAGESPEED_VERSION}-beta/psol/include/out/Release/ \  
&& cp -r /tmp/modpagespeed-${RESTY_PAGESPEED_VERSION}/src/net
/tmp/ngx_pagespeed-${RESTY_PAGESPEED_VERSION}-beta/psol/include/ \  
&& cp -r /tmp/modpagespeed-${RESTY_PAGESPEED_VERSION}/src/testing
/tmp/ngx_pagespeed-${RESTY_PAGESPEED_VERSION}-beta/psol/include/ \  
&& cp -r /tmp/modpagespeed-${RESTY_PAGESPEED_VERSION}/src/pagespeed
/tmp/ngx_pagespeed-${RESTY_PAGESPEED_VERSION}-beta/psol/include/ \  
&& cp -r /tmp/modpagespeed-${RESTY_PAGESPEED_VERSION}/src/third_party
/tmp/ngx_pagespeed-${RESTY_PAGESPEED_VERSION}-beta/psol/include/ \  
&& cp -r /tmp/modpagespeed-${RESTY_PAGESPEED_VERSION}/src/tools
/tmp/ngx_pagespeed-${RESTY_PAGESPEED_VERSION}-beta/psol/include/ \  
&& cp -r
/tmp/modpagespeed-${RESTY_PAGESPEED_VERSION}/src/pagespeed/automatic/pagespeed_automatic.a
/tmp/ngx_pagespeed-${RESTY_PAGESPEED_VERSION}-beta/psol/lib/Release/linux/x64
\  
\  
&& cd /tmp/openresty-${RESTY_VERSION} \  
&& LD_LIBRARY_PATH=/tmp/modpagespeed-${RESTY_PAGESPEED_VERSION}/usr/lib \  
&& ./configure -j${RESTY_J}\  
\--prefix=/var/lib/nginx \  
\--sbin-path=/usr/sbin \  
\--modules-path=/usr/lib/nginx \  
\--prefix=/etc/nginx \  
\--conf-path=/etc/nginx/nginx.conf \  
\--http-log-path=/var/log/nginx/access.log \  
\--error-log-path=/var/log/nginx/error.log \  
\--pid-path=/var/run/nginx.pid \  
${_RESTY_CONFIG_DEPS} \  
${RESTY_CONFIG_OPTIONS} \  
${RESTY_CONFIG_OPTIONS_MORE} \  
\  
&& make install --silent \  
&& apk del .build-deps \  
&& rm -rf /tmp/* \  
&& ln -sf /dev/stdout /var/log/nginx/access.log \  
&& ln -sf /dev/stderr /var/log/nginx/error.log \  
&& mkdir -p /var/cache/ngx_pagespeed \  
&& chmod -R o+wr /var/cache/ngx_pagespeed  
  
# Add additional binaries into PATH for convenience  
ENV
PATH=$PATH:/usr/local/openresty/luajit/bin/:/usr/local/openresty/nginx/sbin/:/usr/local/openresty/bin/  
  
# Copy nginx configuration files  
COPY nginx.conf /usr/local/openresty/nginx/conf/nginx.conf  
COPY nginx.vh.default.conf /etc/nginx/conf.d/default.conf  
  
CMD ["/usr/local/openresty/bin/openresty", "-g", "daemon off;"]  

