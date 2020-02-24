## Meu Setup Ubuntu

Eu já perdi as contas de quantas vezes eu já formatei o Ubuntu e ao longo do tempo eu fui esquecendo o que eu tinha e era legal.
Então um colega de trabalho me mostrou o repositório que ele tinha para o Fedora, e eu decidi fazer mais ou menos a mesma coisa para
o Ubuntu . Primeira coisa eu gostava muito do Fedora mas como estava querendo começar a fazer streaming de código ele não comportou 
muito bem, com isso, voltei pra o Ubuntu.

A idéia é muito simples e fica todo nesse repositório [luizleite/ubuntu-setup](https://github.com/luizleite-hotmart/ubuntu-setup), 
dentro do setup existem  vários executaveis do seguinte tipo:

 1 - Comando para atualizar o ubuntu 
```bash
sudo apt update -y
```

E a partir de agora, tenho 11 comandos para retornar com a configuração que eu tinha antes.
_Ponto de atenção!!!_ Para voltar a configuração que você tinha é sempre bom criar um novo após cada instalação.

O que faço hoje em dia é ver como faz a instalação de alguma software e jogar em um arquivo novo, para facilitar esse processo, eu 
coloquei um comando new-command.sh em que você pode executar::

`./new-command.sh new_command_name`

O comando acima vai criar um arquivo executável com o nome _new_command_name_ , no qual você pode colocar os passos que você quer que rodem.

Agora o que o comando tem que executar depende do que vocês querem, a ultima instalação que fiz foi do Postman, nele um simples `snap install postman` já resolveu.
Lembrando que o intenção não era criar comandos absurdos, e sim, não deixar nenhuma instalação de fora que eu já tinha, e esse problema resolveu.

