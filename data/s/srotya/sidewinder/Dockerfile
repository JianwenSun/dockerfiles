FROM java:8-jre  
MAINTAINER Ambud Sharma  
  
EXPOSE 9928  
EXPOSE 8080  
RUN apt-get -y update  
RUN apt-get -y --force-yes install gettext telnet wget netcat  
  
RUN mkdir -p /usr/local/sidewinder/  
RUN mkdir -p /opt/sidewinder/  
  
RUN curl -o /usr/local/sidewinder/sidewinder.jar
"https://oss.sonatype.org/service/local/artifact/maven/content?r=releases&g=com.srotya.sidewinder&a=sidewinder-
core&v=LATEST"  
  
ADD ./config.yaml /opt/sidewinder/  
ADD ./template.properties /opt/sidewinder/  
ADD ./run.sh /opt/sidewinder/  
  
RUN chmod +x /opt/sidewinder/*.sh  
  
CMD /opt/sidewinder/run.sh

