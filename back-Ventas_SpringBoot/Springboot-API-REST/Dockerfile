# ETAPA 1: Build con MAVEN
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# ETAPA 2: Ejecución con JAVA (Imagen actualizada y disponible)
FROM eclipse-temurin:17-jre-alpine
# SEGURIDAD: Usuario no root
RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring

WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]
