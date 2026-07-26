FROM maven:3.9.16 AS BUILDER
WORKDIR /app
COPY src ./src
COPY pom.xml .
RUN mvn clean package && \
mv target/shipping-1.0.jar shipping.jar

FROM maven:3.9.16-eclipse-temurin-17-alpine
WORKDIR /app
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"

RUN addgroup -S roboshop && adduser -S -G roboshop roboshop && \
    chown -R roboshop:roboshop /app
COPY --from=BUILDER /app/shipping.jar .
USER roboshop
CMD ["java", "-jar", "shipping.jar"]