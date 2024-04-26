# Usage:
# docker build -t my-webgoat:v1 .
# docker run -d -p 127.0.0.1:8085:8085 -p 127.0.0.1:9090:9090 my-webgoat:v1 
# http://localhost:8085/WebGoat/

FROM eclipse-temurin:22.0.1_8-jre
LABEL NAME = "WebGoat: A deliberately insecure Web Application"
LABEL maintainer = "WebGoat team"

ENV WEBGOAT_V 2023.8
ENV WEBGOAT_F webgoat-$WEBGOAT_V.jar
ENV WEBGOAT_DOWNLOAD_URL https://github.com/WebGoat/WebGoat/releases/download/v$WEBGOAT_V/$WEBGOAT_F
ENV WEBGOAT_PORT=8085
ENV TZ=Europe/Amsterdam


RUN set -xe \
    && apt-get update \
    && apt-get install -qqy curl \
    && useradd -ms /bin/bash webgoat \
    && chgrp -R 0 /home/webgoat \
    && chmod -R g=u /home/webgoat \
    && curl -sSL $WEBGOAT_DOWNLOAD_URL > /home/webgoat/webgoat.jar \
    && chown -R webgoat:webgoat /home/webgoat/webgoat.jar \
    && apt-get clean

USER webgoat

#COPY --chown=webgoat target/webgoat-*.jar /home/webgoat/webgoat.jar

EXPOSE 8085
EXPOSE 9090

WORKDIR /home/webgoat
ENTRYPOINT [ "java", \
   "-Duser.home=/home/webgoat", \
   "-Dfile.encoding=UTF-8", \
   "--add-opens", "java.base/java.lang=ALL-UNNAMED", \
   "--add-opens", "java.base/java.util=ALL-UNNAMED", \
   "--add-opens", "java.base/java.lang.reflect=ALL-UNNAMED", \
   "--add-opens", "java.base/java.text=ALL-UNNAMED", \
   "--add-opens", "java.desktop/java.beans=ALL-UNNAMED", \
   "--add-opens", "java.desktop/java.awt.font=ALL-UNNAMED", \
   "--add-opens", "java.base/sun.nio.ch=ALL-UNNAMED", \
   "--add-opens", "java.base/java.io=ALL-UNNAMED", \
   "--add-opens", "java.base/java.util=ALL-UNNAMED", \
   "--add-opens", "java.base/sun.nio.ch=ALL-UNNAMED", \
   "--add-opens", "java.base/java.io=ALL-UNNAMED", \
   "-Drunning.in.docker=true", \
   "-jar", "webgoat.jar", "--server.address", "0.0.0.0" ]