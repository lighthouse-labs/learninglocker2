FROM debian:9

COPY ./sources.list /etc/apt/sources.list

RUN apt-get update \
    && apt-get install -y \
        wget \
        procps \
        curl \
        git \
        python \
        build-essential \
        xvfb \
        apt-transport-https \
        unzip \
        gettext-base \
        socat \
    && wget -qO- https://deb.nodesource.com/setup_8.x | bash \
    && apt-get install -y nodejs \
    && rm -rf /var/lib/apt/lists/*

RUN npm install -g yarn

RUN git clone https://github.com/lighthouse-labs/learninglocker.git /opt/learninglocker \
    && cd /opt/learninglocker \
    && yarn install \
    && yarn build-all

WORKDIR /opt/learninglocker

EXPOSE $UI_PORT $API_PORT

COPY env.template .env
COPY entrypoint-common.sh entrypoint-common.sh
COPY entrypoint-ui.sh entrypoint-ui.sh

ENTRYPOINT ["./entrypoint-common.sh"]

