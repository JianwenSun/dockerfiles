FROM ubuntu:16.04  
MAINTAINER Venatus Digital  
  
RUN apt update \  
&& apt upgrade -y \  
&& apt install -y lib32gcc1 lib32stdc++6 unzip curl libgdiplus iproute2 \  
&& curl -sL https://deb.nodesource.com/setup_6.x | bash - \  
&& apt install -y nodejs \  
&& mkdir /node_modules \  
&& npm install --prefix / ws \  
&& useradd -d /home/container -m container  
  
USER container  
ENV USER=container HOME=/home/container  
  
WORKDIR /home/container  
  
COPY ./entrypoint.sh /entrypoint.sh  
COPY ./wrapper.js /wrapper.js  
  
CMD ["/bin/bash", "/entrypoint.sh"]  

