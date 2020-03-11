# Teste back-end

Baseado nas regras propostas, a aplicação deverá retornar as mensagens aptas para envio(que não foram bloqueadas) e seu respectivo broker.

A entrada será dada com:

_IDMENSAGEM;DDD;CELULAR;OPERADORA;HORARIO_ENVIO;MENSAGEM_ 

Exemplo:
```
bff58d7b-8b4a-456a-b852-5a3e000c0e63;12;996958849;NEXTEL;21:24:03;sapien sapien non mi integer ac neque duis bibendum
b7e2af69-ce52-4812-adf1-395c8875ad30;69;949360612;CLARO;19:05:21;justo lacinia eget tincidunt eget
e7b87f43-9aa8-414b-9cec-f28e653ac25e;34;990171682;VIVO;18:35:20;dui luctus rutrum nulla tellus in sagittis dui
c04096fe-2878-4485-886b-4a68a259bac5;43;940513739;NEXTEL;14:54:16;nibh fusce lacus purus aliquet at feugiat
d81b2696-8b62-4b8b-af82-586ce0875ebc;21;983522711;TIM;16:42:48;sit amet eros suspendisse accumsan tortor quis turpis sed ante
```
A saída esperada será:

_IDMENSAGEM;IDBROKER_

Exemplo:
```
b7e2af69-ce52-4812-adf1-395c8875ad30;2
e7b87f43-9aa8-414b-9cec-f28e653ac25e;1
c04096fe-2878-4485-886b-4a68a259bac5;3
d81b2696-8b62-4b8b-af82-586ce0875ebc;1
```

## Regras

* mensagens com telefone inválido deverão ser bloqueadas(DDD+NUMERO);
* mensagens que estão na _blacklist_ deverão ser bloqueadas; _(ver blacklist)_
* mensagens para o estado de São Paulo deverão ser bloqueadas;
* mensagens com agendamento após as 19:59:59 deverão ser bloqueadas;
* as mensagens com mais de 140 caracteres deverão ser bloqueadas;
* caso possua mais de uma mensagem para o mesmo destino, apenas a mensagem apta com o menor horário deve ser considerada;
* o id_broker será definido conforme a operadora; _(ver broker x operadora)_

### Broker de envio

Cada broker será responsável pelo envio de algumas operadoras, representado pela tabela abaixo:

| ID_BROKER | OPERADORAS |
|-----------|------------|
|   1       |  VIVO, TIM |
|   2       |  CLARO, OI |
|   3       |  NEXTEL    |

### Consulta de blacklist
```
https://front-test-pg.herokuapp.com/blacklist/:phone
```

### Número de telefone celular válido

```
 DDD + CELULAR
```
* DDD com 2 digitos;
* DDD deve ser válido;
* número celular deve conter 9 dígitos;
* numero celular deve começar com 9;
* o segundo dígito deve ser > 6;

Exemplos:

* 41987563653 - ok
* **00**987563653 - nok
* 419**2**7563653 - nok
* 41**8**87563653 - nok

## O que será avaliado?

* Lógica de programação
* Clean code

## O que esperamos?
* Testes unitários
* Documentação do código
* README do projeto
	* Instruções de como usar;
	* Instruções de como testar;
	* Descrição do que utilizou para desenvolver _(linguagem, SO, editor de texto/IDE, libs e etc)_
