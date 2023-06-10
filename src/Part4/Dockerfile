FROM nginx
USER root
COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./server.c /home/server.c
COPY ./start.sh /home/start.sh
RUN apt-get update; \
    apt-get install -y gcc spawn-fcgi libfcgi-dev && \
 groupadd --gid 2000 node \
  && useradd --uid 2000 --gid node --shell /bin/bash --create-home nod
apt-get clean
USER 2000
ENTRYPOINT ["sh", "./start.sh"]
HEALTHCHECK --interval=5s --timeout=3s CMD curl --fail http://localhost:8091/status || exit 1
