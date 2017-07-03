---
layout: page-classic-sidebar-left
title: Change Status
featimg: MapAntifraud.png
previous: /docs/1.0/linktransaction
next: /docs/1.0/analise
---
---

Service to change the status of transactions in review to accept or reject, available only to the Cybersource provider.  

## Hosts

**Test** https://riskhomolog.braspag.com.br  
**Live** https://risk.braspag.com.br

<a name="contract"></a>
  
## Atributos
-----------------------------------

**Status**{:.custom-attrib} `required`{:.custom-tag} `Guid`{:.custom-tag} `Cybersource`{:.custom-provider-cyber}  
Transaction new status.  
Enum: Accept | Reject  

**Comments**{:.custom-attrib} `optional`{:.custom-tag} `255`{:.custom-tag}.`string`{:.custom-tag} `Cybersource`{:.custom-provider-cyber}  
Comment associated with status update.  

<a style="float: right;" href="#attributes"><i class="fa fa-angle-double-up fa-fw"></i></a>

<a name="http_operations"></a>

## Operação HTTP
-----------------------------------

`PATCH`{:.http-patch} [https://riskhomolog.braspag.com.br/Analysis/{Id}](#http_patch){:.custom-attrib}  
Change status transaction.

<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>

<a name="http-patch"></a>

#### `PATCH`{:.http-patch} Change status transaction.
-------------------------------------------------

**PARÂMETROS:**  

``` csharp
Id: Guid  // Transaction Id Antifraud Gateway
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
    "Status":"Accept",
    "Comments":"Transaction OK after contact client."
}
```

**RESPONSE:**  

- When the transaction is received for processing.
``` http
HTTP/1.1 200 OK
```
```json
{
    "Message": "Change status request successfully received. New status: Accept."
}
```

- When the transaction is not found in the database.
``` http
HTTP/1.1 404 Not found
```
```json
{
    "Message": "The transaction does not exist."
}
```

- When the transaction is not eligible to change status.
``` http
HTTP/1.1 400 Bad Request
```
```json
{
    "Message": "The transaction is not able to change status. Actual status: Reject."
}
```

- When the new status sent is different from Accept or Reject.
``` http
HTTP/1.1 400 Bad Request
```
```json
{
    "Message": "The new status is invalid to update transaction. Accepted status are: 'Accept' or 'Reject'."
}
```

- When the type or size of any field is not sent as specified in the manual.
``` http
HTTP/1.1 400 Bad Request
```
```json
{
    "Message": "The request is invalid.",
    "ModelState": {
        "request.Status": [
            "Error converting value \"Review\" to type 'Antifraude.Domain.Enums.StatusType'. Path 'Status', line 2, position 16."
        ],
        "request.Comments": [
            "The field Comments must be a string or array type with a maximum length of '255'."
        ]
    }
}
```