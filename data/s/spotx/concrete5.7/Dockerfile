FROM chriswayg/apache-php  
MAINTAINER Joel DuBien joel@spotx.tv  
  
# This image provides Concrete5.7 at root of site  
# Install pre-requisites for Concrete5 & nano for editing conf files  
RUN apt-get update && \  
DEBIAN_FRONTEND=noninteractive apt-get -y install \  
php5-curl \  
php5-gd \  
php5-mysql \  
unzip \  
wget \  
patch \  
nano && \  
apt-get clean && rm -r /var/lib/apt/lists/*  
  
# Find latest download details at https://www.concrete5.org/get-started  
# - for newer version: change Concrete5 version# & download url & md5  
ENV CONCRETE5_VERSION 5.7.5.2  
ENV C5_URL https://www.concrete5.org/download_file/-/view/82243/  
ENV C5_MD5 61e48a8d4bf281a25420c3d2186a1a3d  
# nano and other commands will not work without this  
ENV TERM xterm  
  
# Copy apache2 conf dir & Download Concrete5  
# Perl script to enable ability to activate 'Pretty URLs' and redirection in
.htaccess by 'AllowOverride'  
# - it matches a multi-line string and replaces 'None' with 'FileInfo'  
RUN perl -i.bak -0pe 's/<Directory \/var\/www\/>\n\tOptions Indexes
FollowSymLinks\n\tAllowOverride None/<Directory \/var\/www\/>\n\tOptions
Indexes FollowSymLinks\n\tAllowOverride FileInfo/' /etc/apache2/apache2.conf
&& \  
cp -r /etc/apache2 /usr/local/etc/apache2 && \  
cd /usr/local/src && \  
wget --no-verbose $C5_URL -O concrete5.zip && \  
echo "$C5_MD5 concrete5.zip" | md5sum -c - && \  
unzip -qq concrete5.zip && \  
rm -v concrete5.zip && \  
rm -v /var/www/html/index.html  
  
RUN chmod -R g+w /var/www/html && chgrp -R root /var/www/html && \  
chmod -R g+w /etc/apache2 && chgrp -R root /etc/apache2 && \  
chmod -R g+w /var/log/apache2 && chgrp -R root /var/log/apache2 && \  
chmod -R g+w /var/run/apache2 && chgrp -R root /var/run/apache2 && \  
chmod -R g+w /var/lock/apache2 && chgrp -R root /var/lock/apache2  
  
# Persist website user data, logs & apache config  
VOLUME [ "/var/www/html", "/var/log/apache2", "/etc/apache2" ]  
  
EXPOSE 8080 8443  
WORKDIR /var/www/html  
  
COPY docker-entrypoint /docker-entrypoint  
  
ENTRYPOINT ["/docker-entrypoint"]  
CMD ["apache2-foreground"]  

