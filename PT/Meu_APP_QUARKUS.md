# Meu primeiro app com Quarkus

Hoje eu decidi que iria criar meu primeiro APP utilizando Quarkus, mas por que?! Na verdade é só uma validação mesmo eu sei que o Spring boot tá bem na frente em alguns pontos, mas [Quarkus](https://quarkus.io/) e [Micronaut](https://micronaut.io/) são ótimas alternativas, e estão ganhando espaço principalmente por causa do BOOM que temos de GRAAL_VM.

Na verdade, esse é meu segundo projeto com Quarkus o primeiro que tive oportunidade de fazer foi no DevoxxUK19 juntamente com os commiters e criadores do projeto. Lá tive oportunidade de tirar duvidas e vi o potencial que existe dentro dessa parte.

## O que é QUARKUS.IO?

Quarkus é uma alternativa de framework java assim como spring boot e micronaut. Tem como objetivo ser container first alguns dizem até ser Kubernets nativo. A home do projeto mostra um conceito bem legal de ser o Java supersônico e isso é possível.
Uma das coisas mais interessantes que eu achei foi ao ler essa parte do site em que eles comentam sobre live coding. Em que há a mudança de quase um paradigma Java.
De:
Escreva código -> Compile -> Deploy -> Refresh -> Repeat
Para:
Escreva código ->Refresh -> Repita
E parece idiota mais isso tira um tempo gigantesco de desenvolvimento.

## Start do projeto
Para dar start no seu projeto basta rodar o comando a seguir


```bash
mvn io.quarkus:quarkus-maven-plugin:0.19.1:create \
    -DprojectGroupId=com.luizleiteoliveira \
    -DprojectArtifactId=helloworld \
    -DclassName="com.luizleiteoliveira.helloworld.ApplicationResource" \
    -Dpath="/hello"

```

O que esse comando está gerando ?
 * A estrutura completa do Maven
 * Uma classe ApplicationResource dentro de /hello
 * Uma classe de teste associada a classe acima
 * Uma landing page disponível ao subir a aplicação em http://localhost:8080 
 * Dois exemplos de Dockerfile para modos nativos e jvm

## O Hello World

Para criar o seu primeiro Hello World em rest nem tem muito esforço pois dentro da classe que você deu o start já vem ela automatica da seguinte forma:

```java
@Path("/hello")
public class ApplicationResource {

    @GET
    @Produces(MediaType.TEXT_PLAIN)
    public String hello() {
        return "hello";
    }
}
```

Depois disso basta executar o comando em um terminal para rodar o quakus em modo de desenvolvimento:
```bash
./mvnw compile quarkus:dev
```

Esse comando já habilita uma porta 5005 para debug, com isso, deve ser feita uma configuração de debug remoto na sua IDE favorita.

##Configurando Debug Remoto do Intellij:

Dentro da edição de configurações do Intellij (CTRL+SHIT + A -> Edit Configurations)
Clique no '+' e adicione uma configuração para a porta 5005 deve ficar parecido com essa:

![Imagem mostrando porta como 5005 e host = localhost ](https://raw.githubusercontent.com/luizleite-hotmart/presentations/master/images/post-quarkus/Screenshot%20from%202019-07-31%2008-10-24.png
)

##Primeiro teste o 'Hotdeploy'

Na hora que fiz a parte acima já pensei é perdi meu Hotdeploy vou ter que jogar isso no chão toda hora e me ferrei então resolvi fazer o teste e enquanto minha aplicação estava em rodando alterei o meu hello para:

```java
@Path("/hello")
public class ApplicationResource {

    @GET
    @Produces(MediaType.TEXT_PLAIN)
    public String hello(@QueryParam("who") final String who) {
        return "hello "+ who;
    }
}
```

Assim que chamei o endpoint http://localhost:8080/hello?who=teste apareceu no meu terminal a mensagem: 'Hot replace total time: 0.726s' e não é que meu endpoint estava realmente alterado e isso é uma situação que eu teria que com certeza eu deveria reiniciar minha aplicação só que ele fez isso sem reclamar.
Claro que eu não fui a fundo mas funcionou muito bem até agora. A partir da próxima vez vou começar a fazer uma aplicação mais real com o quarkus vendo como é salvar os dados e talvez consumir uma API ou algo assim.


##O poder em ação
Até agora sem enormes vantagens e é a hora que entramos na parte legal, vamos para o nativo. Depois da aplicação ficar do jeito que está existe um comando maven para buildar um binario da aplicação.

`mvn package -Pnative`

Para executar esse comando suas variáveis de ambiente assim como seu Graal já deve estar configurado para funcionar corretamente. Após a execução vai ser criado dentro do /target um executável, para rodar é bem simples é só ./<ARQUIVO_GERADO> , e agora sim o susto em 0.003s minha aplicação está rodando.
![Imagem mostrando terminal e quarkus do app rodando em 0.003 segundos](https://raw.githubusercontent.com/luizleite-hotmart/presentations/master/images/post-quarkus/Screenshot%20from%202019-07-31%2008-19-33.png)

##Conclusão.

Como já falei os testes que eu fiz não foram nada só mais um tipo de primeira impressão, mas até agora tá bem tranquilo. Achei muito simples o primeiro start do projeto e coloca-lo para funcionar foi absurdo o tanto que foi rápido. 
Um outro ponto que gostei que é dentro do site existe uma parte de [Guides](https://quarkus.io/guides/), mostrando vários tutoriais de como executar coisa 'x' em Quarkus. 

Sobre o meu projeto você pode consultar dentro do github.

{% github https://github.com/luizleite-hotmart/quarkus-poc/ %}
