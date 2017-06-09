---
layout: page-classic-sidebar-left
title: Authentication
featimg: MapAntifraud.png
previous: /docs/1.0/postnotification
next: /docs/1.0/analise
---
---

The Gateway Anti-Fraud API uses the industry-standard OAuth 2.0 protocol for authorization to access your resources. 

This document describes the flow necessary for **client** obtain valid access tokens for use on the platform. If you want more information about the OAuth 2.0 protocol, see [https://oauth.net/2/](https://oauth.net/2/){:target="_blank"}.  

## Hosts

**Test** https://authhomolog.braspag.com.br  
**Live** https://auth.braspag.com.br

## Flow to obtain the access token  
----------------------------------------------

* The access token is obtained through the authorization flow **Client Credentials**.

![Obtaining Access Tokens]({{ site.url }}/img/AntifraudeAuthentication.png){: .centerimg }{:title="Flow to obtain the access token "}

-- Access Token Obtaining Flow:

1. The *Client Application*, informs the *OAuth Braspag* API your credentials.  

2. The *OAuth Braspag* validates the credential received. If valid, returns the access token for the *Client Application*.  

-- Analysis Flow:

3. A *Client Application* informs the access token in the header of the HTTP Fraud Analysis requests.  

4. If the access token is valid, the request is processed and the analysis response is returned *Client application*.  


## Exemple HTTP request  
----------------------------------------------

### Scenario I: Obtaining access token  

* In order to authenticate with the Anti-Fraud API, it is necessary that the credentials **user** and **password** be created in advance, which must be requested from Braspag's Implementation Team.

* Once in possession of the credentials, it will be necessary to "code it" in Base64, using a convention **"username: password"**.
<br/>Exemple:

    * User: braspagtestes
    * Password: 1q2w3e4r
    * String a ser codificada em Base 64: **braspagtestes:1q2w3e4r**
    * Resultado: YnJhc3BhZ3Rlc3RlczoxcTJ3M2U0cg==

**REQUEST:**  

``` http
POST https://authhomolog.braspag.com.br/oauth2/token HTTP/1.1
Host: https://authhomolog.braspag.com.br
Content-Type: application/x-www-form-urlencoded
Authorization: Basic {StringCodificadaEmBase64}
Scope: AntifraudGatewayApp
Cache-Control: no-cache

grant_type=client_credentials
```

**RESPONSE:**  

``` http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
```
``` json
{
  "access_token": "faSYkjfiod8ddJxFTU3vti_rQV9fGvMrBNn0ZIZDqrLadEPKTUjt6ZPJSnNHtvOoJ6KO6gakgeyXNmSxFYHx7Y_-OCf8zgzILTVzCN5G1WTBWOKZHt-RknkmQLOgA882pWhC1gtOIQoq2tFX6-1VhOqsSCrdI3cUa2HolbGkxZWZMTPOl4Jzuy6ejo_USCMBNPqzvinchS0M33Bi8PiWMYwdpAbvwAe_nhIKNGmsAG6s7PTgWc2RksG6DaX8exdjvlGE9CMADq5LeM4JJ-BguZoHAP3yDBVZpe_DzI3JOrAYv0yzToBllPIMmq6CY-V8GJmckWByOGooBKr6COkZ1R9NPg2bvruYEC3g8hzKloUG21CD5r_la-t-0FvGHHY-8L7cKGybLidIYtw5aWOUgO2Aq0YScEnj1byDAsY6ROMnnzLrywkqscsf5xJACJwBmmEggHRyTVMY1-oOzmH6B2GNtC621i2XQ-8U6KVx9qD0R4qdWRn__AFatL7miTthMfO_PO2HWdDX_xD0i0jqcw",
  "token_type": "bearer",
  "expires_in": 599
}
```
 
 * In the response it is important to highlight the **expires_in** field, with the expiration time for access token in seconds.

### How to obtain a user credential?  

> Request a credential by email [implantacao.operacoes@braspag.com.br](mailto:implantacao.operacoes@braspag.com.br)
