FROM nextcloud:apache  
  
RUN apt-get update && apt-get install -y \  
supervisor \  
cron \  
&& rm -rf /var/lib/apt/lists/*  
  
RUN mkdir /var/log/supervisord /var/run/supervisord && \  
echo "*/15 * * * * root su - www-data -s /bin/bash -c \"php -f
/var/www/html/cron.php\"" >> /etc/crontab && \  
echo "*/15 * * * * root su - www-data -s /bin/bash -c \"php -f
/var/www/html/occ files:scan --all\"\n" >> /etc/crontab  
  
COPY supervisord.conf /etc/supervisor/supervisord.conf  
  
CMD ["/usr/bin/supervisord"]

