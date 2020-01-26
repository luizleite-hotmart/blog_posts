# Como fazer testes unitários em controllers de um app Spring Boot

## Mas pra que?
Antes de começar a falar sobre o como fazer esses teste, temos que primeiro entender o motivo deles serem importantes e, considerados necessários. Os teste aqui vão fazer um mock de banco, conexões, serviços, com isso, a única parte que vai ser testada será o controller.

A maioria dos desenvolvedores, eu me incluo nessa parte, compartilha que nessa camada não deve existir regra de negócio ou chamada para os dados, existem outras camadas para isso. Então a única coisa que vai ser testada será uma resposta simulada (Mockada no bom português), muitos vêem que isso não é suficiente para criar testes unitários e testes end-to-end seriam mais adequados, mas vamos para um exemplo.

Imagine que você possui o seguinte código VO:

```Java
class 
```

e em um belo dia alguém decide subir o código novo removendo um dos atributos, que já foram combinados em contrato com as outras aplicações e ele fica assim:

```java
class
```

Claro que um teste de integração caso estejam bem executados pegariam antes de ir para produção, mas testes de integração custam caro e são lentos para executar. No conceito de Fail-Fast, em que quanto antes falhar menos danoso será para o seu projeto testes de contrato facilitariam muito para uma falha e correção antecipada.

## Como fazer?
Já avisei aqui que este será focado em Spring Boot caso esteja em outro framework pode ser diferente.

Antes de começar vamos criar um projeto para isso você pode apenas ir em [Start Spring](https://start.spring.io/) e criar seu projeto apenas com a dependência Web, ou seguir