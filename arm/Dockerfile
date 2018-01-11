FROM hypriot/rpi-alpine:3.6

ENV GOOGLE_HOME_KODI_CONFIG="/config/kodi-hosts.config.js"
ENV NODE_ENV=production
ENV PORT=8099

RUN apk -U update && \
    apk -U upgrade && \
    apk -U add \
        nodejs \
        nodejs-npm \
    && \
    rm -rf /var/cache/apk/*

VOLUME /config
RUN mkdir -p /home/node/app
WORKDIR /home/node/app

COPY package*.json ./
RUN npm install --production && npm cache clean --force
COPY ./ .

EXPOSE 8099
USER node
CMD ["node", "server.js"]
