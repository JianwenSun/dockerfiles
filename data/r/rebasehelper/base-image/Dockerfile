ARG BASE_IMAGE=fedora:latest  
FROM ${BASE_IMAGE}  
  
RUN echo -e "deltarpm=0\ninstall_weak_deps=0\ntsflags=nodocs" >>
/etc/dnf/dnf.conf \  
# update GPG keys first in case some of them are missing  
&& dnf -y --nogpgcheck update fedora-gpg-keys || true \  
&& dnf -y update \  
&& dnf -y install \  
python2 \  
python2-devel \  
python3 \  
python3-devel \  
python2-rpm \  
python3-rpm \  
python2-tox \  
python3-tox \  
python2-pip \  
python3-pip \  
python2-setuptools \  
python3-setuptools \  
redhat-rpm-config \  
libxml2-devel \  
libxslt-devel \  
licensecheck \  
xz-devel \  
krb5-devel \  
git \  
rpm-build \  
mock \  
rpmlint \  
libabigail \  
pkgdiff \  
dnf \  
dnf-plugins-core \  
# needed by rpm-py-installer  
rpm-devel \  
# necessary for rpmbuild  
@buildsys-build \  
&& dnf clean all  

