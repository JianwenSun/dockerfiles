# Project Freedom  
# UE CIVIC API IMAGE  
# Copyright 2017  
FROM mhart/alpine-node  
LABEL author="borzou@theboeffect.com"  
RUN mkdir /src  
  
COPY . /src  
WORKDIR /src  
RUN mv /src/config_changeme.js /src/config.js  
RUN yarn  
  
EXPOSE 4020  
CMD ["node", "./bin/www"]

