---
layout: page-classic-sidebar-left
title: Visão Geral
previous: 
next: /docs/2.1.0/oauth
---
---
BlackBox é a plataforma da [Braspag](http://www.braspag.com.br){:target="_blank} que combina virtualização de pagamentos, carrinho de compras e mídias sociais para proporcionar uma experiência de checkout rápida, segura e ubíqua. 

A plataforma é composta por um conjunto de APIs Web baseadas em arquitetura REST, que trocam dados em formato JSON seguindo fluxos de autorização definidos pelo protocolo OAuth 2, todos padrões amplamente utilizados pelo mercado e suportado pelas comunidades técnicas. 

Internamente, BlackBox foi construido utilizando alguns dos principais produtos da Braspag, como o Cartão Protegido, para tokenização de cartões, e o Pagador, para processamento de pagamentos. 
  
> A plataforma Braspag é certificada PCI DSS 3.2 e ISO 22301
  
As APIs REST permitem integrar a sua aplicação com a plataforma BlackBox. 
  

## Lista completa das APIs
---------------------------

*Versão: **2.1.0***

API | Descrição | Usos comuns
------------ | ------------- | -------------
*Product API* | Gerenciamento de Produtos e SKUs  | Cadastrar produto, cadastrar SKU, alterar preços ou descrição de produto
*Cart API* | Carrinho de Compras social | Criar carrinho, incluir item no carrinho, alterar quantidade de itens no carrinho
*Catalog API* | Catálogo de Produtos e SKUs  | Pesquisar produtos por loja ou categoria
*Checkout API* | Checkout de Carrinho de Compras  | Enviar novo pedido, salvar informações de Checkout para recorrência
*Order API* | Pedidos  | Listar pedidos recebidos por loja, data ou status, confirmar pedido, histórico de pedidos
*Address API* | Endereços de Entrega  | Cadastrar endereço de entrega, remover endereço de entrega
*PaymentMethod API* | Meios de Pagamento  | Cadastrar meio de pagamento, remover meio de pagamento
*Device API* | Dispositivos IoT  | Configurar dispositivo de compras IoT, gerar pedido a partir de dispositivo 
*Account API* | Contas de Usuário  | Registrar novo usuário, alterar senha de usuário
*OAuth2 AS API* | Servidor de Autorização OAuth2  | Obter token de acesso  
  

![BlackBox API]({{ site.url }}/img/docs-blackboxapi-01.png){: .featimg } 