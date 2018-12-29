FROM ubuntu:16.04 as env

#Installing  dependencies
RUN apt update && apt install -y curl && curl -sL https://deb.nodesource.com/setup_8.x 
RUN apt install -y nodejs && apt install -y npm
RUN npm install -g @angular/cli
RUN npm install -g n
RUN n 8

# Installing Nginx.
# RUN \
#   add-apt-repository -y ppa:nginx/stable && \
#   apt update && \
#   apt install -y nginx && \
#   rm -rf /var/lib/apt/lists/* && \
#   echo "\ndaemon off;" >> /etc/nginx/nginx.conf && \
#   chown -R www-data:www-data /var/lib/nginx

#Enviroment Variables
#Most of them would be on code and on the container through jenkins credentials plugin
ENV API_URL http://localhost:5000 
ENV API_KEY THISISAENVARIABLE

WORKDIR /drproject

EXPOSE 80 
EXPOSE 4200

#Keep this container alive 
#TODO: start a web server on foreground
ENTRYPOINT ["tail", "-f", "/dev/null"]

FROM env as build

#Grab all the files on my local to my working directory on the container
COPY . .
RUN npm install


# create a tag for qa here
FROM build as prod

CMD ["ng", "serve"]

#use this for qa
# FROM env as prod

