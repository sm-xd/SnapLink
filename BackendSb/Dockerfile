# Use Maven 3.9 with Java 21 to build
FROM maven:3.9.6-eclipse-temurin-21 AS build

WORKDIR /app

# Copy everything into container
COPY . .

# Build the Spring Boot project (skip tests)
RUN mvn clean package -DskipTests

# Use lightweight Java 21 runtime to run app
FROM eclipse-temurin:21-jre

WORKDIR /app

# Copy the JAR built in previous stage
COPY --from=build /app/target/*.jar app.jar

# Expose port
EXPOSE 8080

# Run the Spring Boot app
ENTRYPOINT ["java", "-jar", "/app/app.jar"]