FROM node:12
ENV NPM_CONFIG_LOGLEVEL warn
WORKDIR /usr/src/app

COPY . .
RUN yarn install --production --ignore-engines --frozen-lockfile
RUN yarn add typescript
RUN yarn build

EXPOSE 80
CMD ["yarn", "start"]
