FROM debian:jessie  
  
LABEL maintainer "opsxcq@strm.sh"  
  
RUN apt-get update && \  
apt-get upgrade -y && \  
DEBIAN_FRONTEND=noninteractive apt-get install -y \  
debconf-utils && \  
echo mysql-server-5.5 mysql-server/root_password password vulnerables |
debconf-set-selections && \  
echo mysql-server-5.5 mysql-server/root_password_again password vulnerables |
debconf-set-selections && \  
DEBIAN_FRONTEND=noninteractive apt-get install -y \  
apache2 \  
mysql-server \  
php5 \  
php5-mysql \  
php-pear \  
php5-gd \  
curl \  
vim \  
git \  
&& \  
apt-get clean && \  
rm -rf /var/lib/apt/lists/*  
  
RUN git clone \--depth 1 https://github.com/ethicalhack3r/DVWA.git && \  
cp -r DVWA/* /var/www/html && \  
rm -rf DVWA  
#COPY DVWA /var/www/html  
COPY php.ini /etc/php5/apache2/php.ini  
  
RUN chown www-data:www-data -R /var/www/html && \  
rm /var/www/html/index.html  
  
EXPOSE 80  
COPY main.sh /  
ENTRYPOINT ["/main.sh"]  

