FROM andyshinn/dnsmasq:latest  
MAINTAINER Chris Schmich <schmch@gmail.com>  
COPY dnsmasq.conf /etc/dnsmasq.conf  
COPY update-hosts.sh /etc/periodic/daily/update-hosts  
COPY start.sh /srv/purify/start.sh  
RUN apk add --no-cache curl \  
&& chmod +x /etc/periodic/daily/update-hosts \  
&& chmod +x /srv/purify/start.sh  
EXPOSE 53 53/udp  
ENTRYPOINT ["/srv/purify/start.sh"]  

