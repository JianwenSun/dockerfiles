FROM smartentry/alpine:3.4-0.3.2  
MAINTAINER Yifan Gao <docker@yfgao.com>  
  
COPY . $ASSETS_DIR  
  
RUN smartentry.sh build  
  
CMD ["/usr/sbin/named", "-u", "named", "-g"]  

