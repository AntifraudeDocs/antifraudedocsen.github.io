---
layout: page-classic-sidebar-left
title: Report Chargeback
featimg: MapAntifraud.png
previous: /docs/1.0/fingerprint
next: /docs/1.0/linktransaction
---
---

Service to send the transactions to Braspag that have already been analyzed and suffered chargeback by the customers. This information is used to track fraud and ACI / ReD Shield may recommend rules to prevent subsequent fraud attacks.  

Obs.: The service accepts POST request with a maximum of 100 items in the collection.  

## Hosts

**Test** https://riskhomolog.braspag.com.br  
**Live** https://risk.braspag.com.br

<a name="contract"></a>
  
## Contract fields
-----------------------------------

**Id**{:.custom-attrib}  `required`{:.custom-tag} `Guid`{:.custom-tag}  
Transaction identifier in Antifraud Gateway.

**BraspagTransactionId**{:.custom-attrib}  `optional`{:.custom-tag} `Guid`{:.custom-tag}  
Transaction identifier in Pagador.

**ChargebackAmount**{:.custom-attrib} `required`{:.custom-tag} `long`{:.custom-tag}  
Cahargeback amount.  
Ex.: 150000 (Valor equivalente a R$1.500,00)

**ChargebackDate**{:.custom-attrib} `required`{:.custom-tag} `date`{:.custom-tag}  
Date of chargeback confirmation.  
Ex.: 2017-12-02

**ChargebackReasonCode**{:.custom-attrib} `required`{:.custom-tag} `5`{:.custom-tag} `string`{:.custom-tag}  
Chargeback reason code.

**IsFraud**{:.custom-attrib} `required`{:.custom-tag} `bool`{:.custom-tag}  
Flag to identify whether the chargeback was motivated by fraud or not

<a style="float: right;" href="#attributes"><i class="fa fa-angle-double-up fa-fw"></i></a>

<a name="http_operations"></a>

## HTTP Operations
-----------------------------------

`POST`{:.http-post} [https://riskhomolog.braspag.com.br/Chargeback/](#post_retrocbk){:.custom-attrib}  
Report Chargeback  

<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>

<a name="post_retrocbk"></a>

#### `POST`{:.http-post} Report Chargeback
-------------------------------------------

**REQUEST:**  

``` http
POST https://riskhomolog.braspag.com.br/Chargeback/ HTTP/1.1
Host: {antifraude endpoint}
Authorization: Bearer {access_token}
Content-Type: application/json
```

``` json
{
    "Chargebacks":
    [
        {
            "Id" : "fb647240-824f-e711-93ff-000d3ac03bed",
            "BraspagTransactionId": "a3e08eb2-2144-4e41-85d4-61f1befc7a3b",
            "ChargebackAmount" : "1000",
            "ChargebackDate" : "2017-12-02",
            "ChargebackReasonCode" : "1",
            "IsFraud" : "false"
        },
        {
            "Id": "9004ba26-f1f1-e611-9400-005056970d6f",
            "ChargebackAmount": "27580",
            "ChargebackDate": "2017-12-02",
            "ChargebackReasonCode": "54",
            "IsFraud": "true"
        },
        {
            "Id": "4493d42c-8732-4b13-aadc-b07e89732c26",
            "ChargebackAmount": "59960",
            "ChargebackDate": "2017-12-02",
            "ChargebackReasonCode": "54",
            "IsFraud": "true"
        },
        {
            "Id": "22b5e829-edf1-e611-9414-0050569318a7",
            "ChargebackAmount": "150000",
            "ChargebackDate": "2017-12-02",
            "ChargebackReasonCode": "54",
            "IsFraud": "true"
        }
    ]
}
```

**RESPONSE:**  

- When all sent chargeback transactions are processed successfully
``` http
HTTP/1.1 200 Ok
```

- When all sent chargeback transactions are not processed, the transaction identifier with the reason is returned through the "ChargebackProcessingStatus" field.  

    * Reason equal to "Success", the chargeback transaction was successfully processed.  
    * Reason equal to "AlreadyExist," the chargeback transaction is already associated with the original fraud analysis transaction.
    * Reason equal to "Remand", the chargeback transaction should be forwarded.  
    * Reason equal to "NotFound", the chargeback transaction should not be resubmitted because the origin of this linked fraud analysis was not found in the database.  

``` http
HTTP/1.1 300 Multiple Choices
```
``` json
{
    "Chargebacks":
    [
         {
            "Id" : "fb647240-824f-e711-93ff-000d3ac03bed",
            "BraspagTransactionId": "a3e08eb2-2144-4e41-85d4-61f1befc7a3b",
            "ChargebackAmount" : "1000",
            "ChargebackDate" : "2017-12-02",
            "ChargebackReasonCode" : "1",
            "IsFraud" : "false",
            "ChargebackProcessingStatus": "Success"
        },
        {
            "Id": "9004ba26-f1f1-e611-9400-005056970d6f",
            "ChargebackAmount": "27580",
            "ChargebackDate": "2017-12-02",
            "ChargebackReasonCode": "54",
            "IsFraud": "true",
            "ChargebackProcessingStatus": "AlreadyExist"
        },
        {
            "Id": "4493d42c-8732-4b13-aadc-b07e89732c26",
            "ChargebackAmount": "59960",
            "ChargebackDate": "2017-12-02",
            "ChargebackReasonCode": "54",
            "IsFraud": "true",
            "ChargebackProcessingStatus": "Remand"
        },
        {
            "Id": "22b5e829-edf1-e611-9414-0050569318a7",
            "ChargebackAmount": "150000",
            "ChargebackDate": "2017-12-02",
            "ChargebackReasonCode": "54",
            "IsFraud": "true",
            "ChargebackProcessingStatus": "NotFound"
        }
    ]
}
```
