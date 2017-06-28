---
layout: page-classic-sidebar-left
title: Analyze
featimg: MapAntifraud.png
previous: /docs/1.0/autenticacao
next: /docs/1.0/postnotification
---
---

This page describes the fields of the Gateway Anti-Fraud contract, as well as examples of HTTP requests.  

## Hosts

**Test** https://riskhomolog.braspag.com.br  
**Live** https://risk.braspag.com.br

<a name="contract"></a>
  
## Contract Fields
-----------------------------------

**MerchantOrderId**{:.custom-attrib}  `required`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Merchant Order Number.  

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

**OrderDate**{:.custom-attrib} `default = DateTime.Now`{:.custom-tag} `optional`{:.custom-tag} `datetime`{:.custom-tag}  
Order date.  
Ex.: 2016-12-09T19:16:38.155Z

**BraspagTransactionId**{:.custom-attrib} `optional`{:.custom-tag} `Guid`{:.custom-tag}  
Transaction Id in Pagador Braspag.  
Ex.: ED3B6646-5B6E-451C-B3CF-4FF5E807CB69  
Note: If the flow implemented to your business is the first call to make the fraud analysis through the Gateway Anti-Fraud and the second is the authorization through the Pagador, make a third call so that the transactions of the Gateway Anti-Fraud and Pagador are linked. For more details access: [Associate transaction Pagador and Antifraud]({{ site.baseurl }}{% link docs/1.0/linktransaction.md %})  

**SplitingPaymentMethod**{:.custom-attrib} `default = None`{:.custom-tag} `optional`{:.custom-tag} `23`{:.custom-tag} `string`{:.custom-tag}  
Identifies whether the transaction authorization is with one or two cards or with more than one payment method, for example credit card and bank slip.  
Enum:  
None -> Payment only with a credit card  
CardSplit -> Payment with more than one credit card  
MixedPaymentMethodSplit -> Payment with more than one payment method  

**IsRetryTransaction**{:.custom-attrib} `default = false`{:.custom-tag} `optional`{:.custom-tag} `bool`{:.custom-tag}  
Identifies that it is a transactional analysis retest. This field must be sent with value equal to TRUE when the return code of the first attempt is equal to BP900, which identifies timeout between Braspag and the Provider. Field to be sent only when Provider equal to ReDShield.  

**Card.Number**{:.custom-attrib} `required`{:.custom-tag} `19`{:.custom-tag} `string`{:.custom-tag}  
Credit card number.

**Card.Holder**{:.custom-attrib} `required`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Holder name.  

**Card.ExpirationDate**{:.custom-attrib} `required`{:.custom-tag} `7`{:.custom-tag} `string`{:.custom-tag}  
Expiration date.  
Ex.: 01/2023

**Card.CVV**{:.custom-attrib} `required`{:.custom-tag} `4`{:.custom-tag} `string`{:.custom-tag}  
Security code.  

**Card.Brand**{:.custom-attrib} `required`{:.custom-tag} `10`{:.custom-tag} `string`{:.custom-tag}  
Brand.  
Supported brands: Amex | Diners | Discover | JCB | Master | Dankort | Cartebleue | Maestro | Visa | Elo | Hipercard  

**Card.EciThreeDSecure**{:.custom-attrib} `optional`{:.custom-tag} `1`{:.custom-tag} `string`{:.custom-tag}  
Authentication ECI(Eletronic Commerce Indicator code) code  

**Card.Token**{:.custom-attrib}  `optional`{:.custom-tag} `Guid`{:.custom-tag}  
Credit card identifier saved on the Cartão Protegido.  
Note.: This field can be sent in place of the fields **Card.Number, Card.Holder, Card.ExpirationDate**, making them as well as not mandatory. The system will consume the Cartão Protegido by sending this field to fill the above.  

**Card.Alias**{:.custom-attrib}  `optional`{:.custom-tag} `64`{:.custom-tag} `string`{:.custom-tag}  
Credit card alias saved on the Cartão Protegido.  
Note.: This field can be sent in the fraud analysis when you want to save a card to the Cartão Protegido together with the **Card.Save** field equal to TRUE.  
Note2.: This field can be sent in place of the fields **Card.Number, Card.Holder, Card.ExpirationDate**, making them as well as not mandatory. The system will consume the Cartão Protegido by sending this field to fill the above.  
Note3.: This field loses priority if the **Card.Token** field is also sent.  

**Card.Save**{:.custom-attrib} `default = false`{:.custom-tag} `optional`{:.custom-tag} `bool`{:.custom-tag}  
Indicates whether credit card data will be stored on the Cartão Protegido. The Token generated on the Cartão Protegido platform associated with the credit card data, will return in the response of the fraud analysis through **Card.Token** field.  
Note.: The following fields are saved on the Cartão Protegido: **Card.Number, Card.Holder, Card.ExpirationDate**.  
Note2.: The action of saving the data of the credit card will only be made if the merchant has the product Cartão Protegido hired.  

**Billing.Street**{:.custom-attrib} `optional`{:.custom-tag} `24`{:.custom-tag} `string`{:.custom-tag}  
Street of billing address.  

**Billing.Number**{:.custom-attrib}  `optional`{:.custom-tag} `5`{:.custom-tag} `string`{:.custom-tag}  
Number of billing address.  

**Billing.Complement**{:.custom-attrib}  `optional`{:.custom-tag} `14`{:.custom-tag} `string`{:.custom-tag}  
Complement of billing address.  

**Billing.Neighborhood**{:.custom-attrib}  `optional`{:.custom-tag} `15`{:.custom-tag} `string`{:.custom-tag}  
Neighborhood of billing address.  

**Billing.City**{:.custom-attrib}  `optional`{:.custom-tag} `20`{:.custom-tag} `string`{:.custom-tag}  
City of billing address.  

**Billing.State**{:.custom-attrib}  `optional`{:.custom-tag} `2`{:.custom-tag} `string`{:.custom-tag}  
State of billing address.  

