# shoal-server  
#  
# VERSION 0.0.1  
FROM centos:6  
MAINTAINER Ian Gable <igable@uvic.ca>  
  
RUN yum update -y \  
&& yum install epel-release -y \  
&& curl http://shoal.heprc.uvic.ca/repo/shoaldev.repo -o
/etc/yum.repos.d/shoal.repo \  
&& yum update -y \  
&& rpm --import http://hepnetcanada.ca/pubkeys/igable.asc \  
&& yum install shoal-server -y \  
&& yum clean all  

