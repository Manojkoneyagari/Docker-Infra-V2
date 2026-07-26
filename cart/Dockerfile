
FROM node:20.20-alpine3.22 AS BUILDER
WORKDIR /app
COPY *.js .
COPY *.json .
RUN npm install

FROM node:20.20-alpine3.22
WORKDIR /app
ENV REDIS_HOST="redis" \
 CATALOGUE_HOST="catalogue" \
  CATALOGUE_PORT=8080
   
RUN addgroup -S roboshop && adduser -S -G roboshop roboshop && \
    chown -R roboshop:roboshop /app
COPY --from=BUILDER /app /app
USER roboshop
CMD ["node", "server.js"]