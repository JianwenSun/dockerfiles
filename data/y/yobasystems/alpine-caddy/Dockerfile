FROM yobasystems/alpine:amd64  
LABEL maintainer "Dominic Taylor <dominic@yobasystems.co.uk>"
architecture="AMD64/x86_64" version="0.10.10" date="7-feb-2018"  
  
ARG plugins=http.git  
  
RUN apk add --update openssh-client git tar curl  
  
RUN curl --silent --show-error --fail --location --header "Accept:
application/tar+gzip, application/x-gzip, application/octet-stream" -o - \  
"https://caddyserver.com/download/linux/amd64?plugins=${plugins}" \  
| tar --no-same-owner -C /usr/bin/ -xz caddy && \  
chmod 0755 /usr/bin/caddy && \  
addgroup -S caddy && \  
adduser -D -S -H -s /sbin/nologin -G caddy caddy && \  
/usr/bin/caddy -version  
  
EXPOSE 80 443 2015  
VOLUME /srv  
WORKDIR /srv  
  
ADD files/Caddyfile /etc/Caddyfile  
ADD files/index.html /srv/index.html  
  
RUN chown -R caddy:caddy /srv  
  
USER caddy  
  
ENTRYPOINT ["/usr/bin/caddy"]  
CMD ["--conf", "/etc/Caddyfile"]  

