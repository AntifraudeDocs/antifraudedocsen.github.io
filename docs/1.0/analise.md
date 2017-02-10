---
layout: page-classic-sidebar-left
title: Análise
previous: /docs/1.0/autenticacao
next: /docs/1.0/sku
---
---

Esta página descreve os campos do contrato do Antifraude Gateway, além de conter exemplos de requisições HTTP.  

  
<a name="contract"></a>
  
## Campos do Contrato
-----------------------------------

**MerchantOrderId**{:.custom-attrib}  `100`{:.custom-tag}  `string`{:.custom-tag}  
Número do Pedido da Loja.  

**TotalOrderAmount**{:.custom-attrib}  `Int64`{:.custom-tag}  
Valor total do pedido em centavos.  
Ex: 150000 (Valor equivalente a R$1.500,00)

**TransactionAmount**{:.custom-attrib}  `Int64`{:.custom-tag}  
Valor da transação financeira a ser analisada.  
Ex: 123456 Valor equivalente a R$1.234,56)

**Currency**{:.custom-attrib}  `3`{:.custom-tag}  `string`{:.custom-tag}  
Moeda no formato ISSO 4217  
Ex: BRL (Real Brasileiro)

**Provider**{:.custom-attrib}  `15`{:.custom-tag}  `string`{:.custom-tag}  
Nome do Provedor da Solução de Analise de Fraude.  
Ex: Cybersource, Redshield

**Description**{:.custom-attrib}  `2048`{:.custom-tag}  `string`{:.custom-tag}  
Descrição do produto

**IsEnabled**{:.custom-attrib}  `bool`{:.custom-tag}  
Flag que indica se produto está habilitado

**Manufacturer.Name**{:.custom-attrib}  `opcional`{:.custom-tag}  `64`{:.custom-tag}  `string`{:.custom-tag}  
Fabricante do produto

**Manufacturer.Model**{:.custom-attrib}  `opcional`{:.custom-tag}  `64`{:.custom-tag}  `string`{:.custom-tag}  
Modelo do produto  

**Manufacturer.Warranty**{:.custom-attrib}  `opcional`{:.custom-tag}  `int`{:.custom-tag}  
Garantia do produto (em meses)  

**Skus**{:.custom-attrib}  `opcional`{:.custom-tag}  `array`{:.custom-tag}  
Lista de SKUs do produto  
  
<a style="float: right;" href="#attributes"><i class="fa fa-angle-double-up fa-fw"></i></a>

<a name="http_operations"></a>

## Operações HTTP
-----------------------------------

`POST`{:.http-post} [/api/analise/](#post_product){:.custom-attrib}  
Criação de produto  

`PUT`{:.http-put} [/api/analise/{productId}](#put_product){:.custom-attrib}  
Atualização de produto  

`GET`{:.http-get} [/api/analise/{productId}](#getbyid_product){:.custom-attrib}  
Obtenção de Produto por Id  

`GET`{:.http-get} [/api/analise/](#get_product){:.custom-attrib}  
Listagem de Produtos  

<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>

<a name="post_product"></a>

#### `POST`{:.http-post} Criação de Produto 
-------------------------------------------

**REQUEST:**  

``` http
POST /api/analise/ HTTP/1.1
Host: {blackbox endpoint}
Authorization: Bearer {access_token}
Content-Type: application/json
```

``` json
{
  "MerchantId": "99999999-9999-9999-9999-999999999999",
  "Name": "Nome do produto",
  "Description": "Descrição do produto",
  "Manufacturer": {
    "Name": "Fabricante do produto", 
    "Warranty": 12,
    "Model": "MODEL0001"
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
      "href": "/api/analise/9999",
      "method": "GET"
    }
  }
}
```
  
<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>
  
<a name="put_product"></a>

#### `PUT`{:.http-put} Atualização de Produto 
-------------------------------------------
  
**PARÂMETROS:**  

``` csharp
productId: int  // id do produto
```

**REQUEST:**  

``` http
PUT /api/analise/{productId} HTTP/1.1
Host: {blackbox endpoint}
Authorization: Bearer {access_token}
Content-Type: application/json
```

``` json
{
  "MerchantId": "99999999-9999-9999-9999-999999999999",
  "Name": "Nome do produto",
  "Description": "Descrição do produto",
  "Manufacturer": {
    "Name": "Fabricante do produto", 
    "Warranty": 12,  
    "Model": "MODEL0001" 
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
      "href": "/api/analise/9999",
      "method": "GET"
    }
  }
}
```
  
<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>
  
<a name="getbyid_product"></a>

#### `GET`{:.http-get} Obtenção de Produto por Id
-------------------------------------------------

**PARÂMETROS:**  

``` csharp
productId: int  // id do produto
```

**REQUEST:**  

``` http
GET /api/analise/{productId} HTTP/1.1
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
  "CreatedOn": "2017-01-23T09:44:13.3466667",
  "UpdatedOn": "2017-01-23T09:44:13.3466667",
  "MerchantId": "99999999-9999-9999-9999-999999999999",
  "Name": "Nome do produto",
  "Description": "Descrição do produto",
  "Manufacturer": {
    "Name": "Fabricante do produto",
    "Warranty": 12,
    "Model": "MODEL0001"
  },
  "IsEnabled": true,
  "Skus": [
    {
      "Id": 9999999,
      "Sku": "PROD9999",
      "CreatedOn": "2017-01-23T09:44:15.16",
      "UpdatedOn": "2017-01-23T09:44:15.16",
      "Status": 0,
      "Name": "SKU PROD9999",
      "Description": "Descrição do item",
      "Inventory": {
        "UpdatedOn": "2017-01-23T09:44:14.66",
        "Quantity": 100,
        "Type": 0
      },
      "Dimensions": {
        "Weight": 1.0,
        "Height": 2.5,
        "Lenght": 2.5,
        "Width": 10
      },
      "ListPrice": {
        "CreatedOn": "2017-01-23T09:44:13.97",
        "Amount": 10000,
        "Currency": "BRL"
      },
      "SellPrice": {
        "CreatedOn": "2017-01-23T09:44:14.16",
        "Amount": 9000,
        "Currency": "BRL"
      }
    }
  ]
}
```
  
<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>
  
<a name="get_product"></a>

#### `GET`{:.http-get} Listagem de Produtos
-------------------------------------------------

**REQUEST:**  

``` http
GET /api/analise/ HTTP/1.1
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
  

