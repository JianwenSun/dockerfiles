FROM node:6.10-alpine  
  
COPY index.js package.json /app/  
  
WORKDIR /app/  
  
RUN npm install  
  
ENTRYPOINT ["node", "/app/index.js"]  

