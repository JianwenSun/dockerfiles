FROM openjdk:8u131-jre-alpine  
  
RUN apk add --no-cache bash curl tar && \  
addgroup -g 750 -S logstash && \  
adduser -u 750 -D -S -G logstash logstash  
  
ENV HOME_DIR /usr/share/logstash  
ENV VERSION 5.6.2  
WORKDIR ${HOME_DIR}  
  
RUN apk add --no-cache bash curl tar && \  
curl -fsSL
https://artifacts.elastic.co/downloads/logstash/logstash-${VERSION}.tar.gz |
tar zx --strip-components=1  
  
#RUN /usr/share/logstash/bin/logstash-plugin install logstash-codec-cloudtrail  
RUN /usr/share/logstash/bin/logstash-plugin install logstash-filter-csv
logstash-input-s3  
  
#COPY ./assets/logstash.yml /usr/share/logstash/config/logstash.yml  
RUN chown -R logstash:logstash ${HOME_DIR} ${HOME_DIR}/*  
  
USER logstash  
  
EXPOSE 5000  
ENTRYPOINT ["/usr/share/logstash/bin/logstash"]  
  
CMD []  

