# it's offical so i'm using it + alpine is so small  
FROM python:2.7-alpine  
  
COPY /autoscaler.py /autoscaler.py  
  
RUN pip install requests beautifulsoup4 boto3  
  
CMD python /autoscaler.py

