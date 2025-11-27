FROM node:18-alpine

WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install --production

COPY . .

ENV NODE_ENV=production
ENV PORT=8080

EXPOSE 8080

RUN addgroup -S app && adduser -S app -G app
USER app

CMD ["node", "server.js"]
