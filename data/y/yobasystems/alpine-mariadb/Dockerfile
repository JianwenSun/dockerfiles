FROM yobasystems/alpine:amd64  
LABEL maintainer "Dominic Taylor <dominic@yobasystems.co.uk>"
architecture="AMD64/x86_64" version="10.1.28" date="7-feb-2018"  
  
RUN apk --update add mariadb mariadb-client pwgen && \  
rm -f /var/cache/apk/*  
  
ADD files/run.sh /scripts/run.sh  
RUN mkdir /scripts/pre-exec.d && \  
mkdir /scripts/pre-init.d && \  
chmod -R 755 /scripts  
  
EXPOSE 3306  
VOLUME ["/var/lib/mysql"]  
  
ENTRYPOINT ["/scripts/run.sh"]  

