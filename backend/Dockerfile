FROM python:3.7.6-alpine3.11

RUN apk update

RUN apk add --no-cache --virtual .build-deps \
                gcc \
                libc-dev \
                linux-headers \
                mariadb-dev \
                python3-dev \
                postgresql-dev \
                mysql

RUN pip install --upgrade \ virtualenv --trusted-host pypi.python.org

ADD ./requirements.txt /tmp/

# Install PyPi dependencies
WORKDIR /tmp
RUN pip install --upgrade pip && pip install -r requirements.txt

ADD . /code/

RUN mkdir -p /data/uploads
RUN mkdir -p /static

RUN chmod -R a+rw /data
RUN chmod -R a+rw /static

ADD entrypoint.sh /
RUN chmod +x /entrypoint.sh

ENV PYTHONUNBUFFERED 1
WORKDIR /code/

EXPOSE 8000

CMD /./entrypoint.sh
