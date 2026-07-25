FROM maven:3.9.16-eclipse-temurin-17 as builder
WORKDIR /app 
COPY pom.xml .
RUN mvn clean package
COPY src .

FROM maven:3.9.16-eclipse-temurin-17 
WORKDIR /app 
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
COPY app/target/shipping-*.jar app/shipping.jar
USER roboshop
CMD ["java", "-jar","shipping.jar"]
