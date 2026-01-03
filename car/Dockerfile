# Stage 1: Build using a maintained Maven image
FROM maven:3.9.6-eclipse-temurin-17-alpine AS builder
WORKDIR /app
COPY ./pom.xml ./
COPY ./src ./src
RUN mvn clean package -DskipTests

# Stage 2: Runtime using a maintained JRE image
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
# Copy the JAR from the builder stage
COPY --from=builder /app/target/*.jar app.jar

ENTRYPOINT ["java", "-jar", "app.jar"]