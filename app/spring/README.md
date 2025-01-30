Comece criando um novo projeto Spring Boot usando seu IDE preferido ou o site Spring: [https://start.spring.io/](https://start.spring.io/)

## Dependências:

* Java 21
* Maven >= 3.9

## Instalação de Dependências extras (Opicional)
Necessário para testes locais com o build da App:

```sh
# Atualizando o mavan
wget https://dlcdn.apache.org/maven/maven-3/3.9.9/binaries/apache-maven-3.9.9-bin.tar.gz
sudo tar xvf apache-maven-3.9.9-bin.tar.gz -C /opt
sudo ln -s /opt/apache-maven-3.9.9 /opt/maven

# Atualizando o jdk na IDE 
sudo dnf install java-21-amazon-corretto
java --version
```

## Processo de build:

```sh
cd build
/opt/maven/bin/mvn clean install
```

Acesse a app chamando o endpoint:

```sh

curl http://localhost:8080/ping
```

Referências para o processo de build com cópia do Java Agent: [Simplifying Spring Observability with OpenTelemetry Auto-Instrumentation and Java Agent | Part 1](https://medium.com/@ahmadalammar/simplifying-spring-observability-with-opentelemetry-auto-instrumentation-and-java-agent-part-1-ef163f4125e3), autor: [Alammar](https://medium.com/@ahmadalammar?source=post_page---byline--ef163f4125e3--------------------------------).