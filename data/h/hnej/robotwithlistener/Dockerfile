FROM ubuntu:16.04  
RUN apt-get update -y && apt-get install -y \  
firefox=45.0.2+build1-0ubuntu1 \  
python-pip \  
libglu1 \  
wget \  
&& rm -rf /var/lib/apt/lists/*  
  
RUN pip install \  
robotframework \  
robotframework-selenium2library  
  
RUN echo "export PYTHONPATH='${PYTHONPATH}:/vagrant'" >> /.bashrc  
  
ENV DISPLAY=xvfb:0  
WORKDIR /  
COPY pybot.sh /usr/local/bin/  
RUN chmod ug+x /usr/local/bin/pybot.sh  
ENTRYPOINT ["/usr/local/bin/pybot.sh"]  
CMD ["--help"]  

