FROM ubuntu:16.04  
ENV PUPPET_SERVER_VERSION="5.1.4" \  
DUMB_INIT_VERSION="1.2.1" \  
UBUNTU_CODENAME="xenial" \  
PUPPETSERVER_JAVA_ARGS="-Xms256m -Xmx256m" \  
PUPPETSERVER_JRUBYINSTANCES=2 \  
PUPPETDB_TERMINI_VERSION="5.1.3" \  
LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8 LANGUAGE=en_US.UTF-8 \  
PATH=/opt/puppetlabs/server/bin:/opt/puppetlabs/puppet/bin:/opt/puppetlabs/bin:$PATH  
  
LABEL org.label-schema.vendor="VSHN AG" \  
org.label-schema.url="https://github.com/vshn/puppet-in-docker" \  
org.label-schema.name="Puppet Server" \  
org.label-schema.license="BSD-3-Clause" \  
org.label-schema.version=$PUPPET_SERVER_VERSION \  
org.label-schema.vcs-url="https://github.com/vshn/puppet-in-docker" \  
org.label-schema.schema-version="1.0" \  
com.puppet.dockerfile="/Dockerfile"  
  
EXPOSE 8140  
ENTRYPOINT ["dumb-init", "/docker-entrypoint.sh"]  
CMD ["puppetserver"]  
  
COPY Dockerfile /  
  
# TODO checksum check  
RUN apt-get update && \  
apt-get install -y wget git netcat vim locales && \  
locale-gen en_US.UTF-8 && \  
wget https://apt.puppetlabs.com/puppet5-release-"$UBUNTU_CODENAME".deb && \  
wget https://github.com/Yelp/dumb-
init/releases/download/v"$DUMB_INIT_VERSION"/dumb-
init_"$DUMB_INIT_VERSION"_amd64.deb && \  
dpkg -i puppet5-release-"$UBUNTU_CODENAME".deb && \  
dpkg -i dumb-init_"$DUMB_INIT_VERSION"_amd64.deb && \  
rm puppet5-release-"$UBUNTU_CODENAME".deb dumb-
init_"$DUMB_INIT_VERSION"_amd64.deb && \  
apt-get update && \  
apt-get install --no-install-recommends -y
puppetserver="$PUPPET_SERVER_VERSION"-1"$UBUNTU_CODENAME" puppetdb-
termini="$PUPPETDB_TERMINI_VERSION"-1"$UBUNTU_CODENAME" && \  
apt-get clean && \  
rm -rf /var/lib/apt/lists/* && \  
find \  
/etc/puppetlabs \  
/opt/puppetlabs/server/data/puppetserver \  
-exec chgrp -R root {} + \  
-exec chown -R puppet {} + \  
-exec chmod -R g=rwX,g-s {} +  
  
# Add configuration files into the image  
COPY config/puppetserver /etc/default/puppetserver  
COPY config/logback.xml /etc/puppetlabs/puppetserver/  
COPY config/request-logging.xml /etc/puppetlabs/puppetserver/  
COPY config/puppetdb.conf /etc/puppetlabs/puppet/  
COPY config/hiera.yaml /etc/puppetlabs/puppet/hiera.yaml  
  
# Add scripts to get started easily  
COPY config/simple-enc /etc/puppetlabs/puppet/simple-enc  
COPY config/simple-autosign /etc/puppetlabs/puppet/simple-autosign  
COPY request-cert.rb /usr/local/bin  
  
# Copy entrypoint into container  
COPY docker-entrypoint.sh /  
COPY /docker-entrypoint.d/* /docker-entrypoint.d/  
  
# Because of how Puppetserver is started (bash -> su)  
# this currently doesn't work  
#USER puppet  

