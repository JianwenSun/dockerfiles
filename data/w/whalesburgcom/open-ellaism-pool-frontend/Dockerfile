FROM node  
  
ARG environment  
  
RUN npm install -g ember-cli@2.9.1 && \  
npm install -g bower  
  
WORKDIR /open-ellaism-pool-frontend  
ADD . /open-ellaism-pool-frontend  
  
RUN npm install  
RUN bower install --allow-root  
RUN ./build.sh ${environment}  
  
RUN mv dist /dist  
  
RUN chmod +x docker-entrypoint.sh  
  
ENTRYPOINT ["./docker-entrypoint.sh"]  

