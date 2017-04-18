---
layout: page-classic-sidebar-left
title: Status Change Notification
featimg: MapAntifraud.png
previous: /docs/1.0/analise
next: /docs/1.0/autenticacao
---
---

Service that sends a notification post to the client if there is any change of status.

* It is necessary to request the Implementation Team ([implantacao.operacoes@braspag.com.br](mailto:implantacao.operacoes@braspag.com.br)) to register the status change URL.
When stimulated by Braspag's server, sending a POST, the URL registered to receive the
Change status, you must return the HTTP 200 (OK) code, indicating that the message was successfully received and processed by the store server.

* If the store status change URL is accessed by the Braspag server, do not return the
HTTP 200 (OK) or a connection failure occurs, a further 3 send attempts will be made.

* The status change URL can only use port 80 (default for http) or port
443 (default for https). We recommend that the store always work with SSL for this URL, always HTTPS.

![Status Change Notification]({{ site.url }}/img/PostNotification.png){: .centerimg }{:title="Status Change Notification "}

#### `POST`{:.http-post} Status Change Notification 
----------------------------------------------
Below are the sample messages that the Braspag server will send to the registered URL, and what the response should be if it succeeds.

**REQUEST:**  

``` http
POST https://urlregistered.store.com.br/Notification/ HTTP/1.1
Host: urlcregistered.store.com.br
Content-Type: application/json
```

``` json
{  
   "Id":"9004ba26-f1f1-e611-9400-005056970d6f",
   "OrderId":"4493d42c-8732-4b13-aadc-b07e89732c27",
   "OriginalDecision":"Review",
   "NewDecision":"Accept",
   "Reviewer":"João das Couves",
   "ReviewerComments":"Transaction Accepted After Customer Connection",
   "Notes":null,
   "Queue":null,
   "Profile":null
}​​​
```

**RESPONSE:**  

``` http
HTTP/1.1 200 Ok
```