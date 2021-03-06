FROM debian:jessie  
  
# Maintainer  
MAINTAINER Nicolas Dumont  
  
ENV DEBIAN_FRONTEND=noninteractive  
  
# Git branch to build from  
ENV BV_SYN=0.21.0  
ENV BV_TUR=master  
# https://github.com/python-pillow/Pillow/issues/1763  
ENV LIBRARY_PATH=/lib:/usr/lib  
  
# use --build-arg REBUILD=$(date) to invalidate the cache and upgrade all  
# packages  
ARG REBUILD=1  
  
RUN export DEBIAN_FRONTEND=noninteractive \  
&& apt-get update -y \  
&& apt-get upgrade -y \  
&& apt-get install -y \  
bash \  
coreutils \  
coturn \  
curl \  
file \  
gcc \  
git \  
libevent-2.0-5 \  
libevent-dev \  
libffi-dev \  
libffi6 \  
libgnutls28-dev \  
libjpeg62-turbo \  
libjpeg62-turbo-dev \  
libldap-2.4-2 \  
libldap2-dev \  
libsasl2-dev \  
libsqlite3-dev \  
libssl-dev \  
libssl1.0.0 \  
libtool \  
libxml2 \  
libxml2-dev \  
libxslt1-dev \  
libxslt1.1 \  
linux-headers-amd64 \  
make \  
pwgen \  
python \  
python-dev \  
python-pip \  
python-psycopg2 \  
python-virtualenv \  
sqlite \  
unzip \  
zlib1g \  
zlib1g-dev \  
; \  
pip install --upgrade pip ;\  
pip install --upgrade python-ldap ;\  
pip install --upgrade lxml \  
; \  
curl -L https://github.com/matrix-org/synapse/archive/v$BV_SYN.zip -o s.zip \  
&& unzip s.zip \  
&& cd /synapse-$BV_SYN \  
&& pip install --upgrade --process-dependency-links . \  
&& GIT_SYN=$(git ls-remote https://github.com/matrix-org/synapse $BV_SYN | cut
-f 1) \  
&& echo "synapse: $BV_SYN ($GIT_SYN)" >> /synapse.version \  
&& cd / \  
&& rm -rf synapse-$BV_SYN \  
&& rm s.zip \  
; \  
apt-get remove \  
file \  
gcc \  
git \  
libevent-dev \  
libffi-dev \  
libjpeg62-turbo-dev \  
libldap2-dev \  
libsqlite3-dev \  
libssl-dev \  
libtool \  
libxml2-dev \  
libxslt1-dev \  
linux-headers-amd64 \  
make \  
python-dev \  
zlib1g-dev \  
; \  
rm -rf /var/lib/apt/* /var/cache/apt/*  
# install homerserver template  
COPY adds/start.sh /start.sh  
  
RUN chmod a+x /start.sh  
  
# startup configuration  
ENTRYPOINT ["/start.sh"]  
CMD ["start"]  
EXPOSE 8448  
VOLUME ["/data"]  
  
  

