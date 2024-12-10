# Étape 1 : Build avec Maven
FROM maven:3.8.8-eclipse-temurin-17 AS builder
WORKDIR /app
COPY . .
RUN mvn clean package -DskipTests

# Étape 2 : Runtime minimal
FROM openjdk:17-alpine
COPY --from=builder /app/target/words.jar /usr/local/lib/words.jar
COPY --from=builder /app/target/dependency /usr/local/lib/dependency


EXPOSE 8080
CMD ["java", "-Xmx8m", "-Xms8m", "-jar", "/usr/local/lib/words.jar"]
