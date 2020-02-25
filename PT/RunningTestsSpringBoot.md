## Notações para testes unitários em Spring Boot

### Introdução
A um tempo fui rodar um teste que tinha a anotação `@SpringBootTest` e quando começou a rodar, já apareceu o Banner do Spring Boot
e uma mensagem:
` contextLoader = 'org.springframework.boot.test.context.SpringBootContextLoader'` 

Quando eu vi isso, eu já vi que eu nem sabia o por quê de utilizar essa anotação e o qual deveria usar. Então o objetivo 
deste post é de mostrar quais devem ser utilizadas pra qual cenário especifico.

###  Setup Inicial 
Para o nosso setup inicial, vamos utilizar o mínimo e o pom vai precisar das seguintes depêndencias:

```xml
        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
            <exclusions>
                <exclusion>
                    <groupId>org.junit.vintage</groupId>
                    <artifactId>junit-vintage-engine</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
```  
a exclusão do `junit-vintage-engine` é necessária para utilização do JUnit5 que utiliza o `junit-jupiter-engine` .
O uso do H2 vai ser para testar a camada de dados.

### Camada de serviços e DTOs

### Camada de dados

### Camada Web




Twitter: [luizleite_](https://twitter.com/luizleite_)

Twitch: [coffee_and_code](https://www.twitch.tv/coffee_and_code)

Linkedin: [luizleiteoliveira](https://www.linkedin.com/in/luizleiteoliveira/)

dev.to: [luizleite_](https://dev.to/luizleite_)