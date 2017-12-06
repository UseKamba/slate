---
title: Documentação da API Kamba

language_tabs: # must be one of https://git.io/vQNgJ
  - curl

toc_footers:
  - <a href='https://developers.usekamba.com'>© 2017 USEKAMBA</a>

includes:

search: false
---

# Introdução

Use a API do Kamba para integrar uma infraestrutura de pagamentos online para o seu site ou aplicativo. 

## Ponto de partida

As URLs bases da API são:

- **Produção:** `https://api.usekamba.com`
- **Testes:** `https://sandbox.usekamba.com`

## Solicitações HTTP

> Exemplo de solicitação POST HTTP.

```json
POST https://api.usekamba.com/private/v1.1/bank_accounts
Content-Type: application/json
Authorization: Token F84222z531Y242909m960

{
  "foo": "bar"
}

... ou ...

GET https://api.usekamba.com/private/v1.1/bank_accounts/707177c3-bf15-4e7e-b37c-55c3898d9bf4
```

Todas as solicitações HTTP devem fornecer no cabeçalho `Authorization: Token CHAVE_API` e `Content-Type: application/json`. O corpo das solicitações e respostas são codificados em JSON.

Solicitações devem ser enviadas sempre usando HTTPS nas URLs.

## Chaves de API 
As suas chaves de API `api_keys` estão disponíveis no painel de controle para desenvolvedores. Use a chave de teste para testar suas integrações e mude para uma chave de produção quando desejar submeter sua integração para um ambiente com clientes reais. 

## Paginação

## Métodos de Pagamento

Kamba está sempre adicionando novos métodos de pagamento. A Kamba API atualmente suporta estes métodos de pagamento:

* Kamba Carteira 
* KambaQR
* Transferência Bancária (Borderaux)
* IBAN
* Pagamentos por Referência Multicaixa

Todos os métodos de pagamento quando permitidos são mostrados para o consumidor. Você pode configurar os métodos de pagamento usando o painel de controle.

## Fluxo de Pagamento 

1. Um consumidor em seu site ou aplicativo decide fazer Checkout.
2. Seu site ou aplicativo cria uma solicitação de pagamento na plataforma Kamba chamando a API Kamba com o valor `amount`, uma descrição de pagamento `description` e uma URL para qual devemos redirecionar o consumidor após o pagamento ser feito. 
3. A API Kamba responde com um único link para pagamento recém-criado `payment_link`. Seu site ou aplicativo armazena o id de solicitação de pagamento `payment_id` e redireciona o consumidor para o Checkout do Kamba. Esta é a URL para a tela de pagamento `checkout` para esse pagamento específico.
4. O consumidor no Checkout, escolhe um método de pagamento e faz o pagamento. Este processo é inteiramente cuidado pela Kamba. Você não precisa fazer nada aqui.
5. Quando o pagamento é feito o Kamba irá redirecionar de volta para o seu site dependendo do estado `status` do pagamento.  

# SDKs e Bibliotecas 
Se possível, seria mais sábio deixar este nível de integração para os nossos SDKs cliente e servidor. Isso permite que você esteja no controle focando na sua lógica de negócios sem reinventar a roda e deixar a infraestrutura de pagamentos por nossa conta.

Os SDKs da API Kamba estão disponíveis para diversas linguagens de programação. Nós fornecemos bibliotecas para a sua loja virtual/e-commerce, seus aplicativos Android ou iOS.

| SDKs para cliente        | SDKs para servidor           | 
| ------------- |:-------------:|
| Android      | Ruby | 
| iOS      | java | 
| JavaScript      | |

<aside class="notice">
Os SDKs para cliente necessitam de autorização. É usado um sistema de chaves de API (cliente-token) - a forma mais flexível de autorização.
</aside>

## Integração Servidor

## Integração Aplicativos

# Autenticação

