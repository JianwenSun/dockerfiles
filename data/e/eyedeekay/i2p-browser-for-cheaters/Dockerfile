FROM debian:sid  
ARG BROWSER_VERSION="7.5.4"  
ARG PORT="4444"  
ENV DEBIAN_FRONTEND=noninteractive HOME=/home/anon  
  
RUN apt-get update && \  
apt-get -y dist-upgrade && \  
sed -i.bak 's/sid main/sid main contrib/g' /etc/apt/sources.list && \  
apt-get update && apt-get install -y \  
iceweasel \  
gnupg \  
zenity \  
ca-certificates \  
xz-utils \  
curl \  
sudo \  
\--no-install-recommends && \  
localedef -v -c -i en_US -f UTF-8 en_US.UTF-8 || :  
  
RUN groupadd -g 1000 anon  
RUN useradd -m -g 1000 -u 1000 -d /home/anon anon  
RUN mkdir /home/anon/.local  
  
USER anon  
  
WORKDIR /home/anon  
  
RUN curl -sSL -o /home/anon/tor.tar.xz \  
https://www.torproject.org/dist/torbrowser/${BROWSER_VERSION}/tor-browser-
linux64-${BROWSER_VERSION}_en-US.tar.xz  
  
RUN curl -sSL -o /home/anon/tor.tar.xz.asc \  
https://www.torproject.org/dist/torbrowser/${BROWSER_VERSION}/tor-browser-
linux64-${BROWSER_VERSION}_en-US.tar.xz.asc  
  
RUN gpg --keyserver ha.pool.sks-keyservers.net \  
\--recv-keys "EF6E 286D DA85 EA2A 4BA7 DE68 4E2C 6E87 9329 8290"  
  
RUN gpg --verify /home/anon/tor.tar.xz.asc  
  
RUN tar xf /home/anon/tor.tar.xz  
  
RUN rm -f /home/anon/tor.tar.xz*  
  
COPY setup-i2p-browser.sh .  
COPY etc/ etc/  
  
RUN ./setup-i2p-browser.sh "/home/anon/tor-browser_en-US/" "$PORT"  
  
RUN mkdir -p /home/anon/working  
  
RUN cp -r /home/anon/tor-browser_en-US/ /home/anon/working/i2p-browser_en-US/  
  
RUN cd /home/anon/working/ && \  
tar czf /home/anon/i2p-browser.tar.gz .  
  
RUN mv /home/anon/working/i2p-browser_en-US/ /home/anon/i2p-browser_en-US/  
  
USER root  
  
CMD chown -R anon:anon /home/anon/.local/ && \  
chmod -R o+rw /home/anon/.local/ && \  
sudo -u anon /home/anon/i2p-browser_en-US/Browser/start-i2p-browser  

