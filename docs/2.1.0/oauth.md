---
layout: page-classic-sidebar-left
title: Tokens de Autorização
previous: /docs/2.1.0/roles
next: /docs/2.1.0/product
---
---

As APIs BlackBox utilizam o protocolo padrão de mercado OAuth 2.0 para autorização de acesso a seus recursos. 

Este documento descreve o fluxo necessário para que aplicações cliente obtenham tokens de acesso válidos para uso na plataforma. Caso deseje mais informações sobre o protocolo OAuth 2.0, consulte [https://oauth.net/2/](https://oauth.net/2/){:target="_blank"}.  

## O fluxo para obtenção do token de acesso  
----------------------------------------------

O token de acesso é obtido através do fluxo de autorização *Resource Owner Password Credentials*. O diagrama a seguir ilustra, em ordem cronológica, a comunicação que se dá entre a *Aplicação Cliente*, o *Servidor de Autorização* e as APIs.

![Obtenção de Tokens de Acesso]({{ site.url }}/img/docs-blackboxapi-02.png){: .centerimg }{:title="Fluxo para obtenção do Token de Acesso "}

1. O usuário, através da *Aplicação Cliente*, informa ao *Authorization Server* suas credenciais de serviço.  

2. O *Authorization Server* valida a credencial recebida. Se for válida, retorna o token de acesso para a *Aplicação Cliente*.  

3. A *Aplicação Cliente* informa o token de acesso obtido no cabeçalho das requisições HTTP feitas às APIs.   

4. Se o token de acesso for válido, a requisição é processada e os dados são retornados para a *Aplicação Cliente*.

## Exemplo de requisição HTTP  
----------------------------------------------

### Cenário I: Obtenção de token de acesso  

**REQUEST:**  

``` http
POST /oauth/token HTTP/1.1
Host: {blackbox endpoint}
Content-Type: application/x-www-form-urlencoded
Cache-Control: no-cache

username={usuario}&password={senha}&grant_type=password
```

**RESPONSE:**  

``` http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
```
``` json
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
    "token_type": "bearer",
    "expires_in": 86399
}
```
  

### Cenário II: Chamada para operação da API utilizando o token de acesso obtido  
  
**REQUEST:**  

``` http
POST /api/product/ HTTP/1.1
Host: {blackbox endpoint}
Connection: keep-alive
Content-Length: 220
Authorization: Bearer {access_token}
```
  
**RESPONSE:**  

``` http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
```
```json
{
    ...
}
```
  

### Como obter uma credencial de usuário?  

> Este serviço está em **BETA**. Solicite uma credencial pelo e-mail [blackbox@braspag.com.br](mailto:blackbox@braspag.com.br)
