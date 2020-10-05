FROM amopromo/nginx:latest 
MAINTAINER anakinpendragon - anakinpendragon@gmail.com
COPY ./index.html /usr/share/nginx/html/
COPY ./default.conf /etc/nginx/conf.d
EXPOSE 8080
WORKDIR /usr/share/nginx/html/
EXPOSE 8080 
CMD ["nginx", "-g", "daemon off;"]
