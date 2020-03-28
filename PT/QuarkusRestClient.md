# Como usar GraphQL com Quarkus

Tudo que está nesse projeto pode ser encontrado no repositório [GitHub](https://github.com/luizleite-hotmart/quarkus-graphql).

Para criar o projeto utilizamos o próprio site de bootstrap do quarkus para criar o seu pode acessar [aqui](https://code.quarkus.io/).

## Dependências adicionadas

As dependências que vamos usar podem ser encontradas diretamente pelo bootstrap. São as seguintes:

 - JSON-B  _Utilizada para fazer json bind automático_
 - REST Cliente _Utilizada para criar chamada rest_
 
 Para quem usa maven as dependencias vão ficar assim:
 
 ```xml
     <dependency>
       <groupId>io.quarkus</groupId>
       <artifactId>quarkus-resteasy-jsonb</artifactId>
     </dependency>
     <dependency>
       <groupId>io.quarkus</groupId>
       <artifactId>quarkus-rest-client</artifactId>
     </dependency>
 ```

