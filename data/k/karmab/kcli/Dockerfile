FROM centos:7  
MAINTAINER Karim Boumedhel <karimboumedhel@gmail.com>  
  
LABEL name="karmab/kcli" \  
maintainer="karimboumedhel@gmail.com" \  
vendor="Karmalabs" \  
version="10.6" \  
release="1" \  
summary="Libvirt/VirtualBox wrapper on steroids" \  
description="Libvirt/VirtualBox wrapper on steroids"  
  
EXPOSE 9000  
# Group the package installation  
RUN yum -y install epel-release && \  
yum -y install gcc git libvirt-devel python-devel genisoimage qemu-kvm nmap-
ncat python-pip openssh-clients  
  
# Group the pip installation  
RUN pip install -U --no-cache-dir ipaddress  
RUN pip install --no-cache-dir -e
git+https://github.com/karmab/kcli.git#egg=kcli[all]  
  
VOLUME ["/var/run/libvirt", "/root/.ssh", "/root"]  
  
ENTRYPOINT ["/usr/bin/kcli"]  
CMD ["-h"]  

