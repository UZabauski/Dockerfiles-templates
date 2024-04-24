# Usage:
# docker build -t my-flask:v1 .
# docker run -d -p 5000:5000 my-flask:v1
# http://localhost:5000

FROM python:3.9.19

RUN pip install Flask
COPY . /

ENV FLASK_APP=hello.py
EXPOSE 5000
CMD flask run --host=0.0.0.0