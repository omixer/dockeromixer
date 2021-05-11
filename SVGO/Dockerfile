FROM node:16-alpine3.11

# define a work directory
WORKDIR /app

# install a global version of SVGO for the binary, then install it locally as a library 
RUN npm install -g svgo@2.3.0 \
 && npm install svgo@2.3.0

