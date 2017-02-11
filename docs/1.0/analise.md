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

**MerchantOrderId**{:.custom-attrib}  `required`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Número do Pedido da Loja.  

**TotalOrderAmount**{:.custom-attrib} `required`{:.custom-tag} `long`{:.custom-tag}
Valor total do pedido em centavos.  
Ex.: 150000 (Valor equivalente a R$1.500,00)

**TransactionAmount**{:.custom-attrib} `required`{:.custom-tag} `long`{:.custom-tag}  
Valor da transação financeira a ser analisada.  
Ex.: 123456 Valor equivalente a R$1.234,56)

**Currency**{:.custom-attrib} `required`{:.custom-tag} `3`{:.custom-tag} `string`{:.custom-tag}  
Moeda no formato ISSO 4217  
Ex.: BRL (Real Brasileiro)

**Provider**{:.custom-attrib} `required`{:.custom-tag} `15`{:.custom-tag} `string`{:.custom-tag}  
Nome do Provedor da Solução de Analise de Fraude.  
Ex.: ReDShield

**OrderDate**{:.custom-attrib} `required`{:.custom-tag} `datetime`{:.custom-tag}  
Data do pedido.  
Ex.: 2016-12-09T19:16:38.155Z

**BraspagTransactionId**{:.custom-attrib} `optional`{:.custom-tag} `Guid`{:.custom-tag}  
Id da transação no Pagador da Braspag.  
Ex.: ED3B6646-5B6E-451C-B3CF-4FF5E807CB69

**CardData.Number**{:.custom-attrib}  `required`{:.custom-tag} `19`{:.custom-tag} `string`{:.custom-tag}  
Número do cartão de crédito.

**CardData.Holder**{:.custom-attrib}  `required`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Nome do cartão de crédito.  

**CardData.ExpirationDate**{:.custom-attrib}  `required`{:.custom-tag} `7`{:.custom-tag} `string`{:.custom-tag}  
Data de expiração do cartão de crédito.  
Ex.: 01/2023

**CardData.CVV**{:.custom-attrib}  `required`{:.custom-tag} `4`{:.custom-tag} `string`{:.custom-tag}  
Código de segurança do cartão de crédito.  

**CardData.Brand**{:.custom-attrib}  `required`{:.custom-tag} `10`{:.custom-tag} `string`{:.custom-tag}  
Bandeira do cartão de crédito.  
Ex.: COLOCAR AS BANDEIRAS AQUI

**CardData.EciThreeDSecure**{:.custom-attrib}  `optional`{:.custom-tag} `10`{:.custom-tag} `string`{:.custom-tag}  
DESCREVER ISSO

**BillingData.Street**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Logradouro do endereço de cobrança.  

**BillingData.Number**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Número do endereço de cobrança.

**BillingData.Complement**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Complemento do endereço de cobrança.

**BillingData.Neighborhood**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Bairro do endereço de cobrança.

**BillingData.City**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Cidade do endereço de cobrança.

**BillingData.State**{:.custom-attrib}  `optional`{:.custom-tag} `2`{:.custom-tag} `string`{:.custom-tag}  
Estado do endereço de cobrança.

**BillingData.Country**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
País do endereço de cobrança.

**BillingData.ZipCode**{:.custom-attrib}  `optional`{:.custom-tag} `9`{:.custom-tag} `string`{:.custom-tag}  
Código postal do endereço de cobrança.

**ShippingData.Street**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Logradouro do endereço de entrega.  

**ShippingData.Number**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Número do endereço de entrega.

**ShippingData.Complement**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Complemento do endereço de entrega.

**ShippingData.Neighborhood**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Bairro do endereço de entrega.

**ShippingData.City**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Cidade do endereço de entrega.

**ShippingData.State**{:.custom-attrib}  `optional`{:.custom-tag} `2`{:.custom-tag} `string`{:.custom-tag}  
Estado do endereço de entrega.

**ShippingData.Country**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
País do endereço de entrega.

**ShippingData.ZipCode**{:.custom-attrib}  `optional`{:.custom-tag} `9`{:.custom-tag} `string`{:.custom-tag}  
Código postal do endereço de entrega.

