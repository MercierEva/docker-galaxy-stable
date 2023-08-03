FROM alpine:3.14 as build

RUN apk add --no-cache bash python3 cmd:pip3 make curl\
    && apk add --no-cache --virtual build-dep gcc libxml2-dev libxslt-dev musl-dev linux-headers python3-dev \
    && pip3 install bioblend \
    && mkdir -p /src/bioblend/ 

RUN pip3 install pep8 tox --ignore-installed

WORKDIR /src/bioblend

RUN tox --notest

COPY ./run.sh /src/bioblend/run.sh

ENTRYPOINT ./run.sh
