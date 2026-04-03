# /backend/Dockerfile

# --- Stage 1: Build the JAR ---
FROM maven:3.9.14-eclipse-temurin-25 AS builder
WORKDIR /app
COPY pom.xml .
COPY src ./src
# Build the project, skipping tests to speed up the container launch
RUN mvn clean package -DskipTests

# --- Stage 2: Run the JAR ---
FROM eclipse-temurin:25
WORKDIR /app
# Copy the compiled JAR from Stage 1
COPY --from=builder /app/target/*.jar app.jar

# Expose Tomcat's default port
EXPOSE 8080

# Run the Spring Boot application
CMD ["java", "-jar", "app.jar"]