FROM debian:9

COPY ./sources.list /etc/apt/sources.list

RUN apt-get update \
    && apt-get install -y \
        wget \
        procps \
        curl \
        git \
        python \
        python3 \
        python3-pip \
        build-essential \
        g++ \
        xvfb \
        apt-transport-https \
        unzip \
        gettext-base \
        socat \
    && wget -qO- https://deb.nodesource.com/setup_12.x | bash \ 
    && apt-get install -y nodejs \
    && rm -rf /var/lib/apt/lists/*

RUN npm install -g yarn

RUN yarn cache clean

ENV LL_TAG=v7.1.0
RUN git clone https://github.com/LearningLocker/learninglocker.git /opt/learninglocker \
    && cd /opt/learninglocker \
    && git checkout $LL_TAG \
    && yarn install --force --ignore-engines \
    && yarn build-all

WORKDIR /opt/learninglocker

EXPOSE $UI_PORT $API_PORT

COPY env.template .env
COPY entrypoint-common.sh entrypoint-common.sh
COPY entrypoint-ui.sh entrypoint-ui.sh

ENTRYPOINT ["./entrypoint-common.sh"]
