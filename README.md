# Desafio Back-end Caleta

## Antes de começar

- Inicie criando um repositório publico no seu Github.
- Faça todos os commits referentes a esse desafio no seu repositório.
- Quando terminar, envie o link do repositório ao nosso e-mail.
- Se tiver qualquer dúvida durante o desafio, não hesite em nos perguntar.

## Sobre o ambiente da aplicação

Você pode escolher a linguagem de programação e o framework que preferir para desenvolver a aplicação deste teste. Trabalhe com aquilo que você se sentirá confortável.

---

## Introdução

Neste desafio, você representará um cassino que está integrando na nossa API. Você irá criar uma API para simular a carteira digital deste cassino, que
deverá receber transações do fluxo de jogo dos jogadores. A API deverá ser capaz de gerenciar o saldo de um jogador,
e também permitir apostas e ganhos.

### Requisitos:

As respostas da API devem ser no formato **JSON**.  
Caso containerize a aplicação, deve ser usado o **Docker**. (diferencial)

A **API** deve possuir, no mínimo, os três seguintes endpoints:

#### GET /balance

Este endpoint será utilizado para consultar o saldo da carteira digital de um jogador. Ele deverá receber como parâmetro na URL o ID do jogador (por exemplo, `player=1`).

Por exemplo:

*Requisição:* `GET localhost:8000/balance?player=1`

*Resposta:* `{"player": 1, "balance": 1000}`

exemplo 2:

*Requisição:* `GET localhost:8000/balance/1`

*Resposta:* `{"player": 1, "balance": 1000}`

#### POST /bet

Este endpoint será utilizado para realizar apostas usando a carteira digital de um jogador. Ele deverá receber no corpo da requisição um objeto JSON contendo o ID do jogador e o valor a ser sacado. Como resposta, deverá retornar o saldo atualizado da carteira digital e o ID da transação.

Por exemplo:

*Requisição:* `POST localhost:8000/bet` com body `{"player": 1, "value": 5}`

*Resposta:* `"player": 1, "balance": 995, "txn": 1}`

#### POST /win

Este endpoint será utilizado para realizar ganhos usando a carteira digital de um jogador. Ele deverá receber no corpo da requisição um objeto JSON contendo o ID do jogador e o valor a ser depositado. Como resposta, deverá retornar o saldo atualizado da carteira digital e o ID da transação.

Por exemplo:

*Requisição:* `POST localhost:8000/win` com body `{"player": 1, "value": 1000}`

*Resposta:* `{"player":1, "balance": 1995, "txn": 2}`

---

A Adição do endpoint a seguir contabilizará como um extra, a implementação correta dele contará como um diferencial:

#### POST /rollback

Este endpoint será utilizado para cancelar transações de apostas (BET) realizadas anteriormente. Ele deverá receber no corpo da requisição um objeto JSON contendo o ID do jogador, o ID da transação e o valor da transação. Se a transação existir no banco de dados, o valor sacado deverá ser retornado à carteira digital do jogador.

Por exemplo:

*Requisição:* `POST localhost:8000/rollback` com body `{"player":1, "txn":3, "value":10}`

*Resposta:* `{ "code": "OK", "balance": 1995 }`

Contudo, caso a transação já tenha sido cancelada anteriormente deverá ser retornado a mesma mensagem anterior.

*Requisição:* `POST localhost:8000/rollback` com body `{"player":1, "txn":3, "value":10}`

*Resposta:* `{ "code": "OK", "balance": 1995 }`

Caso a transação referir-se a um depósito, a resposta deverá ser `{"code": "Invalid"}`.

*Requisição:* `POST localhost:8000/rollback` com body `{"player":1, "txn":2, "value":1000}`

*Resposta:* `{ "code": "Invalid" }`

---

## O que será avaliado

- Organização do código;
- Tratamento de erros;
- Persistência dos dados.

## O que não será avaliado

- Segurança da aplicação;
- Autenticação de jogadores.

## Diferenciais

- Uso do Docker;
- Implementação de testes automatizados;
- Documentação da API.

---
