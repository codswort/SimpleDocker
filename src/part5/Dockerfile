FROM nginx

RUN apt-get update \
    && apt-get install -y gcc libfcgi-dev spawn-fcgi \
    && rm -rf /var/lib/apt/lists/* \
    && adduser --disabled-password --gecos '' myuser && chown -R myuser /home \
    && touch /var/run/nginx.pid \
    && chown -R myuser:myuser /etc/nginx/nginx.conf /var/cache/nginx /var/run/nginx.pid

COPY server.c server.c

RUN gcc -Wall -Werror -Wextra server.c -lfcgi -o server

COPY nginx/nginx.conf /etc/nginx/nginx.conf
USER myuser

EXPOSE 8080

CMD service nginx start && spawn-fcgi -p 8080 -n ./server && nginx -g 'daemon off;'
