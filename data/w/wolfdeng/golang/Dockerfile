FROM wolfdeng/alpine:3.7  
  
MAINTAINER Tony Deng (wolf.deng@gmail.com)  
  
ENV GOLANG_VERSION 1.9.3  
  
# no-pic.patch: https://golang.org/issue/14851 (Go 1.8 & 1.7)  
  
COPY patch/*.patch /go-alpine-patches/  
  
RUN set -eux; \  
apk add --no-cache --virtual .build-deps \  
bash \  
gcc \  
musl-dev \  
openssl \  
go \  
; \  
export \  
# set GOROOT_BOOTSTRAP such that we can actually build Go  
GOROOT_BOOTSTRAP="$(go env GOROOT)" \  
# ... and set "cross-building" related vars to the installed system's values
so that we create a build targeting the proper arch  
# (for example, if our build host is GOARCH=amd64, but our build env/image is
GOARCH=386, our build needs GOARCH=386)  
GOOS="$(go env GOOS)" \  
GOARCH="$(go env GOARCH)" \  
GOHOSTOS="$(go env GOHOSTOS)" \  
GOHOSTARCH="$(go env GOHOSTARCH)" \  
; \  
# also explicitly set GO386 and GOARM if appropriate  
# https://github.com/docker-library/golang/issues/184  
apkArch="$(apk --print-arch)"; \  
case "$apkArch" in \  
armhf) export GOARM='6' ;; \  
x86) export GO386='387' ;; \  
esac; \  
\  
wget -O go.tgz "https://golang.org/dl/go$GOLANG_VERSION.src.tar.gz"; \  
echo '4e3d0ad6e91e02efa77d54e86c8b9e34fbe1cbc2935b6d38784dca93331c47ae
*go.tgz' | sha256sum -c -; \  
tar -C /usr/local -xzf go.tgz; \  
rm go.tgz; \  
\  
cd /usr/local/go/src; \  
for p in /go-alpine-patches/*.patch; do \  
[ -f "$p" ] || continue; \  
patch -p2 -i "$p"; \  
done; \  
./make.bash; \  
\  
rm -rf /go-alpine-patches; \  
apk del .build-deps; \  
\  
export PATH="/usr/local/go/bin:$PATH"; \  
go version  
  
ENV GOPATH /go  
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH  
  
RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"  
WORKDIR $GOPATH  
  
COPY go-wrapper /usr/local/bin/  

