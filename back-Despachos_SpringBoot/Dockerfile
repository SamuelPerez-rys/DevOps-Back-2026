# Stage 1: Build
FROM maven:3.8.1-openjdk-17 as builder

WORKDIR /app

# Copiar el pom.xml
COPY ./Springboot-API-REST-DESPACHO/pom.xml .

# Descargar dependencias
RUN mvn dependency:go-offline

# Copiar el código fuente
COPY ./Springboot-API-REST-DESPACHO .

# Buildear la aplicación
RUN mvn clean package -DskipTests

# Stage 2: Runtime
FROM openjdk:17

WORKDIR /app

# Copiar el JAR desde el stage anterior
COPY --from=builder /app/target/*.jar app.jar

# Exponer puerto 8081
EXPOSE 8081

# Variables de entorno
ENV DB_ENDPOINT=localhost
ENV DB_PORT=3306
ENV DB_NAME=despachos_db
ENV DB_USERNAME=root
ENV DB_PASSWORD=password

# Comando para ejecutar
ENTRYPOINT ["java", "-jar", "app.jar"]
