FROM ubuntu:16.04  
MAINTAINER ChasonTang <chasontang@gmail.com>  
  
ENV SWIFT_BRANCH swift-3.0.1-release  
ENV SWIFT_VERSION swift-3.0.1-RELEASE  
ENV SWIFT_PLATFORM ubuntu16.04  
# Install related packages and set LLVM 3.6 as the compiler  
RUN apt-get update && \  
apt-get install -y wget libedit2 libicu55 libxml2 libcurl3 clang git && \  
apt-get clean && \  
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*  
  
# Install Swift keys  
RUN wget -q -O - https://swift.org/keys/all-keys.asc | gpg --import - && \  
gpg --keyserver hkp://pool.sks-keyservers.net --refresh-keys Swift  
  
# Install Swift Ubuntu 16.04  
RUN SWIFT_ARCHIVE_NAME=$SWIFT_VERSION-$SWIFT_PLATFORM && \  
SWIFT_URL=https://swift.org/builds/$SWIFT_BRANCH/$(echo "$SWIFT_PLATFORM" | tr
-d .)/$SWIFT_VERSION/$SWIFT_ARCHIVE_NAME.tar.gz && \  
wget $SWIFT_URL && \  
wget $SWIFT_URL.sig && \  
gpg --verify $SWIFT_ARCHIVE_NAME.tar.gz.sig && \  
tar -xvzf $SWIFT_ARCHIVE_NAME.tar.gz --directory /usr/local \--strip-
components=2 && \  
rm -rf $SWIFT_ARCHIVE_NAME* /tmp/* /var/tmp/*  
  
# Print Installed Swift Version  
RUN swift --version