**Billing.Country**{:.custom-attrib}  `optional`{:.custom-tag} `2`{:.custom-tag} `string`{:.custom-tag}  
Country of billing address.  
More details [ISO 2-Digit Alpha Country Code](https://www.iso.org/obp/ui)

**Billing.ZipCode**{:.custom-attrib}  `optional`{:.custom-tag} `9`{:.custom-tag} `string`{:.custom-tag}  
Zipcode of billing address.  

**Shipping.Street**{:.custom-attrib}  `optional`{:.custom-tag} `24`{:.custom-tag} `string`{:.custom-tag}  
Street of shipping address.  

**Shipping.Number**{:.custom-attrib}  `optional`{:.custom-tag} `5`{:.custom-tag} `string`{:.custom-tag}  
Number of shipping address.  

**Shipping.Complement**{:.custom-attrib}  `optional`{:.custom-tag} `14`{:.custom-tag} `string`{:.custom-tag}  
Complement of shipping address.  

**Shipping.Neighborhood**{:.custom-attrib}  `optional`{:.custom-tag} `15`{:.custom-tag} `string`{:.custom-tag}  
Neighborhood of shipping address.  

**Shipping.City**{:.custom-attrib}  `optional`{:.custom-tag} `20`{:.custom-tag} `string`{:.custom-tag}  
City of shipping address.  

**Shipping.State**{:.custom-attrib}  `optional`{:.custom-tag} `2`{:.custom-tag} `string`{:.custom-tag}  
State of shipping address.  

**Shipping.Country**{:.custom-attrib}  `optional`{:.custom-tag} `2`{:.custom-tag} `string`{:.custom-tag}  
Country of shipping address.  
More details [ISO 2-Digit Alpha Country Code](https://www.iso.org/obp/ui)

**Shipping.ZipCode**{:.custom-attrib}  `optional`{:.custom-tag} `9`{:.custom-tag} `string`{:.custom-tag}  
Zipcode of shipping address.  

**Shipping.Email**{:.custom-attrib}  `optional`{:.custom-tag} `60`{:.custom-tag} `string`{:.custom-tag}  
E-mail of the person responsible to receive the product in the shipping address.  

**Shipping.FirstName**{:.custom-attrib}  `optional`{:.custom-tag} `30`{:.custom-tag} `string`{:.custom-tag}  
First name of the person responsible to receive the product in the shipping address.  

**Shipping.MiddleName**{:.custom-attrib}  `optional`{:.custom-tag} `1`{:.custom-tag} `string`{:.custom-tag}  
Middle name of the person responsible to receive the product in the shipping address.  

**Shipping.LastName**{:.custom-attrib}  `optional`{:.custom-tag} `30`{:.custom-tag} `string`{:.custom-tag}  
Last name of the person responsible to receive the product in the shipping address.  

**ShippingData.Phone**{:.custom-attrib}  `optional`{:.custom-tag} `19`{:.custom-tag} `string`{:.custom-tag}  
Phonenumber of the person responsible to receive the product in the shipping address.  
Ex.: 552121114700  
55 = Country code  
21 = State code  
21114700 = Phonenumber  

**ShippingData.WorkPhone**{:.custom-attrib}  `optional`{:.custom-tag} `19`{:.custom-tag} `string`{:.custom-tag}  
Workphone of the person responsible to receive the product in the shipping address.  
Ex.: 552121114700  
55 = Country code  
21 = State code  
21114701 = Phonenumber  

**ShippingData.Mobile**{:.custom-attrib}  `optional`{:.custom-tag} `19`{:.custom-tag} `string`{:.custom-tag}  
Cellphone of the person responsible to receive the product in the shipping address.  
Ex.: 5521988776655  
55 = Country code  
21 = State code  
988776655 = Cellphone 

**Shipping.ShippingMethod**{:.custom-attrib}  `optional`{:.custom-tag} `27`{:.custom-tag} `string`{:.custom-tag}  
Shipping Method.  
Enum:  
SameDay = Same day delivery method  
NextDay = Delivery method the next day  
TwoDay = Delivery method in two days  
ThreeDay = Delivery method in three days  
LowCost = Low cost delivery method  
Pickup = Pickup store  
CarrierDesignatedByCustomer = Customer designated delivery method  
International = International delivery method  
Military = Military delivery method  
Other = Another type of delivery method  
None = No delivery method, because it is a service or subscription  

**Shipping.Comment**{:.custom-attrib}  `optional`{:.custom-tag} `160`{:.custom-tag} `string`{:.custom-tag}  
Shipping address references.  

**Customer.MerchantCustomerId**{:.custom-attrib}  `required`{:.custom-tag} `16`{:.custom-tag} `string`{:.custom-tag}  
Customer document number.  
Ex.: CPF number | CNPJ number | Passaport number

**Customer.FirstName**{:.custom-attrib}  `required`{:.custom-tag} `30`{:.custom-tag} `string`{:.custom-tag}  
Customer first name.  

**Customer.MiddleName**{:.custom-attrib}  `optional`{:.custom-tag} `1`{:.custom-tag} `string`{:.custom-tag}  
Customer middle name.  

**Customer.LastName**{:.custom-attrib}  `required`{:.custom-tag} `30`{:.custom-tag} `string`{:.custom-tag}  
Customer last name.  

**Customer.BirthDate**{:.custom-attrib}  `required`{:.custom-tag} `date`{:.custom-tag}  
Customer birthdate.  
Ex.: 1983-10-01

**Customer.Gender**{:.custom-attrib}  `optional`{:.custom-tag} `6`{:.custom-tag} `string`{:.custom-tag}  
Customer gender.  
Enum: Male | Female

<!--**Customer.Identity**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Customer identity.  

**Customer.IdentityType**{:.custom-attrib}  `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Customer identity type.  -->

**CustomerData.Email**{:.custom-attrib}  `optional`{:.custom-tag} `60`{:.custom-tag} `string`{:.custom-tag}  
Customer e-mail.  

**CustomerData.Phone**{:.custom-attrib}  `optional`{:.custom-tag} `19`{:.custom-tag} `string`{:.custom-tag}  
Customer phonenumber.  
Ex.: 552121114700  
55 = Country code  
21 = State code  
21114700 = Phonenumber  

**CustomerData.Ip**{:.custom-attrib}  `optional`{:.custom-tag} `15`{:.custom-tag} `string`{:.custom-tag}  
Customer IP address.  

**CustomerData.Mobile**{:.custom-attrib}  `optional`{:.custom-tag} `19`{:.custom-tag} `string`{:.custom-tag}  
Customer cellphone.  
Ex.: 5521988776655  
55 = Country code  
21 = State code  
988776655 = Cellphone 

**Customer.WorkPhone**{:.custom-attrib}  `optional`{:.custom-tag} `19`{:.custom-tag} `string`{:.custom-tag}  
Customer workphone.  
Ex.: 552121114700  
55 = Country code  
21 = State code  
21114701 = Phonenumber  

**CustomerData.BrowserFingerPrint**{:.custom-attrib}  `required`{:.custom-tag} `6010`{:.custom-tag} `string`{:.custom-tag}  
Customer device fingerprint.  
[Fingerprint Setup]({{ site.baseurl }}{% link docs/1.0/fingerprint.md %})

**Customer.Status**{:.custom-attrib}  `optional`{:.custom-tag} `8`{:.custom-tag} `string`{:.custom-tag}  
Merchant customer status.  
Ex.: New | Existing

**CartItem[n].ProductName**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Product name.  

**CartItem[n].UnitPrice**{:.custom-attrib}  `optional`{:.custom-tag} `long`{:.custom-tag}  
Product unit price.  
Ex.: 10950 (Amount equivalent to $109.50)

**CartItem[n].MerchantItemId**{:.custom-attrib}  `optional`{:.custom-tag} `30`{:.custom-tag} `string`{:.custom-tag}  
Merchant product ID.  

**CartItem[n].Sku**{:.custom-attrib}  `optional`{:.custom-tag} `12`{:.custom-tag} `string`{:.custom-tag}  
Product SKU.  

**CartItem[n].Quantity**{:.custom-attrib}  `optional`{:.custom-tag} `int`{:.custom-tag}  
Product quantity.  

**CartItem[n].OriginalPrice**{:.custom-attrib}  `optional`{:.custom-tag} `long`{:.custom-tag}  
Product original price.  
Ex.: 11490 (Amount equivalent to $114.90)

**CartItem[n].GiftMessage**{:.custom-attrib}  `optional`{:.custom-tag} `160`{:.custom-tag} `string`{:.custom-tag}  
Gift message.  

**CartItem[n].Description**{:.custom-attrib}  `optional`{:.custom-tag} `76`{:.custom-tag} `string`{:.custom-tag}  
Product description.  

**CartItem[n].ShippingInstructions**{:.custom-attrib}  `optional`{:.custom-tag} `160`{:.custom-tag} `string`{:.custom-tag}  
Product shipping instructions.  

**CartItem[n].ShippingMethod**{:.custom-attrib}  `optional`{:.custom-tag} `27`{:.custom-tag} `string`{:.custom-tag}  
Product shipping method.  
Enum:  
SameDay = Same day delivery method  
NextDay = Delivery method the next day  
TwoDay = Delivery method in two days  
ThreeDay = Delivery method in three days  
LowCost = Low cost delivery method  
Pickup = Pickup store  
CarrierDesignatedByCustomer = Customer designated delivery method  
International = International delivery method  
Military = Military delivery method  
Other = Another type of delivery method  
None = No delivery method, because it is a service or subscription  

**CartItem[n].ShippingTranckingNumber**{:.custom-attrib}  `optional`{:.custom-tag} `19`{:.custom-tag} `string`{:.custom-tag}  
Product shipping tracking number.  

**CartItem[n].Passenger.FirstName**{:.custom-attrib} `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Passanger last name.  

**CartItem[n].Passenger.MiddleName**{:.custom-attrib} `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Passanger middle name.  

**CartItem[n].Passenger.LastName**{:.custom-attrib} `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Passanger last name.  

**CartItem[n].Passenger.DateOfBirth**{:.custom-attrib} `optional`{:.custom-tag} `date`{:.custom-tag}  
Passanger birthdate.  
Ex.: 1985-07-22  

**CartItem[n].Passenger.PassangerId**{:.custom-attrib} `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
ID of the passenger to whom the ticket was issued.  

**CartItem[n].Passenger.Status**{:.custom-attrib} `optional`{:.custom-tag} `15`{:.custom-tag} `string`{:.custom-tag}  
Airline classification.  
Enum: Gold | Platinum  

**CartItem[n].Passenger.PassengerType**{:.custom-attrib} `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Passenger type.  
Enum: Adult | Child | Infant | Youth | Student | SeniorCitizen | Military

**CartItem[n].Passenger.Email**{:.custom-attrib} `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Passenger e-mail.  

**CartItem[n].Passenger.Phone**{:.custom-attrib} `optional`{:.custom-tag} `35`{:.custom-tag} `string`{:.custom-tag}  
Passenger phone.  
Ex.: 552121114700  
55 = Country code  
21 = State code  
21114700 = Phonenumber  

<!--**CustomerConfigurationData.ServiceId**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `string`{:.custom-tag}  
Id of the service in the risk system. This field is usually set up as a configuration, but in some situations you might want to use the dynamic request based option described here.
For the ReD Shield this defines which fraud screening service to use.  -->

<!--**CustomerConfigurationData.RiskBrand**{:.custom-attrib}  `optional`{:.custom-tag} `50`{:.custom-tag} `long`{:.custom-tag}  
Brand for the risk request.  -->

**CustomerConfigurationData.Website**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Merchant website.  

<!--**CustomerConfigurationData.AccessTokenS**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  -->

**MerchantDefinedData.Key**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Field defined in partnership with provider.  

**MerchantDefinedData.Value**{:.custom-attrib}  `optional`{:.custom-tag} `255`{:.custom-tag} `string`{:.custom-tag}  
Field defined in partnership with provider.  

Note: Among 15 fields available for customization, 5 are 256 alphanumeric characters and 10 are alphanumeric characters in size.  
Note2.: There are already 2 fields beyond the 15 available, which the merchant can send, which are:  
      - Segment = Merchant Segment Code (MCC). If it fits in more than one segment, send the code of the main segment that the merchant operates.  
      - MerchantId = Merchant identifier in the shopkeeper. This identify is not the merchant identifier in the anti-fraud at Braspag. Example of sending, when the merchant works with marketplace, where you can send the identifier of the selling merchant (Seller).  

**Travel.CompleteRoute**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Full trip route. Concatenation of legs (airport code) of origin and destination of the trip in the format, ORIG1-DEST1:ORIG2-DEST2.  
Ex.: SFO-JFK:JFK-LHR:LHR-CDG  

**Travel.DepartureTime**{:.custom-attrib}  `optional`{:.custom-tag} `datetime`{:.custom-tag}  
Departure date.  
Ex.: 2017-03-01T15:10:00.000Z  

**Travel.JourneyType**{:.custom-attrib}  `optional`{:.custom-tag} `100`{:.custom-tag} `string`{:.custom-tag}  
Journey type.  
Enum: OneWayTrip | RoundTrip

**Travel.TravelLeg[n].Origin**{:.custom-attrib}  `optional`{:.custom-tag} `5`{:.custom-tag} `string`{:.custom-tag}  
Travel origin airport code.  
Ex.: SFO  

**Travel.TravelLeg[n].Destination**{:.custom-attrib}  `optional`{:.custom-tag} `5`{:.custom-tag} `string`{:.custom-tag}  
Travel destination airport code.  
Ex.: JFK  

<a style="float: right;" href="#attributes"><i class="fa fa-angle-double-up fa-fw"></i></a>

<a name="http_operations"></a>

## HTTP Operations
-----------------------------------

`POST`{:.http-post} [https://riskhomolog.braspag.com.br/Analysis/](#post_analise){:.custom-attrib}  
Transaction analysis  

`GET`{:.http-get} [https://riskhomolog.braspag.com.br/Analysis/{Id}](#get_analise){:.custom-attrib}  
Get analysis details  

<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>

<a name="post_analise"></a>

#### `POST`{:.http-post} Transaction analysis 
-------------------------------------------

**REQUEST:**  

``` http
POST https://riskhomolog.braspag.com.br/Analysis/ HTTP/1.1
Host: {antifraude endpoint}
Authorization: Bearer {access_token}
Content-Type: application/json
MerchantId: {Merchant Id in Gateway Antifraud}
```

``` json
{
  "MerchantOrderId": "4493d42c-8732-4b13-aadc-b07e89732c26",
  "TotalOrderAmount": 1500,
  "TransactionAmount": 1000,
  "Currency": "BRL",
  "Provider": "RedShield",
  "OrderDate": "2016-12-09 12:35:58.852",
  "BraspagTransactionId":"a3e08eb2-2144-4e41-85d4-61f1befc7a3b",
  "SplitingPaymentMethod": "None",
  "IsRetryTransaction": false,
  "Card": {
  "Number" : "4000111231110112",
    "Holder": "Fernando Test",
    "ExpirationDate": "12/2023",
    "Cvv": "999",
    "Brand": "VISA",
    "EciThreeDSecure": "5"
  },
  "Billing": {
    "Street": "Av Marechal Camara",
    "Number": "12345",
    "Complement": "Sala 123",
    "Neighborhood": "Centro",
    "City": "Rio de Janeiro",
    "State": "RJ",
    "Country": "BR",
    "ZipCode": "20080123"
  },
  "Shipping": {
        "Street": "Avenida Rio Branco",
        "Number": "30000",
        "Complement": "sl 123",
        "Neighborhood": "Centro",
        "City": "Rio de Janeiro",
        "State": "RJ",
        "Country": "BR",
        "ZipCode": "123456789",
        "Email": "emailentrega@dominio.com.br",
        "FirstName": "João",
        "MiddleName": "P",
        "LastName": "Silvao",
        "ShippingMethod": "SameDay",
        "Phone": "552121114700",
        "WorkPhone": "552121114721",
        "Mobile": "5521998765432",
        "Comment": "Em frente ao 322"
    },
  "Customer": {
        "MerchantCustomerId": "10050665740",
        "FirstName": "João",
        "MiddleName": "P",
        "LastName": "Silva",
        "BirthDate": "2016-12-09",
        "Gender": "Male",
        "Email": "emailcomprador@dominio.com.br",
        "Phone": "552121114700",
        "WorkPhone": "552121114721",
        "Mobile": "5521998765432",
        "Ip": "127.0.0.1",
        "BrowserFingerprint": "04003hQUMXGB0poNf94lis1ztuLYRFk+zJ17aP79a9O8mWOBmEnKs6ziAo94ggAtBvKEN6/FI8Vv2QMAyHLnc295s0Nn8akZzRJtHwsEilYx1P+NzuNQnyK6+7x2OpjJZkl4NlfPt7h9d96X/miNlYT65UIY2PeH7sUAh9vKxMn1nlPu2MJCSi12NBBoiZbfxP1Whlz5wlRFwWJi0FRulruXQQGCQaJkXU7GWWZGI8Ypycnf7F299GIR12G/cdkIMFbm6Yf0/pTJUUz1vNp0X2Zw8QydKgnOIDKXq4HnEqNOos1c6njJgQh/4vXJiqy0MXMQOThNipDmXv9I185O+yC2f3lLEO0Tay66NZEyiLNePemJKSIdwO9O5ZtntuUkG6NTqARuHStXXfwp8cyGF4MPWLuvNvEfRkJupBy3Z8hSEMEK7ZWd2T2HOihQxRh4qp+NANqYKBTl3v6fQJAEKikeSQVeBN8sQqAL0BZFaIMzbrnMivi6m6JRQUIdvEt+MbJEPFc0LjRycC5ApUmJO+Aoo9VKL1B8ftMSQ1iq1uTKn16ZOmDpzZrZhMPbH83aV0rfB2GDXcjpghm9klVFOw7EoYzV7IDBIIRtgqG9KZ+8NH/z6D+YNUMLEUuK1N2ddqKbS5cKs2hplVRjwSv7x8lMXWE7VDaOZWB8+sD1cMLQtEUC0znzxZ4bpRaiSy4dJLxuJpQYAFUrDlfSKRv/eHV3QiboXLuw9Lm6xVBK8ZvpD5d5olGQdc+NgsqjFnAHZUE+OENgY4kVU9wB84+POrI4MkoD4iHJ5a1QF8AZkZDFo1m1h9Bl+J2Ohr6MkBZq8DG5iVaunHfxUdHou5GL7lS1H7r+8ctfDXi8AfOPjzqyODJQ74Aiel35TKTOWG8pq1WO6yzJ1GNmMuMWZBamlGXoG/imnjwHY9HQtQzpGfcm0cR8X2Fd1ngNFGLDGZlWOX0jWtOwU6XVGT37JFD9W/cx4kzI+mPNi65X5WFPYlDG9N0Lbh5nOj3u3DXqRCiKCUrsEkMt8z9fxO9pLLGVQUKIYR2wTw53CiWK96FOpPevDWtH2XR0QkfOd02D73n81x6hEMCy0s3hRLn08Th9FlNHDMJBqLj+Tz8rG2TtNki3mJC7Ass1MT2qnKBI77n6vsQkAp59TfbZm/tBXwAoYdLJXge8F/numhd5AvQ+6I8ZHGJfdN3qWndvJ2I7s5Aeuzb8t9//eNsm73fIa05XreFsNyfOq1vG2COftC6EEsoJWe5h5Nwu1x6PIKuCaWxLY+npfWgM0dwJPmSgPx7TNM31LyVNS65m83pQ+qMTRH6GRVfg7HAcS5fnS/cjdbgHxEkRmgkRq1Qs48sbX9QC8nOTD0ntb6FcJyEOEOVzmJtDqimkzDq+SXR1/63AYe4LEj+ogRgN+Z8HAFhGFzd/m6snVviELfRqJ4LLQIk9Y/fzqnsF6I5OGxfdT2sxxK2Vokpi3jWhCcEknw7dYlHYpOnCHZO7QVgjQTngF2mzKf4GeOF4ECFsWTgLy6HFEitfauYJt1Xh1NfZZerBMwXLFzdhzoTQxGlcXc8lZIoEG1BLYv/ScICf8Ft9PEtpEa+j0cDSlU99UoH2xknwR1W9MRGc5I/euE63/IMJTqguZ3YcnJpjSVnAGSpyz/0gKjypJ3L86rHFRGXt0QbmaXtSl2UmmjI0p0LCCdx7McatCFEVI6FwPpPV0ZSMv/jM75eBid1X/lTV4XNzjowzR/iFlKYMzHZtVO9hCBPKlTwblRXNn4MlvNm/XeSRQ+Mr0YV5w5CL5Z/tGyzqnaLPj/kOVdyfj8r2m5Bcrz4g/ieUIo8qRFv2T2mET46ydqaxi27G4ZYHj7hbiaIqTOxWaE07qMCkJw==",
        "Status": "NEW"
    },
  "CartItems": [
    {
      "ProductName": "Mouse",
      "UnitPrice": "12000",
      "MerchantItemId": "4",
      "Sku": "abc123",
      "Quantity": 1,
      "OriginalPrice": "12000",
      "GiftMessage": "Te amo!",
      "Description": "Uma description do Mouse",
      "ShippingInstructions": "Proximo ao 546",
      "ShippingMethod": "SameDay",
      "ShippingTrackingNumber": "123456",
      "Passenger": {
        "FirstName": "João",
        "MiddleName": "P",
        "LastName": "Silva",
        "PassengerId": "1",
        "Status": "NEW",
        "PassengerType": "Adult",
        "Email": "emailpassageiro@dominio.com.br",
        "Phone" : "552121114700",
        "DateOfBirth": "1982-04-30"
      }
    },
    {
      "ProductName": "Teclado",
      "UnitPrice": "96385",
      "MerchantItemId": "3",
      "Sku": "abc456",
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
    "MerchantWebsite": "www.test.com"
  },
  "MerchantDefinedData": [
    {
      "Key": "USER_DATA4",
      "Value": "Valor definido com o Provedor a ser enviado neste campo."
    },
    {
      "Key": "Segment",
      "Value": "8999"
    },
    {
      "Key": "MerchantId",
      "Value": "Seller123456"
    }
  ],
  "Travel": {
    "CompleteRoute": "GIG-CGH-EZE",
    "DepartueTime": "2016-12-10",
    "JourneyType": "OneWayTrip",
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
  }
}
```

**RESPONSE:**  

- When the transaction has the analysis performed.

**Id**  
Id of the transaction in the Antifraude Gateway Braspag.

**AnalysisResult.Status**  
Transaction status in the Anti-fraud Gateway Braspag after the analysis.  
Enum:  
Started = Transaction received by Braspag.  
Accept = Transaction accepted after fraud analysis.  
Review = Transaction under review after fraud analysis.  
Reject = Transaction rejected after fraud analysis.  
Unfinished = Transaction not finalized by some internal error in the system.  
ProviderError = Transaction with error in the anti-fraud provider.  

**Message**  
Anti-Fraud provider return message.  

**ProviderCode**  
Anti-fraud provider return code.  

**ProviderTransactionId**  
Transaction ID in the anti-fraud provider.  

**ProviderRequestTransactionId**  
Transaction request id in the anti-fraud provider.  

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
    "ProviderTransactionId": "487931363026",
    "ProviderRequestTransactionId": "8a8394865a353cc4015a37947c5f7e35"
  },
  "MerchantOrderId": "4493d42c-8732-4b13-aadc-b07e89732c26",
  "TotalOrderAmount": 1500,
  "TransactionAmount": 1000,
  "Currency": "BRL",
  "Provider": "RedShield",
  "OrderDate": "2016-12-09 12:35:58.852",
  "BraspagTransactionId":"a3e08eb2-2144-4e41-85d4-61f1befc7a3b",
  "SplitingPaymentMethod": "None",
  "IsRetryTransaction": false,
  "Card": {
  "Number" : "400011******0112",
    "Holder": "Fernando Test",
    "ExpirationDate": "12/2023",
    "Cvv": "***",
    "Brand": "VISA",
    "EciThreeDSecure": "5"
  },
  "Billing": {
    "Street": "Av Marechal Camara",
    "Number": "12345",
    "Complement": "Sala 123",
    "Neighborhood": "Centro",
    "City": "Rio de Janeiro",
    "State": "RJ",
    "Country": "BR",
    "ZipCode": "20080123"
  },
  "Shipping": {
        "Street": "Avenida Rio Branco",
        "Number": "30000",
        "Complement": "sl 123",
        "Neighborhood": "Centro",
        "City": "Rio de Janeiro",
        "State": "RJ",
        "Country": "BR",
        "ZipCode": "123456789",
        "Email": "emailentrega@dominio.com.br",
        "FirstName": "João",
        "MiddleName": "P",
        "LastName": "Silvao",
        "ShippingMethod": "SameDay",
        "Phone": "552121114700",
        "WorkPhone": "552121114721",
        "Mobile": "5521998765432",
        "Comment": "Em frente ao 322"
    },
  "Customer": {
        "MerchantCustomerId": "10050665740",
        "FirstName": "João",
        "MiddleName": "P",
        "LastName": "Silva",
        "BirthDate": "2016-12-09",
        "Gender": "Male",
        "Email": "emailcomprador@dominio.com.br",
        "Phone": "552121114700",
        "WorkPhone": "552121114721",
        "Mobile": "5521998765432",
        "Ip": "127.0.0.1",
        "BrowserFingerprint": "04003hQUMXGB0poNf94lis1ztuLYRFk+zJ17aP79a9O8mWOBmEnKs6ziAo94ggAtBvKEN6/FI8Vv2QMAyHLnc295s0Nn8akZzRJtHwsEilYx1P+NzuNQnyK6+7x2OpjJZkl4NlfPt7h9d96X/miNlYT65UIY2PeH7sUAh9vKxMn1nlPu2MJCSi12NBBoiZbfxP1Whlz5wlRFwWJi0FRulruXQQGCQaJkXU7GWWZGI8Ypycnf7F299GIR12G/cdkIMFbm6Yf0/pTJUUz1vNp0X2Zw8QydKgnOIDKXq4HnEqNOos1c6njJgQh/4vXJiqy0MXMQOThNipDmXv9I185O+yC2f3lLEO0Tay66NZEyiLNePemJKSIdwO9O5ZtntuUkG6NTqARuHStXXfwp8cyGF4MPWLuvNvEfRkJupBy3Z8hSEMEK7ZWd2T2HOihQxRh4qp+NANqYKBTl3v6fQJAEKikeSQVeBN8sQqAL0BZFaIMzbrnMivi6m6JRQUIdvEt+MbJEPFc0LjRycC5ApUmJO+Aoo9VKL1B8ftMSQ1iq1uTKn16ZOmDpzZrZhMPbH83aV0rfB2GDXcjpghm9klVFOw7EoYzV7IDBIIRtgqG9KZ+8NH/z6D+YNUMLEUuK1N2ddqKbS5cKs2hplVRjwSv7x8lMXWE7VDaOZWB8+sD1cMLQtEUC0znzxZ4bpRaiSy4dJLxuJpQYAFUrDlfSKRv/eHV3QiboXLuw9Lm6xVBK8ZvpD5d5olGQdc+NgsqjFnAHZUE+OENgY4kVU9wB84+POrI4MkoD4iHJ5a1QF8AZkZDFo1m1h9Bl+J2Ohr6MkBZq8DG5iVaunHfxUdHou5GL7lS1H7r+8ctfDXi8AfOPjzqyODJQ74Aiel35TKTOWG8pq1WO6yzJ1GNmMuMWZBamlGXoG/imnjwHY9HQtQzpGfcm0cR8X2Fd1ngNFGLDGZlWOX0jWtOwU6XVGT37JFD9W/cx4kzI+mPNi65X5WFPYlDG9N0Lbh5nOj3u3DXqRCiKCUrsEkMt8z9fxO9pLLGVQUKIYR2wTw53CiWK96FOpPevDWtH2XR0QkfOd02D73n81x6hEMCy0s3hRLn08Th9FlNHDMJBqLj+Tz8rG2TtNki3mJC7Ass1MT2qnKBI77n6vsQkAp59TfbZm/tBXwAoYdLJXge8F/numhd5AvQ+6I8ZHGJfdN3qWndvJ2I7s5Aeuzb8t9//eNsm73fIa05XreFsNyfOq1vG2COftC6EEsoJWe5h5Nwu1x6PIKuCaWxLY+npfWgM0dwJPmSgPx7TNM31LyVNS65m83pQ+qMTRH6GRVfg7HAcS5fnS/cjdbgHxEkRmgkRq1Qs48sbX9QC8nOTD0ntb6FcJyEOEOVzmJtDqimkzDq+SXR1/63AYe4LEj+ogRgN+Z8HAFhGFzd/m6snVviELfRqJ4LLQIk9Y/fzqnsF6I5OGxfdT2sxxK2Vokpi3jWhCcEknw7dYlHYpOnCHZO7QVgjQTngF2mzKf4GeOF4ECFsWTgLy6HFEitfauYJt1Xh1NfZZerBMwXLFzdhzoTQxGlcXc8lZIoEG1BLYv/ScICf8Ft9PEtpEa+j0cDSlU99UoH2xknwR1W9MRGc5I/euE63/IMJTqguZ3YcnJpjSVnAGSpyz/0gKjypJ3L86rHFRGXt0QbmaXtSl2UmmjI0p0LCCdx7McatCFEVI6FwPpPV0ZSMv/jM75eBid1X/lTV4XNzjowzR/iFlKYMzHZtVO9hCBPKlTwblRXNn4MlvNm/XeSRQ+Mr0YV5w5CL5Z/tGyzqnaLPj/kOVdyfj8r2m5Bcrz4g/ieUIo8qRFv2T2mET46ydqaxi27G4ZYHj7hbiaIqTOxWaE07qMCkJw==",
        "Status": "NEW"
    },
  "CartItems": [
    {
      "ProductName": "Mouse",
      "UnitPrice": "12000",
      "MerchantItemId": "4",
      "Sku": "abc123",
      "Quantity": 1,
      "OriginalPrice": "12000",
      "GiftMessage": "Te amo!",
      "Description": "Uma description do Mouse",
      "ShippingInstructions": "Proximo ao 546",
      "ShippingMethod": "SameDay",
      "ShippingTrackingNumber": "123456",
      "Passenger": {
        "FirstName": "João",
        "MiddleName": "P",
        "LastName": "Silva",
        "PassengerId": "1",
        "Status": "NEW",
        "PassengerType": "Adult",
        "Email": "emailpassageiro@dominio.com.br",
        "Phone" : "552121114700",
        "DateOfBirth": "1982-04-30"
      }
    },
    {
      "ProductName": "Teclado",
      "UnitPrice": "96385",
      "MerchantItemId": "3",
      "Sku": "abc456",
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
    "MerchantWebsite": "www.test.com"
  },
  "MerchantDefinedData": [
    {
      "Key": "USER_DATA4",
      "Value": "Valor definido com o Provedor a ser enviado neste campo."
    },
    {
      "Key": "Segment",
      "Value": "8999"
    },
    {
      "Key": "MerchantId",
      "Value": "Seller123456"
    }
  ],
  "Travel": {
    "CompleteRoute": "GIG-CGH-EZE",
    "DepartueTime": "2016-12-10",
    "JourneyType": "OneWayTrip",
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
  }
}
```
- When the data submitted for analysis has any inconsistency in the values, permitted sizes and / or field types as specified in the manual.

**Message**  
Message for an invalid request.  

**ModelState**  
If any field does not conform to the type or domain specified in the manual.  

**ModelState.FraudAnalysisRequestError**  
If any field does not conform to the size specified in the manual.  

``` http
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8
```
``` json
{
  "Message": "The request is invalid.",
  "ModelState": {
    "request.Customer.Gender": [
      "Error converting value \"M\" to type 'Antifraude.Domain.Enums.GenderType'. Path 'Customer.Gender', line 51, position 17."
    ],
    "FraudAnalysisRequestError": [
      "The Card.EciThreeDSecure lenght is gratter than 1",
      "The Shipping.Complement lenght is gratter than 14",
      "The Shipping.MiddleName lenght is gratter than 1",
      "The Customer.MerchantCustomerId lenght is gratter than 16",
      "The Customer.MiddleName lenght is gratter than 1"
    ]
  }
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

- When the transaction is not found in the database.  

``` http
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8
```

- When the transaction is found in the database.  

``` http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
```
``` json
{
  "Id": "22b5e829-edf1-e611-9414-0050569318a7",
  "AnalysisResult": {
    "Status": "Review",
    "Message": "Payment void and transaction challenged by ReD Shield",
    "ProviderCode": "100.400.148",
    "ProviderTransactionId": "487931363026",
    "ProviderRequestTransactionId": "8a8394865a353cc4015a37947c5f7e35"
  },
  "MerchantOrderId": "4493d42c-8732-4b13-aadc-b07e89732c26",
  "TotalOrderAmount": 1500,
  "TransactionAmount": 1000,
  "Currency": "BRL",
  "Provider": "RedShield",
  "OrderDate": "2016-12-09 12:35:58.852",
  "BraspagTransactionId":"a3e08eb2-2144-4e41-85d4-61f1befc7a3b",
  "SplitingPaymentMethod": "None",
  "IsRetryTransaction": false,
  "Card": {
  "Number" : "400011******0112",
    "Holder": "Fernando Test",
    "ExpirationDate": "12/2023",
    "Cvv": "***",
    "Brand": "VISA",
    "EciThreeDSecure": "5"
  },
  "Billing": {
    "Street": "Av Marechal Camara",
    "Number": "12345",
    "Complement": "Sala 123",
    "Neighborhood": "Centro",
    "City": "Rio de Janeiro",
    "State": "RJ",
    "Country": "BR",
    "ZipCode": "20080123"
  },
  "Shipping": {
        "Street": "Avenida Rio Branco",
        "Number": "30000",
        "Complement": "sl 123",
        "Neighborhood": "Centro",
        "City": "Rio de Janeiro",
        "State": "RJ",
        "Country": "BR",
        "ZipCode": "123456789",
        "Email": "emailentrega@dominio.com.br",
        "FirstName": "João",
        "MiddleName": "P",
        "LastName": "Silvao",
        "ShippingMethod": "SameDay",
        "Phone": "552121114700",
        "WorkPhone": "552121114721",
        "Mobile": "5521998765432",
        "Comment": "Em frente ao 322"
    },
  "Customer": {
        "MerchantCustomerId": "10050665740",
        "FirstName": "João",
        "MiddleName": "P",
        "LastName": "Silva",
        "BirthDate": "2016-12-09",
        "Gender": "Male",
        "Email": "emailcomprador@dominio.com.br",
        "Phone": "552121114700",
        "WorkPhone": "552121114721",
        "Mobile": "5521998765432",
        "Ip": "127.0.0.1",
        "BrowserFingerprint": "04003hQUMXGB0poNf94lis1ztuLYRFk+zJ17aP79a9O8mWOBmEnKs6ziAo94ggAtBvKEN6/FI8Vv2QMAyHLnc295s0Nn8akZzRJtHwsEilYx1P+NzuNQnyK6+7x2OpjJZkl4NlfPt7h9d96X/miNlYT65UIY2PeH7sUAh9vKxMn1nlPu2MJCSi12NBBoiZbfxP1Whlz5wlRFwWJi0FRulruXQQGCQaJkXU7GWWZGI8Ypycnf7F299GIR12G/cdkIMFbm6Yf0/pTJUUz1vNp0X2Zw8QydKgnOIDKXq4HnEqNOos1c6njJgQh/4vXJiqy0MXMQOThNipDmXv9I185O+yC2f3lLEO0Tay66NZEyiLNePemJKSIdwO9O5ZtntuUkG6NTqARuHStXXfwp8cyGF4MPWLuvNvEfRkJupBy3Z8hSEMEK7ZWd2T2HOihQxRh4qp+NANqYKBTl3v6fQJAEKikeSQVeBN8sQqAL0BZFaIMzbrnMivi6m6JRQUIdvEt+MbJEPFc0LjRycC5ApUmJO+Aoo9VKL1B8ftMSQ1iq1uTKn16ZOmDpzZrZhMPbH83aV0rfB2GDXcjpghm9klVFOw7EoYzV7IDBIIRtgqG9KZ+8NH/z6D+YNUMLEUuK1N2ddqKbS5cKs2hplVRjwSv7x8lMXWE7VDaOZWB8+sD1cMLQtEUC0znzxZ4bpRaiSy4dJLxuJpQYAFUrDlfSKRv/eHV3QiboXLuw9Lm6xVBK8ZvpD5d5olGQdc+NgsqjFnAHZUE+OENgY4kVU9wB84+POrI4MkoD4iHJ5a1QF8AZkZDFo1m1h9Bl+J2Ohr6MkBZq8DG5iVaunHfxUdHou5GL7lS1H7r+8ctfDXi8AfOPjzqyODJQ74Aiel35TKTOWG8pq1WO6yzJ1GNmMuMWZBamlGXoG/imnjwHY9HQtQzpGfcm0cR8X2Fd1ngNFGLDGZlWOX0jWtOwU6XVGT37JFD9W/cx4kzI+mPNi65X5WFPYlDG9N0Lbh5nOj3u3DXqRCiKCUrsEkMt8z9fxO9pLLGVQUKIYR2wTw53CiWK96FOpPevDWtH2XR0QkfOd02D73n81x6hEMCy0s3hRLn08Th9FlNHDMJBqLj+Tz8rG2TtNki3mJC7Ass1MT2qnKBI77n6vsQkAp59TfbZm/tBXwAoYdLJXge8F/numhd5AvQ+6I8ZHGJfdN3qWndvJ2I7s5Aeuzb8t9//eNsm73fIa05XreFsNyfOq1vG2COftC6EEsoJWe5h5Nwu1x6PIKuCaWxLY+npfWgM0dwJPmSgPx7TNM31LyVNS65m83pQ+qMTRH6GRVfg7HAcS5fnS/cjdbgHxEkRmgkRq1Qs48sbX9QC8nOTD0ntb6FcJyEOEOVzmJtDqimkzDq+SXR1/63AYe4LEj+ogRgN+Z8HAFhGFzd/m6snVviELfRqJ4LLQIk9Y/fzqnsF6I5OGxfdT2sxxK2Vokpi3jWhCcEknw7dYlHYpOnCHZO7QVgjQTngF2mzKf4GeOF4ECFsWTgLy6HFEitfauYJt1Xh1NfZZerBMwXLFzdhzoTQxGlcXc8lZIoEG1BLYv/ScICf8Ft9PEtpEa+j0cDSlU99UoH2xknwR1W9MRGc5I/euE63/IMJTqguZ3YcnJpjSVnAGSpyz/0gKjypJ3L86rHFRGXt0QbmaXtSl2UmmjI0p0LCCdx7McatCFEVI6FwPpPV0ZSMv/jM75eBid1X/lTV4XNzjowzR/iFlKYMzHZtVO9hCBPKlTwblRXNn4MlvNm/XeSRQ+Mr0YV5w5CL5Z/tGyzqnaLPj/kOVdyfj8r2m5Bcrz4g/ieUIo8qRFv2T2mET46ydqaxi27G4ZYHj7hbiaIqTOxWaE07qMCkJw==",
        "Status": "NEW"
    },
  "CartItems": [
    {
      "ProductName": "Mouse",
      "UnitPrice": "12000",
      "MerchantItemId": "4",
      "Sku": "abc123",
      "Quantity": 1,
      "OriginalPrice": "12000",
      "GiftMessage": "Te amo!",
      "Description": "Uma description do Mouse",
      "ShippingInstructions": "Proximo ao 546",
      "ShippingMethod": "SameDay",
      "ShippingTrackingNumber": "123456",
      "Passenger": {
        "FirstName": "João",
        "MiddleName": "P",
        "LastName": "Silva",
        "PassengerId": "1",
        "Status": "NEW",
        "PassengerType": "Adult",
        "Email": "emailpassageiro@dominio.com.br",
        "Phone" : "552121114700",
        "DateOfBirth": "1982-04-30"
      }
    },
    {
      "ProductName": "Teclado",
      "UnitPrice": "96385",
      "MerchantItemId": "3",
      "Sku": "abc456",
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
    "MerchantWebsite": "www.test.com"
  },
  "MerchantDefinedData": [
    {
      "Key": "USER_DATA4",
      "Value": "Valor definido com o Provedor a ser enviado neste campo."
    },
    {
      "Key": "Segment",
      "Value": "8999"
    },
    {
      "Key": "MerchantId",
      "Value": "Seller123456"
    }
  ],
  "Travel": {
    "CompleteRoute": "GIG-CGH-EZE",
    "DepartueTime": "2016-12-10",
    "JourneyType": "OneWayTrip",
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
  }
}
```
  
<a style="float: right;" href="#http_operations"><i class="fa fa-angle-double-up fa-fw"></i></a>
  

