FROM alpine:latest  
  
# Labels  
LABEL maintainer="Paulino Padial <github.com/ppadial>"  
  
# Environment variables (with default values)  
ENV LOG_LEVEL=8  
ENV CRON_SCHEDULE="*/15 * * *"  
ENV RSYNC_OPTS="avzP"  
# Install rsync  
RUN apk update && apk add rsync  
  
# Configure entrypoint  
ADD docker-entrypoint.sh /docker-entrypoint.sh  
RUN chmod +x /docker-entrypoint.sh  
  
# Volumes declaration  
VOLUME [ "/source", "/target" ]  
  
# Start the container process  
ENTRYPOINT ["/docker-entrypoint.sh"]

