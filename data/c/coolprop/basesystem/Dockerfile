# Do not edit this file manually, it was generated on 2017-03-10 at 21:52 from
basesystem/Dockerfile.in  
# Define a base image for all 64bit CoolProp docker images  
FROM coolprop/debian:latest  
# File Author / Maintainer  
MAINTAINER Jorrit Wronski <jowr@ipu.dk>  
# Make sure bash is the standard shell  
RUN rm /bin/sh && ln -sf /bin/bash /bin/sh  
# Install the development packages and compilers  
RUN apt-key update -qq && apt-get update -qq &&
DEBIAN_FRONTEND="noninteractive" apt-get install -y \  
build-essential gfortran gcc cmake git bash rsync curl wget nano python-dev
python-pip && \  
DEBIAN_FRONTEND="noninteractive" apt-get autoclean &&
DEBIAN_FRONTEND="noninteractive" apt-get clean &&
DEBIAN_FRONTEND="noninteractive" apt-get autoremove  
# Add some standard host keys  
RUN mkdir ${HOME}/.ssh && ssh-keyscan github.com >> ${HOME}/.ssh/known_hosts
&& ssh-keyscan bitbucket.org >> ${HOME}/.ssh/known_hosts && ssh-keyscan
coolprop.org >> ${HOME}/.ssh/known_hosts && ssh-keyscan
coolprop.dreamhosters.com >> ${HOME}/.ssh/known_hosts && cat
${HOME}/.ssh/known_hosts  
# Add the entrypoint  
ENTRYPOINT ["linux64", "/bin/sh"]  

