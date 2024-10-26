FROM redis

ARG REDIS_PASSWORD
ARG REDIS_USER
ARG REDIS_USER_PASSWORD

RUN mkdir /usr/local/etc/redis
RUN touch /usr/local/etc/redis/redis.conf
RUN touch /usr/local/etc/redis/users.acl

RUN echo "bind 0.0.0.0" > /usr/local/etc/redis/redis.conf
RUN echo "requirepass ${REDIS_PASSWORD}" >> /usr/local/etc/redis/redis.conf
RUN echo "appendonly yes" >> /usr/local/etc/redis/redis.conf
RUN echo "appendfsync everysec" >> /usr/local/etc/redis/redis.conf

# Configure ACL
RUN echo "user default on >${REDIS_PASSWORD} ~* +@all" > /usr/local/etc/redis/users.acl
RUN echo "user ${REDIS_USER} on >${REDIS_USER_PASSWORD} ~* +@all" >> /usr/local/etc/redis/users.acl

CMD ["redis-server", "/usr/local/etc/redis/redis.conf", "--aclfile", "/usr/local/etc/redis/users.acl"]
