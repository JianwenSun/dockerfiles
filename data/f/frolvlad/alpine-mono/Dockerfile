FROM frolvlad/alpine-glibc:alpine-3.7  
  
RUN apk add --no-cache --virtual=.build-dependencies wget ca-certificates tar
xz && \  
wget
"https://archive.archlinux.org/packages/m/mono/mono-5.0.0.100-2-x86_64.pkg.tar.xz"
-O "/tmp/mono.pkg.tar.xz" && \  
tar -xJf "/tmp/mono.pkg.tar.xz" && \  
cert-sync /etc/ssl/certs/ca-certificates.crt && \  
apk del .build-dependencies && \  
rm /tmp/*  

