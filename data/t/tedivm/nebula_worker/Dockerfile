FROM python:3.6  
ADD requirements.txt /app/requirements.txt  
RUN sed '/^uWSGI/ d' < /app/requirements.txt > /app/requirements_filtered.txt  
WORKDIR /app/  
RUN pip install -r requirements_filtered.txt  
  
ENV SETTINGS /app/settings.yaml  
  
ADD ./nebula/ /app/nebula  
  
RUN useradd -ms /bin/bash nebula  
USER nebula  
  
RUN mkdir -p /home/nebula/.aws  
RUN touch /home/nebula/.aws/credentials  
RUN touch /home/nebula/.aws/config  
RUN chown -R nebula:nebula /home/nebula/.aws  
  
ADD ./docker/worker/start_worker.sh /home/nebula/start_worker.sh  
  
ENTRYPOINT /home/nebula/start_worker.sh  