Para interagir com a API você precisará de chaves de API. A primeira coisa que você deve fazer para conseguir as suas credenciais é criar uma conta comerciante. Cada conta comerciante possui um identificador de comerciante com chaves de API para produção e teste.

* Selecione a conta comerciante relacionada à você.
* Especifique se você está testando ou trabalhando com pagamentos reais ao escolher entre uma chave de API de produção ou de teste.
* Inclua sempre sua chave de API no cabeçalho HTTP `Authorization` dessa forma: `Authorization: Token CHAVE_API`.

<aside class="notice">
É escusado dizer que a chave de API deve substituir CHAVE_API acima. 
</aside>

É muito importante manter quaisquer chaves de API de em segurança. Nunca compartilhe com terceiros. No entanto, se ocorrer uma situação inesperada, as chaves de API devem ser geradas novamente. Não se esqueça de aplicar estas novas chaves no cabeçalho das solicitações HTTP do seu código para suas integrações funcionarem como esperado.

# Saldo da Carteira

# Contas Bancárias

# Métodos de Pagamento

# Solicitações de Pagamento

# Bancos

# Depósitos

# Levantamentos

# Comerciantes

# Transações

> Exemplo do objeto JSON de uma transação.

```json
{
  "id": "a81eda08-d4fe-4dd2-82ee-57203f2d2bbe",
  "intent": "PAY_CONTACT",
  "from": {
      "id": "ze66174f-6041-4b1d-a3eb-08c320e26591",
      "firstname": "Amarildo",
      "lastname": "Lucas",
      "phone_number": "+244924426615",
      "email": "amarildo@hotmail.com",
      "avatar_url": null
  },
  "to": {
      "id": "f840f8c3-5683-487e-8e3e-e0d199c3128c",
      "firstname": "Alexandre",
      "lastname": "Juca",
      "phone_number": "+244912507079",
      "email": "alexandre@hotmail.com",
      "avatar_url": null
  },
  "initial_amount": {
      "total": 3500.00,
      "fee": 0.00
  },
  "amount": {
      "subtotal": 3500.00
  },
  "description": "Dinheiro da parabólica!",
  "status": "PAID",
  "created_at": "2017-11-16T16:23:18.532Z",
  "updated_at": "2017-11-16T16:23:18.585Z",
  "transaction_type": "PAYMENT"
}
```

Uma transação representa o envio de dinheiro entre um remetente `payer` para um destinatário `receiver`. O identificador de uma transação criada com sucesso pertence a ambos. O identificador do remetente `receiver` pode pertencer à um usuário particular ou à um comerciante.

Parâmetros | Descrição
--------- | -----------
id | Identificador único da transação 
intent | Intenção da transação
amount | Valor monetário da transação
currency | Nome da moeda
status | Estado da transação. Ex: `paid`
payer_id | Identificador único do remetente
receiver_id | identificador único do destinatário
description | Descrição da transação
transaction_type | Tipo de transação. Sempre `PAYMENT`
created_at | Data de criação da transação

## Obter uma transação específica

> Exemplo de solicitação HTTP para obter uma transação.

```shell
curl "https://sandbox.usekamba.com/private/v1.1/users/{user_id}/transactions"
  -X GET
  -H "Authorization: Token ZVR4ZwjD2VQbDrDBrAIqqgtt"
```

