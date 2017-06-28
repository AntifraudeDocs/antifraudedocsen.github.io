---
layout: page-classic-sidebar-left
title: Status Change Notification
featimg: MapAntifraud.png
previous: /docs/1.0/analise
next: /docs/1.0/autenticacao
---
---

Service that sends a notification post to the client if there is any change of status.  

* It is necessary to request the Implementation Team ([implantacao.operacoes@braspag.com.br](mailto:implantacao.operacoes@braspag.com.br)) to register the status change URL. When stimulated by Braspag's server, sending a POST, the URL registered to receive the Change status, you must return the HTTP 200 (OK) code, indicating that the message was successfully received and processed by the merchant server.

* If the merchant status change URL is accessed by the Braspag server, do not return the HTTP 200 (OK) or a connection failure occurs, a further 3 send attempts will be made.

* The status change URL can only use port 80 (default for http) or port 443 (default for https). We recommend that the merchant always work with SSL for this URL, always HTTPS.  

* After the merchant receives the status change notification, it must perform a GET through the URL https://riskhomolog.braspag.com.br/Analysis/{Id}, sending the transaction ID that was received in the notice of the change of status .
For more details on how to perform GET, see Analysis of the [Getting Analysis Details] session ({{site.baseurl}} {% link docs / 1.0 / analysis.md%}).

![Status Change Notification]({{ site.url }}/img/PostNotification.png){: .centerimg }{:title="Status Change Notification "}

#### `POST`{:.http-post} Status Change Notification 
----------------------------------------------
Below are the sample messages that the Braspag server will send to the registered URL, and what the response should be if it succeeds.

**REQUEST:**  

``` http
POST https://urlregistered.merchant.com.br/Notification/ HTTP/1.1
Host: urlcregistered.merchant.com.br
Content-Type: application/json
```

``` json
{  
   "Id":"9004ba26-f1f1-e611-9400-005056970d6f"
}​​​
```

**RESPONSE:**  

``` http
HTTP/1.1 200 Ok
```