FROM openjdk:21-jdk
ADD build/target/spring-example-app.jar /spring-example-app.jar
ADD build/target/opentelemetry-javaagent-2.11.0.jar /opentelemetry-javaagent.jar

ENTRYPOINT java -javaagent:/opentelemetry-javaagent.jar \
                -Dotel.traces.exporter=otlp \
                -Dotel.metrics.exporter=otlp \
                -Dotel.logs.exporter=otlp \
                -Dotel.exporter.otlp.endpoint=http://collector:4318 \
                -Dotel.service.name=spring-example-app \
                -jar /spring-example-app.jar