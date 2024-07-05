# Stage 1: Development
FROM maven:3.8.1-jdk-11 as development
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean test

# Stage 2: Build
FROM maven:3.8.1-jdk-11 as build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Stage 3: Production
FROM openjdk:11-jre-slim as production
WORKDIR /app
COPY --from=build /app/target/multi-stage-java-app-1.0.0.jar /app/app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]
