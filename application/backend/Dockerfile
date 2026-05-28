# Build stage
FROM maven:3.9.9-eclipse-temurin-17 AS build

WORKDIR /app

# Copy only pom.xml first to cache dependencies
COPY pom.xml .

# Fix line endings if you're on Windows
RUN dos2unix pom.xml || true

# Download dependencies
RUN mvn dependency:go-offline -B

# Copy source code
COPY src ./src

# Build the application
RUN mvn package -DskipTests

# Runtime stage
FROM eclipse-temurin:17-jre

WORKDIR /app

# Copy JAR from build stage
COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"] 