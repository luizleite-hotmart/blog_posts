# Como utilizar o Runner do Postman

## O que é Postman Runner?

A pouco tempo a ferramenta Postman lançou uma parte, em que é possível fazer automatizações nas suas coleções. Através dessa 
feature conseguimos fazer várias coisas, como:

1. Testes automatizados sobre as coleções para entradas padrão.
2. Testes de carga.
3. Chamadas alterando input como path, query param ou atributo do body.

Essa parte permite que sejam executadas chamadas que estão em um CSV e validação destas.

## Rodar multiplas chamadas com CSV.

Nesse artigo vamos mostrar como rodar uma chamada sobre valores que estão em um CSV.

A API que será utilizada para os testes é a do próprio [ramdom user](https://randomuser.me/api/), documentação completa pode ser vista [aqui](https://randomuser.me/documentation).

Quando fazemos essa chamada podemos colocar vários resultados, um deles é o `seed` que retorna sempre o mesmo usuário. Mudando 
a chamada de `https://randomuser.me/api/?seed=foobar` para uma chamada parametrizada com `{{}}` podemos clicar no botão superior em Runner.
Ao escolher nossa coleção que contem essa API podemos fazer várias coisas, como:

+ Chamadas em loop com algumas interações.
+ Colocar um delay sobre cada chamada.
+ Selecionar um arquivo csv com quais são os valores dos parâmetros que vão ser substituídos na chamada.  
+ Validar respostas para determinada chamada.

Então para validar mostrar um pouco vamos pegar o arquivo csv com o seguinte conteúdo
```csv
seed,answer
foobar,Britney
foo,April
bar,Niskanen
teste,luizleite
```

O arquivo contém duas colunas, a primeira tem o nome `seed` que vai substituir o query param da nossa chamada `https://randomuser.me/api/?seed={{seed}}`
O segundo vai substituir um teste simples que é implementado na seguinte parte:

![Postman](https://lh5.googleusercontent.com/9UPjGsrRjWaBkGURwxJhRO1JaQyVXc-Hz-HF7lOLK14LUsP23MJnuQPihs1a_EAhKi77tZNYtuuXIv9uOoRk=w1920-h976)

o código é:
```
// assertation
pm.test("Body matches string", function () {
    pm.expect(pm.response.text()).to.include(pm.variables.get("answer"));

});
``` 

a parte de `pm.variables.get("answer")` é capaz de pegar uma variavel que podemos passar. A única coisa que esse teste faz é 
validar se o que está em answer existe no body do response.

![Before running](https://lh4.googleusercontent.com/9ybNLrmOwnKATh-uU9csntmlP3UWsxFxAedZ8W3STkqZ5dlXiRLwDhogNK6gH2-jxgeIs6khtVUxlCzAZ_UA=w1920-h976)

Para esse teste fizemos os 3 primeiros resultados darem certo e o último ter um erro, como resultado ficamos com a seguinte resposta:

![Result](https://lh3.googleusercontent.com/Ft5SGGPFEbCl7X1yyV-hw0Xw5iYqy0IdzqwYEVlzVCKtRBhdjQSUnl4HJ5yY3zG-fuaQjyqSMF_D9H2ueapn=w1920-h976-rw)

## Conclusão

A um tempo atrás existiam vários cenários, em que faziamos várias chamadas em loop, na época existia um código compartilhado para fazer isso. 
Provavelmente todos já tiveram que executar um cenário assim para múltiplos parâmetros do qual você fez um export do banco de dados.
Depois que entendi como funciona o collection runner e testes comecei a fazer chamadas bem mais criativas e que ficavam salvas para momentos
futuros. 

É uma opção excelente para um cenário em que necessita de reprocessamento de um lote sendo que pode validar só os casos que deram sucesso.






 