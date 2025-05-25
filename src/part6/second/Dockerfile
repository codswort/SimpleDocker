FROM nginx

RUN apt-get update \
    && apt-get install -y gcc libfcgi-dev spawn-fcgi \
    && rm -rf /var/lib/apt/lists/* \
    && adduser --disabled-password --gecos '' myuser && chown -R myuser /home \
    && touch /var/run/nginx.pid \
    && chown -R myuser:myuser /etc/nginx/nginx.conf /var/cache/nginx /var/run/nginx.pid

COPY nginx/nginx.conf /etc/nginx/nginx.conf
USER myuser
