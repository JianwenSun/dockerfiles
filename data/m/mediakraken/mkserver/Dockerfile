# Download base image  
FROM alpine:3.4  
  
MAINTAINER Quinn D Granfor, spootdev@gmail.com  
  
LABEL www.mediakraken.org.version="dev-0.2.0"  
LABEL Description="This image holds the main server app"  
# create work dir  
RUN mkdir /mediakraken  
  
# copy PIP requirements  
ADD requirements.txt /mediakraken  
WORKDIR /mediakraken  
  
RUN apk add --update \  
cifs-utils \  
nfs-utils \  
postgresql-client \  
openssl \  
alpine-sdk \  
libffi-dev \  
openldap-dev \  
jpeg-dev \  
libxml2-dev \  
libxslt-dev \  
linux-headers \  
musl-dev \  
net-snmp \  
net-snmp-dev \  
openldap-dev \  
portaudio-dev \  
postgresql-dev \  
py-pip \  
python-dev \  
openrc \  
&& pip install -r requirements.txt \  
&& apk del \  
alpine-sdk \  
libxml2-dev \  
libxslt-dev \  
linux-headers \  
musl-dev \  
net-snmp-dev \  
postgresql-dev \  
py-pip \  
python-dev \  
&& apk add \  
py-setuptools \  
&& rm -rf /var/cache/apk/* \  
&& rc-update add netmount  
  
ADD wait-for-it-ash.sh /mediakraken  
# Copy the source files for the app  
ADD src /mediakraken  
ADD ip2country /mediakraken/ip2country  
RUN cd ip2country \  
&& python setup.py install \  
&& cd .. \  
&& rm -R ./ip2country \  
&& rm requirements.txt  
  
EXPOSE 5000  
  
CMD ["/bin/ash"]  

