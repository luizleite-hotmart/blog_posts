# Como usar GraphQL com Quarkus

Tudo que está nesse projeto pode ser encontrado no repositório [GitHub](https://github.com/luizleite-hotmart/quarkus-graphql).

Para a nossa poc o que fizemos foi primeiro pegar.

## Intro ao projeto 

Esse projeto já foi contextualizado no [dev.to](https://dev.to/luizleite_/como-usar-graphql-com-quarkus-ndn). Basicamente o que ele faz
é pegar usar o get da api encontrada em `https://randomuser.me/api` e aplica um GraphQL na resposta.

## GRAPHQL On Quarkus

### Dependências

Para utilizar o GraphQL neste projeto utilizamos uma dependência da [Vert.x](https://vertx.io/), documentação completa você pode encontrar
[aqui](https://vertx.io/docs/vertx-web-graphql/java/) para importar basta adicionar em seu pom.xml

```xml
    <dependency>
      <groupId>io.vertx</groupId>
      <artifactId>vertx-web-graphql</artifactId>
    </dependency>
```
  
