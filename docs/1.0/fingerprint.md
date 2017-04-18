---
layout: page-classic-sidebar-left
title: Fingerprint Setup
featimg: MapAntifraud.png
previous: /docs/1.0/postnotification
next: /docs/1.0/autenticacao
---

Service that collects device fingerprint and real geolocation from buyer IP and creates a *black box*.
This *black box* is a string of encrypted characters that contain all device attributes.  

-----------------------------------

## How it works?

![Fluxo]({{ site.url }}/img/fingerprint.png){: .centerimg }{:title="Fingerprint Collection Flow "}

1 - The store checkout page sends the attributes of the buyer's device to Iovation, thereby creating the *black box*  
2 - The store receives an Iovation encryption string and writes the same on the checkout page in a field of type *hidden*  
3 - The store sends to Braspag, together with the other data of the transaction to be analyzed, the *black box*  
4 - Braspag receives all data, validates and sends to ReD Shield  
5 - ReD Shield receives all data, sends the *black box* to the Iovation decrypt  
6 - Red Shield receives from Iovation the attributes of the buyer's device 

## How to configure?

1 - Include Iovation's javascript on your checkout page  
2 - Add configuration parameters in javascript  
3 - Create a field of type *hidden* on your page to write the *black box* in it and send it along with the transaction data to be analyzed  

**Note.:** Do not cache the script as it may occur that multiple devices are identified as being the same.

* Including javascript from Iovation  

    To include javascript, add the `<script>` element to your checkout page. This is the URL of the snare.js version of the Iovation production environment.  
    **Exemple:** `<script type="text/javascript" src="https://mpsnare.iesnare.com/snare.js"></script>`  

    **IMPORTANT!**  
    The configuration parameters should be placed before the above tag is called. They determine how iovation's javascript will work, and errors can occur if they are placed before the javascript call.

**Exemple**  

```html
<html>
<head>
<script>
    var io_install_flash = false;
    var io_install_stm = false;
    var io_bbout_element_id = 'gatewayFingerprint';
</script>
</head>
<script type="text/javascript" src="https://mpsnare.iesnare.com/snare.js"></script>

<body>
    <form>
        <input type="hidden" name="gatewayFingerprint" id="gatewayFingerprint">
    </form>
</body>
</html>
```




