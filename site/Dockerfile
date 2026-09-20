FROM nginx:1.27-alpine

RUN rm -rf usr/share/nginx/html/*

COPY index.html /usr/share/nginx/html/

COPY kubernetes.html /usr/share/nginx/html/

COPY kubernetes-advanced.html /usr/share/nginx/html/

COPY networking.html /usr/share/nginx/html/

COPY git.html /usr/share/nginx/html/

COPY linux.html /usr/share/nginx/html/

EXPOSE 80

CMD ["nginx","-g","daemon off;"]
