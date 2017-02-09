---
layout: page-classic-sidebar-left
title: SKU
previous: /docs/2.1.0/product
next: 
---
---

SKUs são gerenciados pelo `VENDEDOR`{:.custom-highlight} e representam uma variação específica do [produto]({{ site.baseurl }}{% link docs/2.1.0/product.md %}), como tamanho, cor ou sabor. Cada produto possui ao menos um SKU.  

  
<a name="attributes"></a>
  
## Atributos do objeto
-----------------------------------

**Id**{:.custom-attrib}  `int`{:.custom-tag}  
Identificador do SKU  

**Sku**{:.custom-attrib}  `32`{:.custom-tag}  `string`{:.custom-tag}  
Valor do SKU (Stock Keeping Unit)

**CreatedOn**{:.custom-attrib}  `datetime`{:.custom-tag}  
Data da criação do objeto

**UpdatedOn**{:.custom-attrib}  `datetime`{:.custom-tag}  
Data da última atualização do objeto

**Status**{:.custom-attrib}  `int`{:.custom-tag}  
Status do SKU no estoque. Valores possíveis: (0) em estoque, (1) sem estoque, (2) sob demanda, (3) descontinuado

**Name**{:.custom-attrib}  `256`{:.custom-tag}  `string`{:.custom-tag}  
Nome do SKU

**Description**{:.custom-attrib}  `2048`{:.custom-tag}  `string`{:.custom-tag}  
Descrição do SKU

**ImageUrl**{:.custom-attrib}  `opcional`{:.custom-tag}  `256`{:.custom-tag}  `string`{:.custom-tag}  
URL para a imagem do SKU

**Inventory.UpdatedOn**{:.custom-attrib}  `datetime`{:.custom-tag}  
Data da última atualização do SKU no inventório

**Inventory.Quantity**{:.custom-attrib}  `int`{:.custom-tag}  
Quantidade de itens disponíveis no inventório  

**Inventory.Type**{:.custom-attrib}  `int`{:.custom-tag}  
Tipo de estoque. Valores possíveis: (0) Finito, (1) Infinito  

**Dimensions.Weight**{:.custom-attrib}  `opcional`{:.custom-tag}  `float`{:.custom-tag}  
Peso do item (em gramas)  

**Dimensions.Height**{:.custom-attrib}  `opcional`{:.custom-tag}  `float`{:.custom-tag}  
Altura do item (em centímetros)  

**Dimensions.Lenght**{:.custom-attrib}  `opcional`{:.custom-tag}  `float`{:.custom-tag}  
Comprimento do item (em centímetros)  

**Dimensions.Width**{:.custom-attrib}  `opcional`{:.custom-tag}  `float`{:.custom-tag}  
Largura do item  (em centímetros)  

**ListPrice.CreatedOn**{:.custom-attrib}  `datetime`{:.custom-tag}  
Data de criação do preço de tabela  

**ListPrice.Amount**{:.custom-attrib}  `int`{:.custom-tag}  
Valor em centavos do preço de tabela. Exemplo: 150 (1,50)  

**ListPrice.Currency**{:.custom-attrib}  `string`{:.custom-tag}  
Código ISO 4217 da moeda utilizada no preço de tabela. Exemplos: BRL, USD, EUR  

**SellPrice.CreatedOn**{:.custom-attrib}  `datetime`{:.custom-tag}  
Data de criação do preço de venda  

**SellPrice.Amount**{:.custom-attrib}  `int`{:.custom-tag}  
Valor em centavos do preço de venda. Exemplo: 150 (1,50)  

**SellPrice.Currency**{:.custom-attrib}  `string`{:.custom-tag}  
Código ISO 4217 da moeda utilizada no preço de venda. Exemplos: BRL, USD, EUR  

  
<a style="float: right;" href="#attributes"><i class="fa fa-angle-double-up fa-fw"></i></a>

<a name="http_operations"></a>

## Operações HTTP
-----------------------------------

