# Usage:
# docker build -t my-webgoat:v1 .
# docker run -d -p 8081:8080 my-webgoat:v1
# http://localhost:8081/WebGoat/

FROM java:jre-alpine

ENV WEBGOAT_VERSION 7.0.1
ENV WEBGOAT_FILE webgoat-container-$WEBGOAT_VERSION-war-exec.jar
ENV WEBGOAT_URL https://github.com/WebGoat/WebGoat/releases/download/$WEBGOAT_VERSION/$WEBGOAT_FILE

WORKDIR /app

RUN set -xe \
    && apk add -U curl \
    && curl -sSL $WEBGOAT_URL > webgoat.jar \
    && apk del curl \
    && rm -rf /var/cache/apk/*

EXPOSE 8080

CMD ["java", "-jar", "webgoat.jar"]