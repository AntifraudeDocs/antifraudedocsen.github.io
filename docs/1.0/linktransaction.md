---
layout: page-classic-sidebar-left
title: Associate transaction Pagador and Antifraud
featimg: MapAntifraud.png
previous: /docs/1.0/retrochargeback
next: /docs/1.0/analise
---
---

Service associating a transaction from Pagador Braspag with the transaction of Antifraud Gateway Braspag.

* The client should make this call when using the flow below:

    - 1º Performs a fraud analysis
    - 2º Performs authorization
    
    - The 3º step should be the call to this service to associate the transaction of the Pagador with the transaction of the Anti-Fraud Gateway.  

<a name="contract"></a>
  
## Atributos
-----------------------------------

**BraspagTransactionId**{:.custom-attrib}  `required`{:.custom-tag} `Guid`{:.custom-tag}  
Transaction identifier in Pagador.  
Ex.: a3e08eb2-2144-4e41-85d4-61f1befc7a3b

<a style="float: right;" href="#attributes"><i class="fa fa-angle-double-up fa-fw"></i></a>

<a name="http_operations"></a>

## Operação HTTP
-----------------------------------

`PATCH`{:.http-patch} [https://riskhomolog.braspag.com.br/Transaction/{Id}](#http_patch){:.custom-attrib}  
Associate transaction Pagador and Antifraud

<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>

<a name="http-patch"></a>

#### `PATCH`{:.http-patch} Associate transaction Pagador and Antifraud 
-------------------------------------------------

**PARÂMETROS:**  

``` csharp
Id: Guid  // Transaction identifier in Antifraud Gateway
```

**REQUEST:**  

``` http
GET https://riskhomolog.braspag.com.br/Transaction/{Id} HTTP/1.1
Host: riskhomolog.braspag.com.br
Authorization: Bearer {access_token}
Content-Type: application/json
```

``` json
{
    "BraspagTransactionId": "a3e08eb2-2144-4e41-85d4-61f1befc7a3b"
}
```

**RESPONSE:**  

- When the Pagador transaction is properly associated with the AntiFraud Gateway transaction  
``` http
HTTP/1.1 200 Ok
```
- When the Pagador transaction is not entered in the requisition  
``` http
HTTP/1.1 400 Not found
```
- When the Antifraud Gateway transaction is not found in the database
``` http
HTTP/1.1 404 Not found
```
- When the Pagador transaction is already associated with another Antifraud Gateway transaction
``` http
HTTP/1.1 409 Conflict
```