# N00b (a.k.a. me) documentation:  
#  
# Build with:  
# docker build -t="thomasjmoerman/sourire:latest" .  
#  
# Run with:  
# docker run -d -p 9999:8080 thomasjmoerman/sourire:latest  
#  
# Test with:  
#
http://192.168.59.103:9999/molecule/OCCc1c%28C%29%5Bn%2B%5D%28%3Dcs1%29Cc2cnc%28C%29nc%28N%292?render-
comment=Vitamin%20B1  
#  
FROM ubuntu:14.04  
MAINTAINER Thomas Moerman (https://twitter.com/thomasjmoerman)  
  
# Install all needed packages and clean up  
RUN apt-get -y update  
RUN sudo apt-get install -y openjdk-7-jdk wget git \  
&& apt-get clean \  
&& rm -rf /var/lib/apt/lists/*  
  
# Install Leiningen 2  
RUN wget -O /bin/lein
https://raw.github.com/technomancy/leiningen/stable/bin/lein  
RUN chmod 755 /bin/lein  
  
# Specify environment variables  
ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64  
ENV LEIN_ROOT yes  
  
WORKDIR /data  
  
# Clone the Sourire git repo  
RUN git clone https://github.com/tmoerman/sourire.git  
  
# Build the standalone jar artifact, move the artifact to bin and remove the
temporary files  
RUN cd /data/sourire \  
&& lein create-standalone \  
&& mv /data/sourire/target/sourire-*-standalone.jar /data/sourire.jar \  
&& cd /data \  
&& rm -rf sourire  
  
# State this in the docker file as info for the operator (`docker inspect
<id>`)  
EXPOSE 8080  
# Launch the Sourire web application on port 8080  
ENTRYPOINT java -jar sourire.jar :port 8080  
CMD [""]  
  
# EOF  

