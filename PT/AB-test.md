## Criando api de AB teste em 2 horas

### O que são testes AB

Resumidamente testes AB são aqueles que, um usuário siga um fluxo, e sempre siga esse fluxo, e algum outro siga o fluxo em 
uma mesma versão. Hoje em dia a gente usa testes AB para diversas coisas como: 

 - [x] Dividir fluxo de usuários (Ex: 10% irão assistir o botão na cor verde o resto de outra cor)
        _Detalhe importante nesse caso um usuário 'X' sempre deve ir para o mesmo fluxo_
        
 - [x] Rollout de features. Utilizado quando criar uma nova funcionalidade e quer ver como os usuários se comportam com ela,
 ou se vai ter algum problema de qualquer tipo, bug, performance, engajamento, na nova funcionalidade.
 
 Mas nada disso vai gerar o resultado que você espera caso não tenha como coletar os dados, então é importante saber qual 
 usuário seguiu e qual não seguiu e ver o resultado de qual resultado. Para isso já tivemos algumas abordagens para coleção,
 a mais simples delas é a própria aplicação dispara um log e se usar Kibana pode criar um dashboard para ver os resultados,
 qual lado foi melhor.
 
 Os testes AB são amplamente utilizados para ver qual alternativa vai ser melhor pra negócio, mas no caso de um bug, que 
 pode ser identificado em um rollout, ele pode representar uma redução nos custos operacionais para empresa.
 
 