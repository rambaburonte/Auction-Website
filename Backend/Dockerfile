# Build stage
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mkdir -p target && mvn clean package -DskipTests

# Package stage
FROM openjdk:17-slim
WORKDIR /app
COPY --from=build /app/target/auction12-0.0.1-SNAPSHOT.jar /app/auction12-0.0.1-SNAPSHOT.jar
EXPOSE 8080
CMD ["java", "-jar", "auction12-0.0.1-SNAPSHOT.jar"]
