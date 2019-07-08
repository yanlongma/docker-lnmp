ARG REDIS_VERSION
FROM redis:${REDIS_VERSION}-alpine

LABEL maintainer="YanlongMa <json_vip@163.com>"

#RUN mkdir -p /usr/local/etc/redis
#COPY redis.conf /usr/local/etc/redis/redis.conf

#CMD [ "redis-server", "/usr/local/etc/redis/redis.conf" ]
CMD [ "redis-server"]

EXPOSE 6379