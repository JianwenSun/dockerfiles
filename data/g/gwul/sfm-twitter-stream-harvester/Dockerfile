FROM gwul/sfm-
base@sha256:07b3495d4496d603d464b3f829f92e61c6d27da8b773e1076e1b6ffcfd643eaf  
MAINTAINER Justin Littman <justinlittman@gwu.edu>  
  
# Install supervisor  
RUN apt-get update && apt-get install -y \  
supervisor=3.0r1-1+deb8u1  
VOLUME /etc/supervisor/conf.d  
  
ADD . /opt/sfm-twitter-harvester/  
WORKDIR /opt/sfm-twitter-harvester  
RUN pip install -r requirements/common.txt -r requirements/release.txt  
  
ADD docker/stream-harvester/invoke.sh /opt/sfm-setup/  
RUN chmod +x /opt/sfm-setup/invoke.sh  
  
ENTRYPOINT ["/opt/sfm-setup/invoke.sh"]  

