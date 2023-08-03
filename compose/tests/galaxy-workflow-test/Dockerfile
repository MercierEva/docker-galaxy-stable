FROM alpine:3.14

ENV TEST_REPO=${TEST_REPO:-https://github.com/usegalaxy-eu/workflow-testing} \
    TEST_RELEASE=${TEST_RELEASE:-master}

RUN apk add --no-cache bash python3 curl make cmd:pip3 \
    && apk add --no-cache --virtual build-dep libxml2-dev libxslt-dev musl-dev linux-headers python3-dev hdf5 hdf5-dev bzip2-dev build-base\
    && pip3 install --upgrade pip setuptools wheel \
    && pip3 install h5py numpy \
    && pip3 install planemo --ignore-installed \
    && mkdir /src && cd /src \
    && curl -L -s $TEST_REPO/archive/$TEST_RELEASE.tar.gz | tar xzf - --strip-components=1 \
    && apk del build-dep

# Make Python3 standard
RUN ln /usr/bin/python3 /usr/bin/python && ln /usr/bin/python3 /usr/bin/python2

ADD ./run.sh /usr/bin/run.sh

WORKDIR /src

ENTRYPOINT /usr/bin/run.sh
