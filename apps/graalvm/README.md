# OpenTelemetry App de teste com Graalvm 
Baseado na documentação [OpenTelemetry Spring Native Example](https://github.com/open-telemetry/opentelemetry-java-examples/tree/main/spring-native)

## Dependências:

* GraalVM com Java 17

## Processo de build:

```sh
cd graalvm-app
../gradlew bootBuildImage --imageName=otel-native-graalvm
```

Para execução do coletor volte a pasta raiz e execute:

```sh
docker-compose up
```

Acesse a app chamando seu endpoint:

```sh
curl http://localhost:8080/ping
```