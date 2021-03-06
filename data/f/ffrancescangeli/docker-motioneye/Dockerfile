FROM phusion/baseimage:0.10.1  
MAINTAINER franco <francescangeli.f@gmail.com>  
  
ENV MOTIONEYE_VERSION=0.39  
RUN apt update  
  
# Set time zone at your choice  
RUN apt install -y tzdata  
ENV TZ=Europe/Rome  
RUN echo "Europe/Rome" > /etc/timezone  
RUN dpkg-reconfigure -f noninteractive tzdata  
  
RUN apt-get install -q -y --no-install-recommends \  
bsd-mailx \  
git \  
mutt \  
ssmtp \  
x264 \  
autoconf \  
automake \  
pkgconf \  
libtool \  
libjpeg8-dev \  
libjpeg-dev \  
build-essential \  
libzip-dev \  
libavformat-dev \  
libavcodec-dev \  
libswscale-dev \  
libavdevice-dev \  
python-dev && \  
apt-get -y clean && \  
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*  
  
RUN add-apt-repository -y ppa:mc3man/xerus-media  
  
RUN apt-get update && \  
apt-get install -q -y --no-install-recommends ffmpeg v4l-utils python-pip
libssl-dev libcurl4-openssl-dev libjpeg-dev && \  
apt-get -y clean && \  
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*  
  
RUN mkdir -p /var/lib/motioneye  
  
# Copy and scripts  
COPY script/* /usr/local/bin/  
RUN chmod +x /usr/local/bin/*  
  
RUN cd /tmp && git clone \--branch 4.1 https://github.com/Motion-
Project/motion.git motion-project  
RUN cd /tmp/motion-project && \  
autoreconf -fiv && \  
./configure --prefix=/usr --without-pgsql --without-sqlite3 --without-mysql
--with-ffmpeg=/usr && \  
make && \  
touch README \  
make install && \  
cp motion /usr/local/bin/motion && cd / && \  
rm -rf /tmp/motion-project  
  
RUN pip install --upgrade pip  
RUN pip install -U setuptools  
RUN pip install -U pip  
  
RUN pip install motioneye==$MOTIONEYE_VERSION  
  
EXPOSE 8081 8765  
VOLUME ["/config", "/home/nobody/motioneye"]  
  
WORKDIR /home/nobody/motioneye  
  
RUN usermod -g users nobody  
  
#CMD ["/usr/local/bin/docker-motioneye"]  
ADD init/*.sh /etc/my_init.d/  
ADD services /etc/service  
RUN chmod -v +x /etc/service/*/run /etc/service/*/finish /etc/my_init.d/*.sh  

