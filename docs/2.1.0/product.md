---
layout: page-classic-sidebar-left
title: Produto
previous: /docs/2.1.0/oauth
next: /docs/2.1.0/sku
---
---

Permite ao `VENDEDOR`{:.custom-highlight} cadastrar e gerenciar seus produtos. Cada produto possui uma coleção de [SKUs]({{ site.baseurl }}{% link docs/2.1.0/sku.md %}).  

  
<a name="attributes"></a>
  
## Atributos do objeto
-----------------------------------

**Id**{:.custom-attrib}  `int`{:.custom-tag}  
Identificador do produto.  

**CreatedOn**{:.custom-attrib}  `datetime`{:.custom-tag}  
Data da criação do objeto  

**UpdatedOn**{:.custom-attrib}  `datetime`{:.custom-tag}  
Data da última atualização do objeto

**MerchantId**{:.custom-attrib}  `guid`{:.custom-tag}  
Identificador da loja, composto por 36 caracteres no formato *99999999-9999-9999-9999-999999999999*  

**Name**{:.custom-attrib}  `256`{:.custom-tag}  `string`{:.custom-tag}  
Nome do produto

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

`POST`{:.http-post} [/api/product/](#post_product){:.custom-attrib}  
Criação de produto  

`PUT`{:.http-put} [/api/product/{productId}](#put_product){:.custom-attrib}  
Atualização de produto  

`GET`{:.http-get} [/api/product/{productId}](#getbyid_product){:.custom-attrib}  
Obtenção de Produto por Id  

`GET`{:.http-get} [/api/product/](#get_product){:.custom-attrib}  
Listagem de Produtos  

<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>

<a name="post_product"></a>

#### `POST`{:.http-post} Criação de Produto 
-------------------------------------------

**REQUEST:**  

``` http
POST /api/product/ HTTP/1.1
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
      "href": "/api/product/9999",
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
PUT /api/product/{productId} HTTP/1.1
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
      "href": "/api/product/9999",
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
GET /api/product/{productId} HTTP/1.1
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
GET /api/product/ HTTP/1.1
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
  

