---
layout: page-classic-sidebar-left
title: Configuração do Fingerprint
featimg: MapAntifraud.png
previous: /docs/1.0/postnotification
next: /docs/1.0/autenticacao
---

Serviço que coleta impressão digital de dispositivos e geolocalização real do IP do comprador e cria uma *caixa preta*.  
Esta *caixa preta* é uma sequência de caracteres criptografados que contêm todos os atributos do dispositivo.  

-----------------------------------

## Como funciona?

![Fluxo]({{ site.url }}/img/fingerprint.png){: .centerimg }{:title="Fluxo da coleta do fingerprint "}

1 - A página de checkout da loja envia os atributos do dispositivo do comprador para a Iovation, criando assim a *caixa preta*  
2 - O lojista recebe a sequência de caracteres criptografados da Iovation e escreve o mesmo na página de checkout em um campo do tipo *hidden*  
3 - O lojista envia para a Braspag, junto com os demais dados da transação a ser analisada, a *caixa preta*  
4 - A Braspag recebe todos os dados, valida e envia para a ReD Shield  
5 - A ReD Shield recebe todos os dados, envia a *caixa preta* para a Iovation descriptografar  
6 - A Red Shield recebe da Iovation os atributos do dispositivo do comprador 

## Como configurar?

1 - Inclua o javascript da Iovation em sua página de checkout  
2 - Adicione parâmetros de configuração no javascript  
3 - Crie um campo do tipo *hidden* em sua página para escrever a *caixa preta* nele e enviá-lo junto com os dados da transação a ser analisada  

**Obs.:** Não realize cache do script, pois pode ocorrer de vários dispositovos sejam identificados como sendo o mesmo.

* Incluindo o javascript da Iovation  

    Para incluir o javascript, adicione o seguinte elemento `<script>` na sua página de checkout. Esta é a URL da versão do snare.js do ambiente de produção da Iovation.  
    **Exemplo:** `<script type="text/javascript" src="https://mpsnare.iesnare.com/snare.js"></script>`  

    **IMPORTANTE!**  
    Os parâmetros de configuração devem ser colocados antes da chamada da tag acima. Eles determinam como javascript do iovation funcionará, e podem ocorrer erros
    caso os mesmos sejam colocados antes da chamada do javascript.

**Exemplo**  

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



