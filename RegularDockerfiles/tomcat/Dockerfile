FROM eclipse-temurin:22.0.1_8-jre
LABEL maintainer="uzabauski@gmail.com"

RUN set -xe \
    && apt-get update \
    && apt-get install -qqy unzip \
    && apt-get clean

ARG TOMCAT_ID=1000
ARG TOMCAT_HOME=/opt/tomcat
ARG TOMCAT_VERSION=10.1.23

RUN wget -O /opt/tomcat.zip https://archive.apache.org/dist/tomcat/tomcat-10/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.zip && \
cd $(dirname ${TOMCAT_HOME}) && unzip tomcat.zip && \
mv apache-tomcat-${TOMCAT_VERSION} tomcat && \
rm -f /opt/tomcat/tomcat.zip && \
useradd tomcat -u ${TOMCAT_ID} --no-create-home -d ${TOMCAT_HOME} && \
chown -R tomcat: ${TOMCAT_HOME}

USER tomcat

ENV CATALINA_HOME=${TOMCAT_HOME}

EXPOSE 8080

CMD bash /opt/tomcat/bin/catalina.sh run