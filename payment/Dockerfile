FROM python:3.9-alpine AS BUILDER
WORKDIR /app
COPY requirements.txt .
RUN apk add --no-cache --virtual .build-deps gcc musl-dev linux-headers python3-dev \
    && pip3 install --prefix=/install -r requirements.txt \
    && apk del .build-deps

FROM python:3.9-alpine
WORKDIR /app
RUN addgroup -S roboshop && adduser -S -G roboshop roboshop && \
    chown -R roboshop:roboshop /app
COPY --from=BUILDER /install /usr/local 
COPY --chown=roboshop:roboshop payment.ini *.py requirements.txt /app/
USER roboshop
CMD ["uwsgi", "--ini", "payment.ini"]
