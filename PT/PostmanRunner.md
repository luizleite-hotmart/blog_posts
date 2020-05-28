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

A API que será utilizada para os testes é a do próprio [dev.to](https://dev.to/), documentação completa pode ser vista [aqui](https://docs.dev.to/api/).

Para isso criamos uma coleção chamada `dev.to` que contém a chamada de artigos `curl https://dev.to/api/articles`, ao adicionar o parâmetro `username`
a API começa a retornar os artigos de um usuário específico.


 