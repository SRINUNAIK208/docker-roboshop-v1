FROM maven:3.9.16-eclipse-temurin-17 AS builder
WORKDIR /app 
COPY pom.xml .
COPY src ./src
RUN mvn clean package


FROM eclipse-temurin:17-jre
WORKDIR /app 
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
COPY --from=builder /app/target/shipping-*.jar /app/shipping.jar
USER roboshop
CMD ["java", "-jar","shipping.jar"]