> O comando acima retorna o objeto JSON a seguir:

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
  "id": "a81eda08-d4fe-4dd2-82ee-57203f2d2bbe",
  "intent": "PAY_CONTACT",
  "from": {
      "id": "ze66174f-6041-4b1d-a3eb-08c320e26591",
      "firstname": "Amarildo",
      "lastname": "Lucas",
      "phone_number": "+244924426615",
      "email": "amarildo@hotmail.com",
      "avatar_url": null
  },
  "to": {
      "id": "f840f8c3-5683-487e-8e3e-e0d199c3128c",
      "firstname": "Alexandre",
      "lastname": "Juca",
      "phone_number": "+244912507079",
      "email": "alexandre@hotmail.com",
      "avatar_url": null
  },
  "initial_amount": {
      "total": 3500.00,
      "fee": 0.00
  },
  "amount": {
      "subtotal": 3500.00
  },
  "description": "Dinheiro da parabólica!",
  "status": "PAID",
  "created_at": "2017-11-16T16:23:18.532Z",
  "updated_at": "2017-11-16T16:23:18.585Z",
  "transaction_type": "PAYMENT"
}
```

Obtem-se uma transação específica através de um `ID` de transação. Este `ID` pertence ao remetente tanto como ao destinatário.

### Solicitação HTTP

- **URL de teste:** `GET https://sandbox.usekamba.com/private/v1.1/users/{user_id}/transactions`
- **URL de produção:** `GET https://api.usekamba.com/private/v1.1/users/{user_id}/transactions`

### Parâmetros para URL

Parâmetros | Descrição
--------- | -----------
user_id | Identificador único do usuário particular iniciando a transação

### Estado HTTP e códigos de erro
Parâmetros | Descrição
--------- | -----------
400 | Transferência falhou
403 | Chave de API não autorizada

## Criar uma transação

> Exemplo de solicitação POST HTTP para obter uma transação.

```shell
curl -X POST "https://sandbox.usekamba.com/private/v1.1/users/{user_id}/transactions" \
  -H "Authorization: Token ZVR4ZwjD2VQbDrDBrAIqqgtt" \
  -d "receiver_id=af724bac-28f9-4edf-a8f5-54a73da235ee" \  
  -d "payer_id=fe99174f-6041-4z1d-a3eb-08c320e26591" \
  -d "amount=3500.00" \
  -d "description=2 pizzas!" \
  -d "intent=PAY_CONTACT" 
```

> O comando acima retorna o objeto JSON a seguir:

```json
HTTP/1.1 201 Created
Content-Type: application/json; charset=utf-8

{
  "id": "a81eda08-d4fe-4dd2-82ee-57203f2d2bbe",
  "intent": "PAY_CONTACT",
  "from": {
      "id": "ze66174f-6041-4b1d-a3eb-08c320e26591",
      "firstname": "Amarildo",
      "lastname": "Lucas",
      "phone_number": "+244924426615",
      "email": "amarildo@hotmail.com",
      "avatar_url": null
  },
  "to": {
      "id": "f840f8c3-5683-487e-8e3e-e0d199c3128c",
      "firstname": "Alexandre",
      "lastname": "Juca",
      "phone_number": "+244912507079",
      "email": "alexandre@hotmail.com",
      "avatar_url": null
  },
  "initial_amount": {
      "total": 3500.00,
      "fee": 0.00
  },
  "amount": {
      "subtotal": 3500.00
  },
  "description": "Dinheiro da parabólica!",
  "status": "PAID",
  "created_at": "2017-11-16T16:23:18.532Z",
  "updated_at": "2017-11-16T16:23:18.585Z",
  "transaction_type": "PAYMENT"
}
```

Envia dinheiro de um remetente para um destinatário.

### Solicitação HTTP

- **URL de teste:** `POST https://sandbox.usekamba.com/private/v1.1/users/{user_id}/transactions`
- **URL de produção:** `POST https://api.usekamba.com/private/v1.1/users/{user_id}/transactions`

### Parâmetros de URL

Parámetros | Descrição
--------- | -----------
user_id | O `ID` do usuário remetente iniciando a transação

### Parâmetros para a solicitação HTTP

Parâmetros | Descrição
--------- | -----------
intent | Intenção da transação
amount | Valor monetário da transação
currency | Nome da moeda
payer_id | Identificador único do remetente
receiver_id | identificador único do destinatário
description | Descrição da transação

### Estado HTTP e códigos de erro
Parâmetros | Descrição
--------- | -----------
400 | Transferência falhou
403 | Chave de API não autorizada