---
title: Documentação da API Kamba

language_tabs: # must be one of https://git.io/vQNgJ
  - curl

toc_footers:
  - <a href='https://developers.usekamba.com'>© 2017 USEKAMBA</a>

includes:
  - errors

search: false
---

# Introdução

Use a API do Kamba para integrar pagamentos online ou presenciais para o seu site, aplicativo ou estabelecimento. 

## Chaves de API 
As suas chaves de API `api_keys` estão disponíveis no painel de controle para desenvolvedores. Use a chave de teste para testar suas integrações e mude para uma chave de produção quando desejar submeter sua integração para um ambiente com clientes reais. 

## SDKs e Bibliotecas 
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

# Autenticação

Use suas credenciais para receber a sua chave de API e segurar os dados da sua aplicação. A primeira coisa que você precisa fazer para conseguir as suas credenciais é criar um identificador comerciante. Cada identificador comerciante possui uma chave de API para produção e uma chave de API para testes. Utilize estas chaves para:

* Selecione a conta comerciante relacionada à você.
* Especifique se você está testando ou trabalhando com pagamentos reais.
* Mostre à API Kamba que é realmente você nas solicitações HTTP ao fazer uso da chave de API.

<aside class="notice">
A chave de API deve ser enviada junto com cada solicitação da API, fornecendo-nos na chamada HTTP no cabeçalho `header` `Authorization`. 
</aside>

É muito importante manter quaisquer chaves de API de em segurança. Nunca compartilhe com terceiros. No entanto, se ocorrer uma situação de que a segurança de uma chave esteja comprometida, você deve rapidamente gerar outra chave de API que automaticamente expira a anterior. Não se esqueça de aplicar esta nova chave nas requisições do seu código. Até que você o faça, suas integrações não irão funcionar.