---
layout: page-classic-sidebar-left
title: Perfis de Usuário
previous: /docs/2.1.0/overview
next: /docs/2.1.0/oauth
---
---

O acesso às APIs REST são restritos de acordo com o perfil que um determinado usuário possui. O perfil representa o papel que o usuário exerce na plataforma.  
  
  
* `Comprador`, é o usuário que consome produtos e serviços, realiza pagamentos;  
* `Vendedor`, é o usuário que fornece produtos e serviços, recebe pagamentos;  
  
> Um usuário pode possuir ambos os perfis
  
## Comprador
----------------------------
  
O `comprador` seleciona produtos para o seu carrinho de compras e realiza checkouts. Seu perfil é composto pelas seguintes informações: 
  
* Identidade digital (contas Facebook e Braspag são suportadas)  
* Ao menos um endereço de entrega  
* Ao menos um meio de pagamento  
  
![Perfil Comprador]({{ site.url }}/img/docs-consumer-01.png){: .centerimg }{:title="Perfil de usuário Comprador"}
  

## Vendedor
----------------------------

O `vendedor` disponibiliza catálogo de produtos e recebe pedidos. Seu perfil é composto pelas seguintes informações: 

* Identidade digital
* Catálogo de Produtos
* Configuração de Loja
* Serviços de Integração (opcional)  
  
![Perfil Vendedor]({{ site.url }}/img/docs-merchant-01.png){: .centerimg }{:title="Perfil de usuário Vendedor"}