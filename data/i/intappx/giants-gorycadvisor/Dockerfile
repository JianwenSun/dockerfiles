FROM debian:jessie  
  
ENV DEBIAN_FRONTEND noninteractive  
ENV DEBCONF_NONINTERACTIVE_SEEN true  
ENV GOPATH /opt  
ENV CADVISOR_ADDRESS cadvisor:8080  
ENV INTERVAL 20s  
  
ADD startup.sh /opt/startup.sh  
  
WORKDIR /opt/  
  
RUN apt-get update && \  
apt-get install netcat-traditional && \  
apt-get install -y supervisor golang git mercurial vim && \  
git clone https://github.com/docktor/goryCadvisor.git && \  
go get github.com/bigdatadev/goryman && \  
go get github.com/golang/glog && \  
go get github.com/google/cadvisor/client && \  
go get github.com/google/cadvisor/info/v1 && \  
cd goryCadvisor && go build main.go && cd /opt && mv goryCadvisor/main
mainGoryCadvisor && \  
rm -rf /opt/goryCadvisor && \  
apt-get autoremove -y golang git mercurial && \  
apt-get clean && \  
rm -rf /var/lib/apt/lists/* && \  
rm -rf /opt/src && \  
rm -rf /opt/pkg  
  
ADD supervisord.conf.d/* /etc/supervisor/conf.d/  
  
  
CMD ["/opt/startup.sh"]  

