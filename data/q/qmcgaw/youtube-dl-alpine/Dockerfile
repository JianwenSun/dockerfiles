FROM alpine:3.7  
LABEL maintainer="quentin.mcgaw@gmail.com" \  
description="Download with youtube-dl using command line arguments or
configuration files. GeoIP built on top if you use a VPN" \  
download="30.4MB" \  
size="89MB" \  
ram="Depends" \  
cpu_usage="Depends" \  
github="https://github.com/qdm12/youtube-dl-docker"  
COPY vpncheck.sh entrypoint.sh /  
RUN apk add -q --progress --update --no-cache ca-certificates ffmpeg python2
&& \  
mkdir /downloads && \  
rm -rf /var/cache/apk/* && \  
chmod +x /vpncheck.sh /entrypoint.sh  
ENV CITY= \  
ORG=  
VOLUME /downloads  
HEALTHCHECK \--interval=20m --timeout=10s --retries=3 CMD /vpncheck.sh  
ENTRYPOINT /vpncheck.sh && /entrypoint.sh  
CMD [""]

