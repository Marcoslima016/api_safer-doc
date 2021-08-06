

<!-- COMMIT MARKER -->

Modulo destinado a todas as requisições relacionadas ao processo de autenticação. ( Cadastro, login, logout, etc)

---

<!---=========================================== LOGIN ===========================================--->
##Login 

<!----------- INTRO ----------->

###Introdução 
Requisição utilizada para validar um usuário. Se for bem sucedida, retorna um Token JWT que será usado para requisições futuras.

<!---------- REQUEST ---------->
###Request

- **Endpoint:** https://www.segcontrole.com.br/safer/v1/login.php
- **Method:** [![Flattr this git repo](https://img.shields.io/badge/-POST-orange)]()


<!-------- PARAMETERS -------->

###Parametros

<table>
   <!-- HEADER -->
   <thead>
    <tr>
      <th scope="col">Parametro</th>
      <th scope="col">Tipo</th>
      <th scope="col">Descrição</th>
    </tr>
  </thead>
    </tr>
  <!---- DATA --->
  <tbody>
    <!---->
    <tr>
      <td >usuario</td>
      <td>STRING</td>
      <td>
      <b>Obrigatório</b> </br>
      Usuário utilizado para fazer o acesso(login). Nessa caso, o parametro usuario corresponde ao numero de celular usado no cadastro.</td>
    </tr>
    <!---->
    <tr>
      <td >senha</td>
      <td>STRING</td>
      <td>        <b>Obrigatório</b> </br>Senha de acesso do usuário.</td>
    </tr>
    <!---->
    <tr>
      <td >token_push</td>
      <td>STRING</td>
      <td>
      <b>Obrigatório</b> </br>      
      Token push gerado pelo firebase messaging. Utilizado para enviar notificações push para o usuário.</td>
    </tr>
    <!---->
    <tr>
      <td >token_voip</td>
      <td>STRING</td>
      <td>  
      <b>Obrigatório</b> </br>      
      Token de chamadas VOIP</td>
    </tr>
    <!---->
    <tr>
      <td >so</td>
      <td>STRING</td>
      <td>
      <b>Obrigatório</b> </br>
      Indica qual o sistema operacional em que o app esta instalado.</br>
      <b>Valores:</b> IOS / ANDROID 
      </td>
    </tr>    
    <!---->
    <tr>
      <td >so_ver</td>
      <td>STRING</td>
      <td>
      <b>Obrigatório</b> </br>
      Indica qual a versão do sistema operacional. 
      </td>
    </tr>  
    <!---->
    <tr>
      <td >app_id</td>
      <td>INT</td>
      <td>
      <b>Obrigatório</b> </br>
      ID do aplicativo. ( Cada aplicativo da familia Safer tem seu ID unico )
      </td>
    </tr>    
  <tbody>
</table>

<!-------- PARAMETERS -------->

###Authorization

🔑  &ensp; **Token JWT**


<!-------- PARAMETERS -------->

###Examples 


####Request
=== "Dart"

    ``` dart
    var response = await dio.post(
      'https://www.segcontrole.com.br/safer/v1/login.php',
      options: Options(
        headers: {
          'Authorization': 'Bearer <TOKEN JWT>',
        },
      ),
      data: {
        'usuario': 'teste@email.com',
        'senha': "123456",
        'token_push': "<TOKEN PUSH>",
        'token_voip': "<TOKEN VOIP>",
        'so': "IOS",
        'so_ver': "12.5.2",
        'app_id': 2,
      },
    );
    ```

<br/>
####Response
=== "JSON"

    ``` json
    {
        "data": {
            "info": "teste1", 
            "id": 226,
            "email": "teste1@email.com", 
            "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2YWwiOjE2MjYzNjQ4MTUsImRhdGEiOnsiaWQiOiIyMjYiLCJlbWFpbCI6InRlc3RlMUBlbWFpbC5jb20iLCJjZWxfaWQiOiI1NTkxIiwiYXBwX2lkIjoiMiJ9fQ.u1-pD78xeLpnWcTHIy6rJQIUabsiCYEZnFCJj6mqi0k",
            "code": 200
        },
    }
    ```





<!-- 0:"usuario" -> "91"
1:"senha" -> "teste1"
2:"token_push" -> "eMLmsTupIkMdmnI_0ntBcG:APA91bH4T1o9NqEtzeCtY57ifZKf3omDBcbVUezDw9_s0uLamnj0qnj-jbSdTOwaZB3c8HV60lPU23CYZjyMgMisAC6eq2m3C9JDg6V_H…"
3:"token_voip" -> "123"
4:"so" -> "iOS"
5:"so_ver" -> "12.5.2"
6:"app_id" -> 2 
"login.php"
-->


<!---=========================================== CADASTRO ===========================================--->
<br/>

---
##Cadastro de usuários

O processo de cadastro é baseado na confirmação do número de celular, via SMS. Sendo dividido em 3 etapas: 

- **Etapa 1 - Informar o número do celular.** ( Processado via requisição á API )
  Deve ser feita uma requisição ao servidor, passando o número de celular informado pelo usuário. Essa requisição irá retornar o PIN Code, que será usado no próximo passo. O pin code deve ser salvo localmente no front-end, para posteriormente ser comparado ao código informado pelo usuário. 

  </br>

- **Etapa 2 - Confirmar PIN Code recebido via sms.** ( Processado via frontend )
  Essa etapa não envolve requisição a API. A confirmação é feita pelo front-end, da seguinte forma: O usuário deve informar o código recebido via SMS, e o sistema deve verificar se esse código bate com código recebido na resposta da requisição da etapa 1. 

  </br>

- **Etapa 3 - Informar dados do usuário.** ( Processado via requisição á API )
   Requisição ao servidor, passando os dados do usuário ( User, senha, etc ). 

---


<!-----------------------  INFORM PHONE NUMBER ----------------------->
 

###[![Flattr this git repo](https://img.shields.io/badge/-POST-orange)]() Inform phone number 


- **Endpoint:** https://www.segcontrole.com.br/safer/v1/login.php

 <!-- [![Flattr this git repo](https://img.shields.io/badge/-POST-orange)]() -->
<!-------- PARAMETERS -------->

####Parametros


<table>
   <!-- HEADER -->
   <thead>
    <tr>
      <th scope="col">Parametro</th>
      <th scope="col">Tipo</th>
      <th scope="col">Descrição</th>
    </tr>
  </thead>
    </tr>
  <!---- DATA --->
  <tbody>
    <!---->
    <tr>
      <td >usuario</td>
      <td>STRING</td>
      <td>
      <b>Obrigatório</b> </br>
      Usuário utilizado para fazer o acesso(login). Nessa caso, o parametro usuario corresponde ao numero de celular usado no cadastro.</td>
    </tr>
    <!---->
    <tr>
      <td >senha</td>
      <td>STRING</td>
      <td>        <b>Obrigatório</b> </br>Senha de acesso do usuário.</td>
    </tr>
    <!---->
    <tr>
      <td >token_push</td>
      <td>STRING</td>
      <td>
      <b>Obrigatório</b> </br>      
      Token push gerado pelo firebase messaging. Utilizado para enviar notificações push para o usuário.</td>
    </tr>
    <!---->
    <tr>
      <td >token_voip</td>
      <td>STRING</td>
      <td>  
      <b>Obrigatório</b> </br>      
      Token de chamadas VOIP</td>
    </tr>
    <!---->
    <tr>
      <td >so</td>
      <td>STRING</td>
      <td>
      <b>Obrigatório</b> </br>
      Indica qual o sistema operacional em que o app esta instalado.</br>
      <b>Valores:</b> IOS / ANDROID 
      </td>
    </tr>    
    <!---->
    <tr>
      <td >so_ver</td>
      <td>STRING</td>
      <td>
      <b>Obrigatório</b> </br>
      Indica qual a versão do sistema operacional. 
      </td>
    </tr>  
    <!---->
    <tr>
      <td >app_id</td>
      <td>INT</td>
      <td>
      <b>Obrigatório</b> </br>
      ID do aplicativo. ( Cada aplicativo da familia Safer tem seu ID unico )
      </td>
    </tr>    
  <tbody>
</table>

<!-------- PARAMETERS -------->

####Authorization

🔑  &ensp; **Token JWT**


<!-------- PARAMETERS -------->

####Example Request 

=== "Dart"

    ``` dart
    var response = await dio.post(
      'https://www.segcontrole.com.br/safer/v1/login.php',
      options: Options(
        headers: {
          'Authorization': 'Bearer <TOKEN JWT>',
        },
      ),
      data: {
        'usuario': 'teste@email.com',
        'senha': "123456",
        'token_push': "<TOKEN PUSH>",
        'token_voip': "<TOKEN VOIP>",
        'so': "IOS",
        'so_ver': "12.5.2",
        'app_id': 2,
      },
    );
    ```

<br/>
####Example Response 
=== "JSON"

    ``` json
    {
        "data": {
            "info": "teste1", 
            "id": 226,
            "email": "teste1@email.com", 
            "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2YWwiOjE2MjYzNjQ4MTUsImRhdGEiOnsiaWQiOiIyMjYiLCJlbWFpbCI6InRlc3RlMUBlbWFpbC5jb20iLCJjZWxfaWQiOiI1NTkxIiwiYXBwX2lkIjoiMiJ9fQ.u1-pD78xeLpnWcTHIy6rJQIUabsiCYEZnFCJj6mqi0k",
            "code": 200
        },
    }
    ```