**ShippingData.Email**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
E-mail do responsável a receber o produto no endereço de entrega.

**ShippingData.FirstName**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Primeiro nome do responsável a receber o produto no endereço de entrega.

**ShippingData.MiddleName**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Nome do meio do responsável a receber o produto no endereço de entrega.

**ShippingData.LastName**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Último nome do responsável a receber o produto no endereço de entrega.

**ShippingData.Phone**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Número do telefone do responsável a receber o produto no endereço de entrega.

**ShippingData.WorkPhone**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Número do telefone de trabalho do responsável a receber o produto no endereço de entrega.

**ShippingData.Mobile**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Número do celular do responsável a receber o produto no endereço de entrega.

**ShippingData.ShippingMethod**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Meio de entrega.  
Ex.: None | SameDay | NexDay | TwoDay | ThreeDay | LowCost | CarrierDesignatedByCustomer | Pickup | International | Military | Other

**ShippingData.Comment**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Referências do endereço de entrega.

**CustomerData.MerchantCustomerId**{:.custom-attrib}  `required`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Número do documento de identificação do comprador.  
Ex.: CPF | CNPJ | Passaporte

**CustomerData.FirstName**{:.custom-attrib}  `required`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Primeiro nome do comprador.

**CustomerData.MiddleName**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Nome do meio do comprador.

**CustomerData.LastName**{:.custom-attrib}  `required`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Último nome do comprador do comprador.

**CustomerData.BirthDate**{:.custom-attrib}  `required`{:.custom-tag} `datetime`{:.custom-tag}  
Data de nascimento do comprador.  
Ex.: 1983-10-01T00:00:00.000Z

**CustomerData.Gender**{:.custom-attrib}  `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Sexo do comprador.  
Ex.: VERIFICAR DOMINIO.

**CustomerData.Identity**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Identidade do comprador.

**CustomerData.IdentityType**{:.custom-attrib}  `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Tipo de identidade do comprador.

**CustomerData.Email**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
E-mail do comprador.

**CustomerData.Phone**{:.custom-attrib}  `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Telefone do comprador.

**CustomerData.Ip**{:.custom-attrib}  `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Endereço de IP do comprador.

**CustomerData.Mobile**{:.custom-attrib}  `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Celular do comprador.

**CustomerData.WorkPhone**{:.custom-attrib}  `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Telefone de trabalho do comprador.

**CustomerData.BrowserFingerPrint**{:.custom-attrib}  `required`{:.custom-tag} `6010`{:.custom-tag} `string`{:.custom-tag}  
Impressão digital de dispositivos e geolocalização real do IP do comprador.  
LINK DE COMO INTEGRAR

