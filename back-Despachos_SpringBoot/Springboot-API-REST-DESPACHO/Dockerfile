# ETAPA 1: Construcción (Build)
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app

# Copiamos los archivos necesarios para compilar
COPY pom.xml .
COPY src ./src

# Generamos el archivo .jar
RUN mvn clean package -DskipTests

# ETAPA 2: Ejecución (Runtime seguro)
FROM openjdk:17-jdk-slim

# CUMPLIMIENTO DE PAUTA: Crear usuario no privilegiado
RUN addgroup --system spring && adduser --system spring --ingroup spring
USER spring:spring

WORKDIR /app

# Traemos el jar desde la etapa de compilación
COPY --from=build /app/target/*.jar app.jar

# Exponemos el puerto (normalmente los backends usan el 8080 u 8081)
EXPOSE 8081

ENTRYPOINT ["java", "-jar", "app.jar"]
