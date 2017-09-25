FROM alpine
# yxakuo/buildpack-deps:redislive

MAINTAINER Allen tGuo(yxakuo@hotmail.com)

RUN apk add --update zip curl py-pip \
    && rm -rf /var/cache/apk/*

RUN mkdir -p /redislive \
    && curl -o /redislive/RedisLive-master.zip -L https://codeload.github.com/nkrode/RedisLive/zip/master

RUN cd /redislive \
    && unzip RedisLive-master.zip \
    && mv RedisLive-master/* . \
    && rm -rf RedisLive-master RedisLive-master.zip

COPY conf/redis-live.conf /redislive/src/redis-live.conf

RUN cd /redislive \
    && pip install -r requirements.txt

RUN chmod +x /redislive/src/redis-monitor.py \
    && chmod +x /redislive/src/redis-live.py \
    && chmod -R 777 /redislive

WORKDIR /redislive/src

EXPOSE 8888

# Configure container to run as an executable
CMD ["./redis-monitor.py", "--duration=120", "--quiet"]

ENTRYPOINT ["./redis-live.py"]