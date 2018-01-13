FROM arm32v6/alpine:3.7

ENV GOOGLE_HOME_KODI_CONFIG="/config/kodi-hosts.config.js"
ENV NODE_ENV=production
ENV PORT=8099

COPY tmp/qemu-arm-static /usr/bin/qemu-arm-static

RUN apk -U update && \
    apk -U upgrade && \
    apk -U add \
        nodejs \
        nodejs-npm \
    && \
    rm -rf /var/cache/apk/* && \
    adduser -S node


VOLUME /config
RUN mkdir -p /home/node/app
WORKDIR /home/node/app

COPY package*.json ./
RUN npm install --production && npm cache clean --force
COPY ./ .

EXPOSE 8099
USER node
CMD ["node", "server.js"]
