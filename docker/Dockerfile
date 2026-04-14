FROM nginx:1.27-alpine

LABEL author="Abhilash Indulkar"

WORKDIR /usr/share/nginx/html

COPY src/ .

EXPOSE 80

USER nginx

CMD ["nginx", "-g", "daemon off;"]
