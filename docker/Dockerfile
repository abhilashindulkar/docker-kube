FROM nginx:1.23

COPY ../src/index.html /usr/share/nginx/html
COPY ../src/linux.png /usr/share/nginx/html

EXPOSE 80 443 	

CMD ["nginx", "-g", "daemon off;"]