FROM python:3-alpine  
MAINTAINER Arne Schubert<atd.schubert@gmail.com>  
  
ARG MAPPROXY_VERSION=1.7.0  
ENV MAPPROXY_VERSION $MAPPROXY_VERSION  
ENV MAPPROXY_PROCESSES 4  
ENV MAPPROXY_THREADS 2  
RUN set -x \  
&& apk add --no-cache --virtual .build-deps \  
build-base linux-headers curl \  
zlib-dev jpeg-dev \  
&& apk add --no-cache \  
\--repository http://dl-cdn.alpinelinux.org/alpine/edge/testing \  
gdal-dev proj4-dev geos-dev \  
&& adduser -h /mapproxy -s /bin/sh -D mapproxy \  
&& pip install Shapely Pillow requests geojson uwsgi pyproj
MapProxy==$MAPPROXY_VERSION \  
&& apk del build-base \  
&& rm -Rf /root/* /root/.cache \  
&& mkdir -p /docker-entrypoint-initmapproxy.d  
  
COPY docker-entrypoint.sh /  
ENTRYPOINT ["/docker-entrypoint.sh"]  
CMD ["mapproxy"]  
  
USER mapproxy  
VOLUME ["/mapproxy"]  
EXPOSE 8080  
# Stats  
EXPOSE 9191  