**CustomerData.Status**{:.custom-attrib}  `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Status do comprador na loja.  
Ex.: NEW | EXISTING

**CartItem[n].ProductName**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Nome do produto.

**CartItem[n].UnitPrice**{:.custom-attrib}  `optional`{:.custom-tag} `long`{:.custom-tag}  
Preço unitário do produto.
Ex.: 10950 (Valor equivalente a R$109,50)

**CartItem[n].MerchantItemId**{:.custom-attrib}  `optional`{:.custom-tag} `36`{:.custom-tag} `string`{:.custom-tag}  
ID do produto na loja.

**CartItem[n].Sku**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Sku do produto.

**CartItem[n].Quantity**{:.custom-attrib}  `optional`{:.custom-tag} `int`{:.custom-tag}  
Quantidade do produto.

**CartItem[n].OriginalPrice**{:.custom-attrib}  `optional`{:.custom-tag} `long`{:.custom-tag}  
Preço original do produto.
Ex.: 11490 (Valor equivalente a R$114,90)

**CartItem[n].GiftMessage**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Mensagem de presente.

**CartItem[n].ShippingInstructions**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Instruções de entrega do produto.

**CartItem[n].ShippingMethod**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Meio entrega do produto.  
Ex.: None | SameDay | NexDay | TwoDay | ThreeDay | LowCost | CarrierDesignatedByCustomer | Pickup | International | Military | Other

**CartItem[n].ShippingTranckingNumber**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Número de ratreamento do produto.

**CustomerConfigurationData.ServiceId**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Id do serviço no sistema de risco. Esse campo geralmente é definido por alguma configuração, mas em algumas situações, você pode querer usar a opção baseada em solicitação dinâmica.
Para o ReDShield isso define qual serviço de triagem de fraude deve ser usado.

**CustomerConfigurationData.RiskAmount**{:.custom-attrib}  `optional`{:.custom-tag} `long`{:.custom-tag}  
Valor de risco do pedido.  
Ex.: 1090 (Valor equivalente a R$10,90)

**CustomerConfigurationData.RiskBrand**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `long`{:.custom-tag}  
Bandeira de risco do pedido.  
VERIFICAR DOMINIO AQUI

**CustomerConfigurationData.Website**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Website da loja.

**CustomerConfigurationData.AccessTokenS**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
DESCIÇÂO

**MerchantDefinedData.Key**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Campo definido junto ao provider.

**MerchantDefinedData.Value**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Campo definido junto ao provider.

**TravelData.CompleteRoute**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Rota completa da viagem. Concatenação das pernas (código do aeroporto) de origem e destino da viagem no formato, ORIG1-DEST1:ORIG2-DEST2.  
Ex.: SFO-JFK:JFK-LHR:LHR-CDG

**TravelData.DepartureTime**{:.custom-attrib}  `optional`{:.custom-tag} `datetime`{:.custom-tag}  
Data de partida do vôo.  
Ex.: 2017-03-01T15:10:00.000Z

**TravelData.JouneyType**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Tipo de viagem.  
Ex.: Só ida | Ida e Volta.  
VERIFICAR DOMINIO

**TravelData.TravelLeg[n].Origin**{:.custom-attrib}  `optional`{:.custom-tag} `5`{:.custom-tag} `string`{:.custom-tag}  
Código do aeroporto de origem da viagem.  
Ex.: SFO

**TravelData.TravelLeg[n].Destination**{:.custom-attrib}  `optional`{:.custom-tag} `5`{:.custom-tag} `string`{:.custom-tag}  
Código do aeroporto de destino da viagem.  
Ex.: JFK

**PassengerData[n].FirstName**{:.custom-attrib} `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Primeiro nome do passageiro.

**PassengerData[n].MiddleName**{:.custom-attrib} `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Nome do meio do passageiro.

**PassengerData[n].LastName**{:.custom-attrib} `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Último nome do comprador do passageiro.

**PassengerData[n].DateOfBirth**{:.custom-attrib} `optional`{:.custom-tag} `datetime`{:.custom-tag}  
Data de nascimento do passageiro.  
Ex.: 1985-07-22T00:00:00.000Z

**PassengerData[n].PassangerId**{:.custom-attrib} `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
ID do passageiro a quem o passageiro foi emitido.  

**PassengerData[n].Status**{:.custom-attrib} `optional`{:.custom-tag} `15`{:.custom-tag} `string`{:.custom-tag}  
Classificação da empresa aérea.
Ex.: Gold | Platinum

**PassengerData[n].PassengerType**{:.custom-attrib} `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Tipo do passageiro.  
Ex.: Adult | Child | Infant | Youth | Student | SeniorCitizen | Military

**PassengerData[n].Email**{:.custom-attrib} `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
E-mail do passageiro.

**PassengerData[n].Phone**{:.custom-attrib} `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Telefone do passageiro.

<a style="float: right;" href="#attributes"><i class="fa fa-angle-double-up fa-fw"></i></a>

<a name="http_operations"></a>

## Operações HTTP
-----------------------------------

`POST`{:.http-post} [/api/analise/](#post_analise){:.custom-attrib}  
Análise da transação  

<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>

<a name="post_analise"></a>

#### `POST`{:.http-post} Análise da Transação 
-------------------------------------------

**REQUEST:**  

``` http
POST /api/analise/ HTTP/1.1
Host: {antifraude endpoint}
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
  
<a name="getbyid_analise"></a>

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
  

