Comece criando um novo projeto Spring Boot usando seu IDE preferido ou o site Spring: [https://start.spring.io/](https://start.spring.io/)

## Dependências:

* Java 21
* Maven >= 3.9

## Processo de build:

```sh
cd build
mvn clean install
```

Para execução do coletor volte a pasta raiz e execute:

```sh
docker-compose up
```

Acesse a app chamando seu endpoint:

```sh
curl http://localhost:8080/ping
```

Referências para o processo de build com cópia do Java Agent: [Simplifying Spring Observability with OpenTelemetry Auto-Instrumentation and Java Agent | Part 1](https://medium.com/@ahmadalammar/simplifying-spring-observability-with-opentelemetry-auto-instrumentation-and-java-agent-part-1-ef163f4125e3), autor: [Alammar](https://medium.com/@ahmadalammar?source=post_page---byline--ef163f4125e3--------------------------------).