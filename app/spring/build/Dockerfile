# Estágio de pré-build usando OpenJDK 21
FROM maven:3-amazoncorretto-21 AS prebuild

# Defina o diretório de trabalho
WORKDIR /app

# Copie o arquivo pom.xml e baixe as dependências primeiro
COPY pom.xml ./
RUN mvn dependency:go-offline

# Copie o restante da aplicação
COPY src ./src

# Execute o processo de build e pacote
RUN mvn package

# Estágio final para rodar a aplicação
FROM openjdk:21-jdk

# Defina o diretório de trabalho
WORKDIR /

# Copia do JAR construído do estágio de pré-build
COPY --from=prebuild /app/target/spring-example-app.jar .
COPY --from=prebuild /app/target/opentelemetry-javaagent.jar .

# Comando para rodar a aplicação
ENTRYPOINT java -javaagent:/opentelemetry-javaagent.jar \
                -Dotel.traces.exporter=otlp \
                -Dotel.metrics.exporter=otlp \
                -Dotel.logs.exporter=otlp \
                -Dotel.exporter.otlp.endpoint=http://collector:4318 \
                -Dotel.service.name=spring-example-app \
                -jar /spring-example-app.jar