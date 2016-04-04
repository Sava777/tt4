FROM python:2.7
ENV PYTHONUNBUFFERED 1
RUN apt-get update && apt-get install -y python python-pip python-dev uwsgi-plugin-python git mc mysql-client netcat && rm -rf /var/lib/apt/lists/* && apt-get autoremove -y

RUN addgroup --system django
RUN adduser --system --shell /bin/bash --disabled-password --home /home/django django
RUN adduser django django

USER django
RUN mkdir /home/django/app
WORKDIR /home/django/app
RUN git clone git://github.com/kirpit/django-sample-app.git /home/django/app && cd /home/django/app
# ADD . /app/
COPY docker-entrypoint.sh /home/django/app/
USER root
RUN pip install -r requirements.txt
RUN pip install uwsgi
RUN pip install MySQL-python

EXPOSE 8080
CMD /home/django/app/docker-entrypoint.sh
