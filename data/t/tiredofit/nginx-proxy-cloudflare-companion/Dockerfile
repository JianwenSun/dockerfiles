FROM tiredofit/alpine:3.6  
MAINTAINER Dave Conroy <dave at tiredofit dot ca>  
  
### Set Environment Variables  
ENV ENABLE_CRON=false \  
ENABLE_SMTP=false  
### Dependencies  
RUN apk update && \  
apk add \  
python2 \  
py2-pip \  
&& \  
  
pip install \  
cloudflare \  
docker \  
&& \  
### Cleanup  
rm -rf /root/.cache && \  
rm -rf /var/cache/apk/*  
  
### Add Files  
ADD install /  