`POST`{:.http-post} [/api/product/{productId}/sku](#post_sku){:.custom-attrib}  
Criação de SKU para o produto {productId}  

`PUT`{:.http-put} [/api/product/{productId}/sku/{skuId}](#put_sku){:.custom-attrib}  
Atualização de SKU {skuId} para o produto {productId}  

`GET`{:.http-get} [/api/product/{productId}/sku/{skuId}](#getbyid_sku){:.custom-attrib}  
Obtenção de SKU do produto {productId} por Id

`GET`{:.http-get} [/api/product/{productId}/sku](#get_sku){:.custom-attrib}  
Listagem dos SKUs do produto {productId}  

`PUT`{:.http-put} [/api/product/{productId}/sku/{skuId}/inventory](#put_inventory){:.custom-attrib}  
Atualização de estoque para o SKU {skuId} do produto {productId}  

`GET`{:.http-get} [/api/product/{productId}/sku/{skuId}/inventory](#get_inventory){:.custom-attrib}  
Obtenção de estoque do SKU {skuId}  

`PUT`{:.http-put} [/api/product/{productId}/sku/{skuId}/listprice](#put_listprice){:.custom-attrib}  
Atualização do preço de tabela do SKU {skuId}  

`GET`{:.http-get} [/api/product/{productId}/sku/{skuId}/listprice](#get_listprice){:.custom-attrib}  
Obtenção do preço de tabela do SKU {skuId}  

`PUT`{:.http-put} [/api/product/{productId}/sku/{skuId}/sellprice](#put_sellprice){:.custom-attrib}  
Atualização do preço de venda do SKU {skuId}  

`GET`{:.http-get} [/api/product/{productId}/sku/{skuId}/sellprice](#get_sellprice){:.custom-attrib}  
Obtenção do preço de venda do SKU {skuId}  

<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>

<a name="post_sku"></a>

#### `POST`{:.http-post} Criação de SKU  
-----------------------------------------

**PARÂMETROS:**  

``` csharp
productId: int  // id do produto
```

**REQUEST:**  

``` http
POST /api/product/{productId}/sku HTTP/1.1
Host: {blackbox endpoint}
Authorization: Bearer {access_token}
Content-Type: application/json
```

``` json
{
  "Sku": "PROD9999",
  "Name": "SKU COR AZUL",
  "Description": "Descrição do SKU de Produto",
    "Status": 0,
    "Inventory": {
      "Quantity": 10,
      "Type": 0
    },
    "ListPrice": {
      "Currency": "BRL",
      "Amount" : 1000
    },
    "SellPrice": {
      "Currency": "BRL",
      "Amount" : 999
    }
}
```

**RESPONSE:**  

``` http
HTTP/1.1 201 Created
Content-Type: application/json;charset=UTF-8
```
``` json
{
  "Id": 9999,
  "Links": {
    "self": {
      "href": "/api/product/{productId}/sku/9999",
      "method": "GET"
    }
  }
}
```
  
<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>
  
<a name="put_sku"></a>

#### `PUT`{:.http-put} Atualização de SKU 
-------------------------------------------
  
**PARÂMETROS:**  

``` csharp
productId: int  // id do produto
skuId: int  // id do sku
```

**REQUEST:**  

``` http
PUT /api/product/{productId}/sku/{skuId} HTTP/1.1
Host: {blackbox endpoint}
Authorization: Bearer {access_token}
Content-Type: application/json
```

``` json
{
  "Sku": "PROD9999",
  "Name": "SKU COR AZUL ESCURO",
  "Description": "Nova descrição do sku do produto",
  "ImageUrl": "http://path.to/skuimage.png",
  "Status": 0,
  "Dimensions": {
      "Weight": 1.5,
      "Height": 2.0,
      "Lenght": 3.2,
      "Width": 2.0
    }
}
```

**RESPONSE:**  

``` http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
```
``` json
{
  "Id": 9999,
  "Links": {
    "self": {
      "href": "/api/product/{productId}/sku/9999",
      "method": "GET"
    }
  }
}
```
  
<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>
  
<a name="getbyid_sku"></a>

#### `GET`{:.http-get} Obtenção de SKU por Id
-------------------------------------------------

**PARÂMETROS:**  

``` csharp
productId: int  // id do produto  
skuId: int  // id do sku  
```

**REQUEST:**  

``` http
GET /api/product/{productId}/sku/{skuId} HTTP/1.1
Host: {blackbox endpoint}
Authorization: Bearer {access_token}
Content-Type: application/json
```

**RESPONSE:**  

``` http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
```
``` json
{
  "Id": 9999,
  "Sku": "PROD9999",
  "CreatedOn": "2017-02-08T08:53:23.9112582",
  "UpdatedOn": "2017-02-08T08:53:24.292862",
  "Status": 0,
  "Name": "SKU COR AZUL",
  "Description": "Descrição do SKU de Produto",
  "Inventory": {
    "UpdatedOn": "2017-02-08T08:53:23.9112582",
    "Quantity": 10,
    "Type": 0
  },
  "Dimensions": {
      "Weight": 1.5,
      "Height": 2.0,
      "Lenght": 3.2,
      "Width": 2.0
  },
  "ListPrice": {
    "CreatedOn": "2017-02-08T08:53:23.9112582",
    "Amount": 1000,
    "Currency": "BRL"
  },
  "SellPrice": {
    "CreatedOn": "2017-02-08T08:53:23.9112582",
    "Amount": 999,
    "Currency": "BRL"
  }
}
```
  
<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>
  
<a name="get_sku"></a>

#### `GET`{:.http-get} Listagem de SKUs do Produto
---------------------------------------------------
  
**PARÂMETROS:**  

``` csharp
productId: int  // id do produto  
```

**REQUEST:**  

``` http
GET /api/product/{productId}/sku HTTP/1.1
Host: {blackbox endpoint}
Authorization: Bearer {access_token}
Content-Type: application/json
```

**RESPONSE:**  

``` http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
```
``` json
[
  { ... },
  { ... },
  { ... }
]
```
  
<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>
  