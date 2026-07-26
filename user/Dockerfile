FROM node:20.20-alpine3.22 AS BUILDER
WORKDIR /app
COPY package.json .
COPY *.js .
RUN npm install

FROM node:20.20-alpine3.22
WORKDIR /app
ENV MONGO="true" \
    REDIS_URL="redis://redis:6379" \
    MONGO_URL="mongodb://mongodb:27017/users"

RUN addgroup -S roboshop && adduser -S -G roboshop roboshop && \
    chown -R roboshop:roboshop /app
COPY --from=BUILDER /app /app
USER roboshop
CMD ["node", "server.js"]