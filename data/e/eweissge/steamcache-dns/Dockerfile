FROM alpine:latest  
MAINTAINER SteamCache.Net Team <team@steamcache.net>  
  
ENV STEAMCACHE_DNS_VERSION 1  
RUN apk update \  
&& apk add bind  
  
COPY overlay/ /  
  
RUN mkdir -p /var/cache/bind /var/log/named \  
&& chmod 755 /scripts/* \  
&& chown named:named /var/cache/bind /var/log/named  
  
EXPOSE 53/udp  
  
WORKDIR /scripts  
  
ENV LANCACHE_IP 192.168.1.3  
ENV STEAMCACHE_IP 192.168.1.3  
ENV UPLAYCACHE_IP 192.168.1.3  
ENV WINDOWSCACHE_IP 192.168.1.3  
ENTRYPOINT ["/scripts/bootstrap.sh"]  

