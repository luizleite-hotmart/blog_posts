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

Antes de começar vamos criar um projeto para isso você pode apenas ir em [Start Spring](https://start.spring.io/) e criar seu projeto apenas com a dependência Web, ou seguir o tutorial que fiz no [GitHub](https://github.com/luizleite-hotmart/restControllerTest)

Se estiver tudo certo as dependências do seu Pom devem parecer com o código a seguir.

```xml
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
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
    </dependencies>
```

Agora vamos criar um VO simples de açõs que tem uma data, o código da ação e, o valor que ela tem. O meu código da classe ficou da seguinte forma.

```java
import java.math.BigDecimal;
import java.util.Date;

public class Stock {
    private Date date;
    private String code;
    private BigDecimal value;

    public Stock(Date date, String code, BigDecimal value) {
        this.date = date;
        this.code = code;
        this.value = value;
    }

    public BigDecimal getValue() {
        return value;
    }

    public void setValue(BigDecimal value) {
        this.value = value;
    }

    public String getCode() {
        return code;
    }

    public void setCode(String code) {
        this.code = code;
    }

    public Date getDate() {
        return date;
    }

    public void setDate(Date date) {
        this.date = date;
    }
}
```

Agora para ser um pouco mais dificil vamos criar um service que retorna um algumas ações, o meu ficou da seguinte forma

```java
import java.math.BigDecimal;
import java.util.Date;
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

@Service
public class StockServices {
    
    public List<Stock> createMockStocks(int howMany) {
        return IntStream.range(0, howMany).mapToObj(i -> new Stock(new Date(), "STK" + i, BigDecimal.valueOf(i))).collect(Collectors.toList());
    }
}
```

e agora pra finalizar a nossa camada Web que deve ter ficado algum código assim:

```java
import com.luizleiteoliveira.restControllerTest.service.StockServices;
import com.luizleiteoliveira.restControllerTest.vo.Stock;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.ResponseBody;

import java.util.List;

@Controller
public class StockController {

    private final StockServices stockServices;

    public StockController(StockServices stockServices) {
        this.stockServices = stockServices;
    }

    @GetMapping(value = "/stocks")
    public @ResponseBody
    List<Stock> getStocks(@RequestParam("howMany") int howMany) {
        return stockServices.createMockStocks(howMany);
    }
}
```

