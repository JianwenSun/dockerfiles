#  
# Dockerfile for langrisha/npm-lazy  
#  
# Based on the much regarded Google Node.js image.  
FROM google/nodejs-runtime  
  
# Volumize the NPM package cache.  
VOLUME ["/root/.npm_lazy"]  
  
# Server is listening on 0.0.0.0:8080, by default.  
EXPOSE 8080  
# Default server arguments.  
CMD ["--show-config", "--external-url=http://strategenics__npm_lazy:8080"]  
  
# Start the server on entry.  
ENTRYPOINT ["/nodejs/bin/node", "index.js"]  

