FROM --platform=${TARGETPLATFORM:-linux/amd64} node:12.13.0-alpine as ship

RUN apk --no-cache add curl ca-certificates \
    && addgroup -S app && adduser -S -g app app
WORKDIR /root/
ENV NPM_CONFIG_LOGLEVEL warn

RUN mkdir -p /home/app

WORKDIR /home/app
COPY package.json ./
RUN npm i

COPY . .

RUN npm test
WORKDIR /home/app/
RUN chown app:app -R /home/app && chmod 777 /tmp

USER app

CMD ["node index.js"]
