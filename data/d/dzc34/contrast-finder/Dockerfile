FROM dzc34/contrast-finder:pre-requisites_from-Ubuntu  
  
# #### usage ######################################################  
#  
# --- Building this docker image  
# docker build -t asqatasun/contrast-finder .  
# docker build -t asqatasun/contrast-finder --build-arg
CONTRAST_FINDER_RELEASE=0.3.5 .  
# docker build -t asqatasun/contrast-finder --build-arg
SRC_URL_PREFIX=https://github.com/Asqatasun/Contrast-
Finder/releases/download/v0.3.5/ .  
# docker build -t asqatasun/contrast-finder --build-arg
SRC_URL=https://github.com/Asqatasun/Contrast-
Finder/releases/download/v0.3.5/contrast-finder-webapp-0.3.5.war .  
#  
# --- Launch a container  
# docker run -p 127.0.0.1:8087:8080 \--name contrast.finder -d
asqatasun/contrast-finder  
#  
# --- Playing with this docker image  
# docker exec -ti contrast.finder /bin/bash  
# docker logs -f contrast.finder  
#  
# #### source code ###############################################  
# https://github.com/Asqatasun/Contrast-
Finder/releases/download/v${CONTRAST_FINDER_RELEASE}/contrast-finder-
webapp-${CONTRAST_FINDER_RELEASE}.war  
# could be overridden with \--build-arg CONTRAST_FINDER_RELEASE=<release>  
# could be overridden with \--build-arg SRC_URL_PREFIX=<url_prefix>  
# could be overridden with \--build-arg SRC_URL=<url>  
#  
# #### FROM ######################################################  
# asqatasun/contrast-finder:pre-requisites_from-Ubuntu
https://github.com/Asqatasun/Contrast-Finder/blob/master/docker/pre-
requisites/pre-requisites_from-Ubuntu/Dockerfile  
# |-- ubuntu:14.04 https://github.com/tianon/docker-brew-ubuntu-
core/blob/dist/trusty/Dockerfile  
###################################################################  
  
# build variables  
# ARG CONTRAST_FINDER_RELEASE="0.3.6-dev"  
ARG CONTRAST_FINDER_RELEASE="0.3.5"  
ARG SRC_URL_PREFIX="https://github.com/Asqatasun/Contrast-
Finder/releases/download/v${CONTRAST_FINDER_RELEASE}"  
ARG SRC_URL="${SRC_URL_PREFIX}/contrast-finder-
webapp-${CONTRAST_FINDER_RELEASE}.war"  
  
# Install contrast-finder  
RUN cd /root/ && \  
wget ${SRC_URL} && \  
mv -v /root/contrast-*.war /root/contrast-finder.war && \  
mv -v /root/contrast-finder.war /var/lib/tomcat7/webapps  
  
  
# environment variables  
ENV CONTRAST_FINDER=${CONTRAST_FINDER_RELEASE}  
ENV SRC=${SRC_URL}  
  
CMD service tomcat7 start ; \  
tail -f /var/log/tomcat7/catalina.out \  
/var/log/contrast-finder/contrast-finder.log  
  
  
  

