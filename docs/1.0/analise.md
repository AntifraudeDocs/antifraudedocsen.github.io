---
layout: page-classic-sidebar-left
title: Analyze
featimg: MapAntifraud.png
previous: /docs/1.0/autenticacao
next: /docs/1.0/postnotification
---
---

This page describes the fields of the Gateway Anti-Fraud contract, as well as examples of HTTP requests.  

  
<a name="contract"></a>
  
## Contract Fields
-----------------------------------

**MerchantOrderId**{:.custom-attrib}  `required`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Store Order Number.  

**TotalOrderAmount**{:.custom-attrib} `required`{:.custom-tag} `long`{:.custom-tag}  
Total order value in cents.  
Ex.: 150000 (Amount equivalent to $1,500.00).

**TransactionAmount**{:.custom-attrib} `required`{:.custom-tag} `long`{:.custom-tag}  
Value of the financial transaction to be analyzed.  
Ex.: 123456 (Amount equivalent to $1,234.56).

**Currency**{:.custom-attrib} `required`{:.custom-tag} `3`{:.custom-tag} `string`{:.custom-tag}  
Currency. More information at [ISO 4217 - Currency Codes](https://www.iso.org/iso-4217-currency-codes.html)  
Ex.: USD (Dolar) | BRL(Real)

**Provider**{:.custom-attrib} `required`{:.custom-tag} `15`{:.custom-tag} `string`{:.custom-tag}  
Fraud analysis solution provider name.  
Enum: ReDShield

**OrderDate**{:.custom-attrib} `required`{:.custom-tag} `datetime`{:.custom-tag}  
Order date.  
Ex.: 2016-12-09T19:16:38.155Z

**BraspagTransactionId**{:.custom-attrib} `optional`{:.custom-tag} `Guid`{:.custom-tag}  
Transaction Id in Pagador Braspag.  
Ex.: ED3B6646-5B6E-451C-B3CF-4FF5E807CB69  

**SplitingPaymentMethod**{:.custom-attrib} `optional`{:.custom-tag} `23`{:.custom-tag} `string`{:.custom-tag}  
Identifies whether the transaction authorization is with one or two cards or with more than one payment method, for example credit card and bank slip.  
Enum:  
None -> Payment only with a credit card  
CardSplit -> Payment with more than one credit card  
MixedPaymentMethodSplit -> Payment with more than one payment method  

**IsRetryTransaction**{:.custom-attrib} `optional`{:.custom-tag} `bool`{:.custom-tag}  
Identifies that it is a transactional analysis retest. This field must be sent with value equal to TRUE when the return code of the first attempt is equal to BP900, which identifies timeout between Braspag and the Provider. Field to be sent only when Provider equal to ReDShield.  

**CardData.Number**{:.custom-attrib}  `required`{:.custom-tag} `19`{:.custom-tag} `string`{:.custom-tag}  
Credit card number.

**CardData.Holder**{:.custom-attrib}  `required`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Holder name.  

**CardData.ExpirationDate**{:.custom-attrib}  `required`{:.custom-tag} `7`{:.custom-tag} `string`{:.custom-tag}  
Expiration date.  
Ex.: 01/2023

**CardData.CVV**{:.custom-attrib}  `required`{:.custom-tag} `4`{:.custom-tag} `string`{:.custom-tag}  
Security code.  

**CardData.Brand**{:.custom-attrib}  `required`{:.custom-tag} `10`{:.custom-tag} `string`{:.custom-tag}  
Brand.  

**CardData.EciThreeDSecure**{:.custom-attrib}  `optional`{:.custom-tag} `10`{:.custom-tag} `string`{:.custom-tag}  
Authentication ECI(Eletronic Commerce Indicator code) code  

**BillingData.Street**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Street of billing address.  

**BillingData.Number**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Number of billing address.  

**BillingData.Complement**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Complement of billing address.  

**BillingData.Neighborhood**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Neighborhood of billing address.  

**BillingData.City**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
City of billing address.  

**BillingData.State**{:.custom-attrib}  `optional`{:.custom-tag} `2`{:.custom-tag} `string`{:.custom-tag}  
State of billing address.  

**BillingData.Country**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Country of billing address.  

**BillingData.ZipCode**{:.custom-attrib}  `optional`{:.custom-tag} `9`{:.custom-tag} `string`{:.custom-tag}  
Zipcode of billing address.  

**ShippingData.Street**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Street of shipping address.  

**ShippingData.Number**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Number of shipping address.  

**ShippingData.Complement**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Complement of shipping address.  

**ShippingData.Neighborhood**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Neighborhood of shipping address.  

**ShippingData.City**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
City of shipping address.  

**ShippingData.State**{:.custom-attrib}  `optional`{:.custom-tag} `2`{:.custom-tag} `string`{:.custom-tag}  
State of shipping address.  

**ShippingData.Country**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Country of shipping address.  

**ShippingData.ZipCode**{:.custom-attrib}  `optional`{:.custom-tag} `9`{:.custom-tag} `string`{:.custom-tag}  
Zipcode of shipping address.  

**ShippingData.Email**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
E-mail of the person responsible to receive the product in the shipping address.  

**ShippingData.FirstName**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
First name of the person responsible to receive the product in the shipping address.  

**ShippingData.MiddleName**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Middle name of the person responsible to receive the product in the shipping address.  

**ShippingData.LastName**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Last name of the person responsible to receive the product in the shipping address.  

**ShippingData.Phone**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Phonenumber of the person responsible to receive the product in the shipping address.  

**ShippingData.WorkPhone**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Workphone of the person responsible to receive the product in the shipping address.  

**ShippingData.Mobile**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Cellphone of the person responsible to receive the product in the shipping address.  

**ShippingData.ShippingMethod**{:.custom-attrib}  `optional`{:.custom-tag} `27`{:.custom-tag} `string`{:.custom-tag}  
Shipping Method.  
Enum: None | SameDay | NexDay | TwoDay | ThreeDay | LowCost | CarrierDesignatedByCustomer | Pickup | International | Military | Other  

**ShippingData.Comment**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Shipping address references.  

**CustomerData.MerchantCustomerId**{:.custom-attrib}  `required`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Customer document number.  
Ex.: CPF number | CNPJ number | Passaport number

**CustomerData.FirstName**{:.custom-attrib}  `required`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Customer first name.  

**CustomerData.MiddleName**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Customer middle name.  

**CustomerData.LastName**{:.custom-attrib}  `required`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Customer last name.  

**CustomerData.BirthDate**{:.custom-attrib}  `required`{:.custom-tag} `datetime`{:.custom-tag}  
Customer birthdate.  
Ex.: 1983-10-01T00:00:00.000Z

**CustomerData.Gender**{:.custom-attrib}  `optional`{:.custom-tag} `6`{:.custom-tag} `string`{:.custom-tag}  
Customer gender.  
Enum: Male | Female

**CustomerData.Identity**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Customer identity.  

**CustomerData.IdentityType**{:.custom-attrib}  `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Customer identity type.  

**CustomerData.Email**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Customer e-mail.  

**CustomerData.Phone**{:.custom-attrib}  `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Customer phonenumber.  

**CustomerData.Ip**{:.custom-attrib}  `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Customer IP address.  

**CustomerData.Mobile**{:.custom-attrib}  `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Customer cellphone.  

**CustomerData.WorkPhone**{:.custom-attrib}  `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Customer workphone.  

**CustomerData.BrowserFingerPrint**{:.custom-attrib}  `required`{:.custom-tag} `6010`{:.custom-tag} `string`{:.custom-tag}  
Customer device fingerprint.  
[Fingerprint Setup]({{ site.baseurl }}{% link docs/1.0/fingerprint.md %})

**CustomerData.Status**{:.custom-attrib}  `optional`{:.custom-tag} `8`{:.custom-tag} `string`{:.custom-tag}  
Store customer status.  
Ex.: New | Existing

**CartItem[n].ProductName**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Product name.  

**CartItem[n].UnitPrice**{:.custom-attrib}  `optional`{:.custom-tag} `long`{:.custom-tag}  
Product unit price.  
Ex.: 10950 (Amount equivalent to $109.50)

**CartItem[n].MerchantItemId**{:.custom-attrib}  `optional`{:.custom-tag} `36`{:.custom-tag} `string`{:.custom-tag}  
Store product ID.  

**CartItem[n].Sku**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Product SKU.  

**CartItem[n].Quantity**{:.custom-attrib}  `optional`{:.custom-tag} `int`{:.custom-tag}  
Product quantity.  

**CartItem[n].OriginalPrice**{:.custom-attrib}  `optional`{:.custom-tag} `long`{:.custom-tag}  
Product original price.  
Ex.: 11490 (Amount equivalent to $114.90)

**CartItem[n].GiftMessage**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Gift message.  

**CartItem[n].Description**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Product description.  

**CartItem[n].ShippingInstructions**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Product shipping instructions.  

**CartItem[n].ShippingMethod**{:.custom-attrib}  `optional`{:.custom-tag} `27`{:.custom-tag} `string`{:.custom-tag}  
Product shipping method.  
Enum: None | SameDay | NexDay | TwoDay | ThreeDay | LowCost | CarrierDesignatedByCustomer | Pickup | International | Military | Other

**CartItem[n].ShippingTranckingNumber**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Product shipping tracking number.  

**CustomerConfigurationData.ServiceId**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Id of the service in the risk system. This field is usually set up as a configuration, but in some situations you might want to use the dynamic request based option described here.
For the ReD Shield this defines which fraud screening service to use.  

**CustomerConfigurationData.RiskBrand**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `long`{:.custom-tag}  
Brand for the risk request.  

**CustomerConfigurationData.Website**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Store website.  

<!--**CustomerConfigurationData.AccessTokenS**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  -->

**MerchantDefinedData.Key**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Field defined in partnership with provider.  

**MerchantDefinedData.Value**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Field defined in partnership with provider.  

**TravelData.CompleteRoute**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Full trip route. Concatenation of legs (airport code) of origin and destination of the trip in the format, ORIG1-DEST1:ORIG2-DEST2.  
Ex.: SFO-JFK:JFK-LHR:LHR-CDG  

**TravelData.DepartureTime**{:.custom-attrib}  `optional`{:.custom-tag} `datetime`{:.custom-tag}  
Departure date.  
Ex.: 2017-03-01T15:10:00.000Z

**TravelData.JouneyType**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Journey type.  
Enum: OneWayTrip | RoundTrip

**TravelData.TravelLeg[n].Origin**{:.custom-attrib}  `optional`{:.custom-tag} `5`{:.custom-tag} `string`{:.custom-tag}  
Travel origin airport code.  
Ex.: SFO  

**TravelData.TravelLeg[n].Destination**{:.custom-attrib}  `optional`{:.custom-tag} `5`{:.custom-tag} `string`{:.custom-tag}  
Travel destination airport code.  
Ex.: JFK  

**PassengerData[n].FirstName**{:.custom-attrib} `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Passanger last name.  

**PassengerData[n].MiddleName**{:.custom-attrib} `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Passanger middle name.  

**PassengerData[n].LastName**{:.custom-attrib} `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Passanger last name.  

**PassengerData[n].DateOfBirth**{:.custom-attrib} `optional`{:.custom-tag} `datetime`{:.custom-tag}  
Passanger birthdate.  
Ex.: 1985-07-22T00:00:00.000Z  

**PassengerData[n].PassangerId**{:.custom-attrib} `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
ID of the passenger to whom the ticket was issued.  

**PassengerData[n].Status**{:.custom-attrib} `optional`{:.custom-tag} `15`{:.custom-tag} `string`{:.custom-tag}  
Airline classification.  
Enum: Gold | Platinum  

**PassengerData[n].PassengerType**{:.custom-attrib} `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Passenger type.  
Enum: Adult | Child | Infant | Youth | Student | SeniorCitizen | Military

**PassengerData[n].Email**{:.custom-attrib} `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Passenger e-mail.  

**PassengerData[n].Phone**{:.custom-attrib} `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Passenger phone.  

<a style="float: right;" href="#attributes"><i class="fa fa-angle-double-up fa-fw"></i></a>

<a name="http_operations"></a>

## HTTP Operations
-----------------------------------

`POST`{:.http-post} [https://riskhomolog.braspag.com.br/Analysis/](#post_analise){:.custom-attrib}  
Transaction Analysis  

`GET`{:.http-get} [https://riskhomolog.braspag.com.br/Analysis/{Id}](#get_analise){:.custom-attrib}  
Get analysis details  

<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>

<a name="post_analise"></a>

#### `POST`{:.http-post} Transaction Analysis 
-------------------------------------------

**REQUEST:**  

``` http
POST https://riskhomolog.braspag.com.br/Analysis/ HTTP/1.1
Host: {antifraude endpoint}
Authorization: Bearer {access_token}
Content-Type: application/json
```

``` json
{
  "MerchantOrderId": "4493d42c-8732-4b13-aadc-b07e89732c26",
  "TotalOrderAmount": 1500,
  "TransactionAmount": 1000,
  "Currency": "BRL",
  "Provider": "RedShield",
  "OrderDate": "2016-12-09",
  "BraspagTransactionId":"a3e08eb2-2144-4e41-85d4-61f1befc7a3b",
  "SplitingPaymentMethod": "None",
  "IsRetryTransaction": false,
  "Card": {
  "Number" : "4000111231110112",
    "Holder": "Fernando Test",
    "ExpirationDate": "12/2023",
    "Cvv": "999",
    "Brand": "VISA",
    "EciThreeDSecure": "05"
  },
  "Billing": {
    "Street": "AV Marechal Camara",
    "Number": "160",
    "Complement": "Sala 934",
    "Neighborhood": "Castelo",
    "City": "Rio de janeiro",
    "State": "RJ",
    "Country": "BR",
    "ZipCode": "20020060"
  },
  "Shipping": {
        "Street": "Avenida Rio Branco",
        "Number": "30000",
        "Complement": "Complemento",
        "Neighborhood": "Centro",
        "City": "Rio de Janeiro",
        "State": "RJ",
        "Country": "BR",
        "ZipCode": "123456789",
        "Email": "ffigueiredo@braspag.com.br",
        "FirstName": "Fernando",
        "MiddleName": "Souza",
        "LastName": "Figueiredo",
        "ShippingMethod": "SameDay",
        "Phone": "21-21114700",
        "WorkPhone": "21-21114721",
        "Mobile": "21-998765432",
        "Comment": "Em frente ao 322."
    },
  "Customer": {
        "MerchantCustomerId": "10050665740",
        "FirstName": "Fernando",
        "MiddleName": "Souza",
        "LastName": "Figueiredo",
        "BirthDate": "2016-12-09T19:16:38.155Z",
        "Gender": "M",
        "Identity": "38303106171",
        "IdentityType": "1",
        "Email": "ffigueiredo@braspag.com.br",
        "Phone": "12315454-8787878",
        "WorkPhone": "123456789-78945612",
        "Mobile": "987456-123456",
        "Ip": "127.0.0.1",
        "BrowserFingerprint": "04003hQUMXGB0poNf94lis1ztuLYRFk+zJ17aP79a9O8mWOBmEnKs6ziAo94ggAtBvKEN6/FI8Vv2QMAyHLnc295s0Nn8akZzRJtHwsEilYx1P+NzuNQnyK6+7x2OpjJZkl4NlfPt7h9d96X/miNlYT65UIY2PeH7sUAh9vKxMn1nlPu2MJCSi12NBBoiZbfxP1Whlz5wlRFwWJi0FRulruXQQGCQaJkXU7GWWZGI8Ypycnf7F299GIR12G/cdkIMFbm6Yf0/pTJUUz1vNp0X2Zw8QydKgnOIDKXq4HnEqNOos1c6njJgQh/4vXJiqy0MXMQOThNipDmXv9I185O+yC2f3lLEO0Tay66NZEyiLNePemJKSIdwO9O5ZtntuUkG6NTqARuHStXXfwp8cyGF4MPWLuvNvEfRkJupBy3Z8hSEMEK7ZWd2T2HOihQxRh4qp+NANqYKBTl3v6fQJAEKikeSQVeBN8sQqAL0BZFaIMzbrnMivi6m6JRQUIdvEt+MbJEPFc0LjRycC5ApUmJO+Aoo9VKL1B8ftMSQ1iq1uTKn16ZOmDpzZrZhMPbH83aV0rfB2GDXcjpghm9klVFOw7EoYzV7IDBIIRtgqG9KZ+8NH/z6D+YNUMLEUuK1N2ddqKbS5cKs2hplVRjwSv7x8lMXWE7VDaOZWB8+sD1cMLQtEUC0znzxZ4bpRaiSy4dJLxuJpQYAFUrDlfSKRv/eHV3QiboXLuw9Lm6xVBK8ZvpD5d5olGQdc+NgsqjFnAHZUE+OENgY4kVU9wB84+POrI4MkoD4iHJ5a1QF8AZkZDFo1m1h9Bl+J2Ohr6MkBZq8DG5iVaunHfxUdHou5GL7lS1H7r+8ctfDXi8AfOPjzqyODJQ74Aiel35TKTOWG8pq1WO6yzJ1GNmMuMWZBamlGXoG/imnjwHY9HQtQzpGfcm0cR8X2Fd1ngNFGLDGZlWOX0jWtOwU6XVGT37JFD9W/cx4kzI+mPNi65X5WFPYlDG9N0Lbh5nOj3u3DXqRCiKCUrsEkMt8z9fxO9pLLGVQUKIYR2wTw53CiWK96FOpPevDWtH2XR0QkfOd02D73n81x6hEMCy0s3hRLn08Th9FlNHDMJBqLj+Tz8rG2TtNki3mJC7Ass1MT2qnKBI77n6vsQkAp59TfbZm/tBXwAoYdLJXge8F/numhd5AvQ+6I8ZHGJfdN3qWndvJ2I7s5Aeuzb8t9//eNsm73fIa05XreFsNyfOq1vG2COftC6EEsoJWe5h5Nwu1x6PIKuCaWxLY+npfWgM0dwJPmSgPx7TNM31LyVNS65m83pQ+qMTRH6GRVfg7HAcS5fnS/cjdbgHxEkRmgkRq1Qs48sbX9QC8nOTD0ntb6FcJyEOEOVzmJtDqimkzDq+SXR1/63AYe4LEj+ogRgN+Z8HAFhGFzd/m6snVviELfRqJ4LLQIk9Y/fzqnsF6I5OGxfdT2sxxK2Vokpi3jWhCcEknw7dYlHYpOnCHZO7QVgjQTngF2mzKf4GeOF4ECFsWTgLy6HFEitfauYJt1Xh1NfZZerBMwXLFzdhzoTQxGlcXc8lZIoEG1BLYv/ScICf8Ft9PEtpEa+j0cDSlU99UoH2xknwR1W9MRGc5I/euE63/IMJTqguZ3YcnJpjSVnAGSpyz/0gKjypJ3L86rHFRGXt0QbmaXtSl2UmmjI0p0LCCdx7McatCFEVI6FwPpPV0ZSMv/jM75eBid1X/lTV4XNzjowzR/iFlKYMzHZtVO9hCBPKlTwblRXNn4MlvNm/XeSRQ+Mr0YV5w5CL5Z/tGyzqnaLPj/kOVdyfj8r2m5Bcrz4g/ieUIo8qRFv2T2mET46ydqaxi27G4ZYHj7hbiaIqTOxWaE07qMCkJw==",
        "Status": "NEW"
    },
  "CartItems": [
    {
      "ProductName": "Mouse",
      "UnitPrice": "12000",
      "MerchantItemId": "4",
      "Sku": "0",
      "Quantity": 1,
      "OriginalPrice": "12000",
      "GiftMessage": "Te amo!",
      "Description": "Uma description do Mouse",
      "ShippingInstructions": "Proximo ao 546",
      "ShippingMethod": "SameDay",
      "ShippingTrackingNumber": "123456"
    },
    {
      "ProductName": "Teclado",
      "UnitPrice": "96385",
      "MerchantItemId": "3",
      "Sku": "0",
      "Quantity": 1,
      "OriginalPrice": "96385",
      "GiftMessage": "Te odeio!",
      "Description": "Uma description do Teclado",
      "ShippingInstructions": "Proximo ao 123",
      "ShippingMethod": "SameDay",
      "ShippingTrackingNumber": "987654"
    }
  ],
  "CustomConfiguration": {
    "ServiceId": "0",
    "RiskBrand": "0",
    "MerchantWebsite": "www.test.com"
  },
  "MerchantDefinedData": [
    {
      "Key": "Segment",
      "Value": "8999"
    }
  ],
  "Travel": {
    "CompleteRoute": "GIG-CGH-EZE",
    "DepartueTime": "2016-12-10",
    "JouneyType": "JT",
    "TravelLegs": [
      {
        "Origin": "GIG",
        "Destination": "CGH"
      },
      {
        "Origin": "CGH",
        "Destination": "EZE"
      }
    ]
  },
  "Passengers": [
    {
      "FirstName": "Fernando",
      "MiddleName": "Souza",
      "LastName": "Figueiredo",
      "PassengerId": "1",
      "Status": "NEW",
      "PassengerType": "Adult",
      "Email": "ffigueiredo@braspag.com.br",
      "Phone" : "21-21114721",
      "DateOfBirth": "1982-04-30 17:00:00"
    }
  ]
}
```

**RESPONSE:**  

``` http
HTTP/1.1 201 Created
Content-Type: application/json;charset=UTF-8
```
``` json
{
  "Id": "22b5e829-edf1-e611-9414-0050569318a7",
  "AnalysisResult": {
    "Status": "Review",
    "Message": "Payment void and transaction challenged by ReD Shield",
    "ProviderCode": "100.400.148",
    "ProviderTransactionId": "8a8394865a353cc4015a37947c5f7e35",
    "ProviderOrderId": "487931363026"
  },
  "MerchantOrderId": "4493d42c-8732-4b13-aadc-b07e89732c26",
  "TotalOrderAmount": 1500,
  "TransactionAmount": 1000,
  "Currency": "BRL",
  "Provider": "RedShield",
  "OrderDate": "2016-12-09",
  "BraspagTransactionId":"a3e08eb2-2144-4e41-85d4-61f1befc7a3b",
  "SplitingPaymentMethod": "None",
  "IsRetryTransaction": false,
  "Card": {
  "Number" : "4000111231110112",
    "Holder": "Fernando Test",
    "ExpirationDate": "12/2023",
    "Cvv": "999",
    "Brand": "VISA",
    "EciThreeDSecure": "05"
  },
  "Billing": {
    "Street": "AV Marechal Camara",
    "Number": "160",
    "Complement": "Sala 934",
    "Neighborhood": "Castelo",
    "City": "Rio de janeiro",
    "State": "RJ",
    "Country": "BR",
    "ZipCode": "20020060"
  },
  "Shipping": {
        "Street": "Avenida Rio Branco",
        "Number": "30000",
        "Complement": "Complemento",
        "Neighborhood": "Centro",
        "City": "Rio de Janeiro",
        "State": "RJ",
        "Country": "BR",
        "ZipCode": "123456789",
        "Email": "ffigueiredo@braspag.com.br",
        "FirstName": "Fernando",
        "MiddleName": "Souza",
        "LastName": "Figueiredo",
        "ShippingMethod": "SameDay",
        "Phone": "21-21114700",
        "WorkPhone": "21-21114721",
        "Mobile": "21-998765432",
        "Comment": "Em frente ao 322."
    },
  "Customer": {
        "MerchantCustomerId": "10050665740",
        "FirstName": "Fernando",
        "MiddleName": "Souza",
        "LastName": "Figueiredo",
        "BirthDate": "2016-12-09T19:16:38.155Z",
        "Gender": "M",
        "Identity": "38303106171",
        "IdentityType": "1",
        "Email": "ffigueiredo@braspag.com.br",
        "Phone": "21-21114700",
        "WorkPhone": "21-21114721",
        "Mobile": "21-998765432",
        "Ip": "127.0.0.1",
        "BrowserFingerprint": "04003hQUMXGB0poNf94lis1ztuLYRFk+zJ17aP79a9O8mWOBmEnKs6ziAo94ggAtBvKEN6/FI8Vv2QMAyHLnc295s0Nn8akZzRJtHwsEilYx1P+NzuNQnyK6+7x2OpjJZkl4NlfPt7h9d96X/miNlYT65UIY2PeH7sUAh9vKxMn1nlPu2MJCSi12NBBoiZbfxP1Whlz5wlRFwWJi0FRulruXQQGCQaJkXU7GWWZGI8Ypycnf7F299GIR12G/cdkIMFbm6Yf0/pTJUUz1vNp0X2Zw8QydKgnOIDKXq4HnEqNOos1c6njJgQh/4vXJiqy0MXMQOThNipDmXv9I185O+yC2f3lLEO0Tay66NZEyiLNePemJKSIdwO9O5ZtntuUkG6NTqARuHStXXfwp8cyGF4MPWLuvNvEfRkJupBy3Z8hSEMEK7ZWd2T2HOihQxRh4qp+NANqYKBTl3v6fQJAEKikeSQVeBN8sQqAL0BZFaIMzbrnMivi6m6JRQUIdvEt+MbJEPFc0LjRycC5ApUmJO+Aoo9VKL1B8ftMSQ1iq1uTKn16ZOmDpzZrZhMPbH83aV0rfB2GDXcjpghm9klVFOw7EoYzV7IDBIIRtgqG9KZ+8NH/z6D+YNUMLEUuK1N2ddqKbS5cKs2hplVRjwSv7x8lMXWE7VDaOZWB8+sD1cMLQtEUC0znzxZ4bpRaiSy4dJLxuJpQYAFUrDlfSKRv/eHV3QiboXLuw9Lm6xVBK8ZvpD5d5olGQdc+NgsqjFnAHZUE+OENgY4kVU9wB84+POrI4MkoD4iHJ5a1QF8AZkZDFo1m1h9Bl+J2Ohr6MkBZq8DG5iVaunHfxUdHou5GL7lS1H7r+8ctfDXi8AfOPjzqyODJQ74Aiel35TKTOWG8pq1WO6yzJ1GNmMuMWZBamlGXoG/imnjwHY9HQtQzpGfcm0cR8X2Fd1ngNFGLDGZlWOX0jWtOwU6XVGT37JFD9W/cx4kzI+mPNi65X5WFPYlDG9N0Lbh5nOj3u3DXqRCiKCUrsEkMt8z9fxO9pLLGVQUKIYR2wTw53CiWK96FOpPevDWtH2XR0QkfOd02D73n81x6hEMCy0s3hRLn08Th9FlNHDMJBqLj+Tz8rG2TtNki3mJC7Ass1MT2qnKBI77n6vsQkAp59TfbZm/tBXwAoYdLJXge8F/numhd5AvQ+6I8ZHGJfdN3qWndvJ2I7s5Aeuzb8t9//eNsm73fIa05XreFsNyfOq1vG2COftC6EEsoJWe5h5Nwu1x6PIKuCaWxLY+npfWgM0dwJPmSgPx7TNM31LyVNS65m83pQ+qMTRH6GRVfg7HAcS5fnS/cjdbgHxEkRmgkRq1Qs48sbX9QC8nOTD0ntb6FcJyEOEOVzmJtDqimkzDq+SXR1/63AYe4LEj+ogRgN+Z8HAFhGFzd/m6snVviELfRqJ4LLQIk9Y/fzqnsF6I5OGxfdT2sxxK2Vokpi3jWhCcEknw7dYlHYpOnCHZO7QVgjQTngF2mzKf4GeOF4ECFsWTgLy6HFEitfauYJt1Xh1NfZZerBMwXLFzdhzoTQxGlcXc8lZIoEG1BLYv/ScICf8Ft9PEtpEa+j0cDSlU99UoH2xknwR1W9MRGc5I/euE63/IMJTqguZ3YcnJpjSVnAGSpyz/0gKjypJ3L86rHFRGXt0QbmaXtSl2UmmjI0p0LCCdx7McatCFEVI6FwPpPV0ZSMv/jM75eBid1X/lTV4XNzjowzR/iFlKYMzHZtVO9hCBPKlTwblRXNn4MlvNm/XeSRQ+Mr0YV5w5CL5Z/tGyzqnaLPj/kOVdyfj8r2m5Bcrz4g/ieUIo8qRFv2T2mET46ydqaxi27G4ZYHj7hbiaIqTOxWaE07qMCkJw==",
        "Status": "NEW"
    },
  "CartItems": [
    {
      "ProductName": "Mouse",
      "UnitPrice": "12000",
      "MerchantItemId": "4",
      "Sku": "0",
      "Quantity": 1,
      "OriginalPrice": "12000",
      "GiftMessage": "Te amo!",
      "Description": "Uma description do Mouse",
      "ShippingInstructions": "Proximo ao 546",
      "ShippingMethod": "SameDay",
      "ShippingTrackingNumber": "123456"
    },
    {
      "ProductName": "Teclado",
      "UnitPrice": "96385",
      "MerchantItemId": "3",
      "Sku": "0",
      "Quantity": 1,
      "OriginalPrice": "96385",
      "GiftMessage": "Te odeio!",
      "Description": "Uma description do Teclado",
      "ShippingInstructions": "Proximo ao 123",
      "ShippingMethod": "SameDay",
      "ShippingTrackingNumber": "987654"
    }
  ],
  "CustomConfiguration": {
    "ServiceId": "0",
    "RiskBrand": "0",
    "MerchantWebsite": "www.test.com"
  },
  "MerchantDefinedData": [
    {
      "Key": "Segment",
      "Value": "8999"
    }
  ],
  "Travel": {
    "CompleteRoute": "GIG-CGH-EZE",
    "DepartueTime": "2016-12-10",
    "JouneyType": "JT",
    "TravelLegs": [
      {
        "Origin": "GIG",
        "Destination": "CGH"
      },
      {
        "Origin": "CGH",
        "Destination": "EZE"
      }
    ]
  },
  "Passengers": [
    {
      "FirstName": "Fernando",
      "MiddleName": "Souza",
      "LastName": "Figueiredo",
      "PassengerId": "1",
      "Status": "NEW",
      "PassengerType": "Adult",
      "Email": "ffigueiredo@braspag.com.br",
      "Phone": "21-21114700",
      "DateOfBirth": "1982-04-30 17:00:00"
    }
  ]
}
```
  
<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>
  
<a name="get_analise"></a>

#### `GET`{:.http-get} Get analysis details
-------------------------------------------------

**PARÂMETROS:**  

``` csharp
Id: Guid  // Transaction ID
```

**REQUEST:**  

``` http
GET https://riskhomolog.braspag.com.br/Analysis/{Id} HTTP/1.1
Host: riskhomolog.braspag.com.br
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
  "AnalysisResult": {
    "Id": "2ab5e829-edf1-e611-9414-0050569318a7",
    "CreatedDate": "2017-02-13T11:06:04.98",
    "ProviderCode": "100.400.148",
    "Message": "Payment void and transaction challenged by ReD Shield",
    "ProviderOrderId": "487931363026"
  },
  "Id": "22b5e829-edf1-e611-9414-0050569318a7",
  "CreatedDate": "2017-02-13T11:05:57.8876743",
  "OrderDate": "2016-12-09T00:00:00",
  "Status": 2,
  "Provider": 1,
  "MerchantId": "51dd5477-f8c1-428d-a9fd-5d2faf40c25c",
  "TotalOrderAmount": 1500,
  "TransactionAmount": 1000,
  "MerchantOrderId": "4493d42c-8732-4b13-aadc-b07e89732c26",
  "Currency": "BRL",
  "ProviderTransactionId": "8a8394865a353cc4015a37947c5f7e35",
  "SplitingPaymentMethod": "None",
  "IsRetryTransaction": false
}
```
  
<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>
  

