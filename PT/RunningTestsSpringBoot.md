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

Vamos criar uma classe bem simples pra fazer alguns testes, para isso vamos criar um usuário:

```java
public class User {

    String name;
    int age;
    String document;

    public User(String name, int age, String document) {
        this.name = name;
        this.age = age;
        this.document = document;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getDocument() {
        return document;
    }

    public void setDocument(String document) {
        this.document = document;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", document='" + document + '\'' +
                '}';
    }
}
```

e o teste que vai executar sobre essa classe vai ser:

```java
import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertTrue;


public class EntityTest {

    @Test
    public void UserTest() {
        User user = new User("name", 12, "DOC12543");
        assertEquals("name", user.name);
        assertTrue(user.toString().contains("User{"));
    }
}
```
E deste jeito já tá rodando os nossos testes em 135ms enquanto se utilizarmos a notação `@SpringBootTest` roda em 459ms,
parece pouco mas vamos lembrar que esse teste é o mais simples e nossa aplicação não tem nada configurado. Mesmo assim 
a diferenção entre os dois testes já foi mais que o triplo.

 

### Camada de dados

### Camada Web




Twitter: [luizleite_](https://twitter.com/luizleite_)

Twitch: [coffee_and_code](https://www.twitch.tv/coffee_and_code)

Linkedin: [luizleiteoliveira](https://www.linkedin.com/in/luizleiteoliveira/)

dev.to: [luizleite_](https://dev.to/luizleite_)