FROM nginx:latest
RUN apt-get update && \
    apt-get install -y \
    gcc \
    libfcgi-dev \
    spawn-fcgi \
    && rm -rf /var/lib/apt/lists/*
COPY server.c server.c
EXPOSE 8080
COPY nginx/nginx.conf /etc/nginx/nginx.conf
CMD service nginx start &&
gcc -Wall -Werror -Wextra server.c -lfcgi -o server && spawn-fcgi -p 8080 -n ./server && nginx -g 'daemon off;'

