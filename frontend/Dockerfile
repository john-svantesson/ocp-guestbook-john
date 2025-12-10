FROM registry.access.redhat.com/ubi10/nginx-126:10.0

WORKDIR /opt/app-root/src

COPY index.html /opt/app-root/src/index.html
COPY nginx.conf /opt/app-root/etc/nginx/nginx.conf

EXPOSE 8080

CMD ["nginx", "-c", "/opt/app-root/etc/nginx/nginx.conf", "-g", "daemon off;"]