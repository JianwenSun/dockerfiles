FROM ubuntu:16.04  
MAINTAINER b@zi.is  
  
ENV BIND_USER=bind \  
BIND_VERSION=1:9.10.3 \  
WEBMIN_VERSION=1.8 \  
DATA_DIR=/data  
  
RUN rm -rf /etc/apt/apt.conf.d/docker-gzip-indexes \  
&& apt-get update \  
&& DEBIAN_FRONTEND=noninteractive apt-get -y install wget \  
&& wget http://www.webmin.com/jcameron-key.asc -qO - | apt-key add - \  
&& echo "deb http://download.webmin.com/download/repository sarge contrib" >>
/etc/apt/sources.list \  
&& apt-get update \  
&& DEBIAN_FRONTEND=noninteractive apt-get install -y bind9=${BIND_VERSION}*
bind9-host=${BIND_VERSION}* webmin=${WEBMIN_VERSION}* dnsutils \  
&& rm -rf /var/lib/apt/lists/*  
  
COPY entrypoint.sh /sbin/entrypoint.sh  
RUN chmod 755 /sbin/entrypoint.sh  
  
EXPOSE 53/udp 53/tcp 10000/tcp  
VOLUME ["${DATA_DIR}"]  
ENTRYPOINT ["/sbin/entrypoint.sh"]  
CMD ["/usr/sbin/named"]  

