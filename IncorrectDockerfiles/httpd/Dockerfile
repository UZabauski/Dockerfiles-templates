# Usage:
# docker build -t my-httpd:v1 .
# docker run -d -p 8082:80 my-httpd:v1
# http://localhost:8082

FROM centos

RUN yum update -y && \
    yum install httpd -y && \
    yum clean all
RUN echo "My httpd container!" > /var/www/html/index.html

EXPOSE 80

ENTRYPOINT ["httpd"]
CMD ["-DFOREGROUND"]