<h1 align="center">Personal Organizers</h1>

Fake API a base de JSON-Server + JSON-Server-Auth, feita para ser usada no desenvolvimento das API's nos Capstones do Q2.

A url base da API é

//add insomnia btn

<br/>

<h2 align="center"> Criação de usuário </h2>

```
POST /register - FORMATO DA REQUISIÇÃO
```

<br/>

```
 {
      "name": "Teste",
      "email": "teste@gmail.com",
      "password": "123456",
      "confirmPassword": "123456",
      "urlPicture": "https://br.freepik.com/fotos-gratis/o-gato-vermelho-ou-branco-eu-no-estudio-branco_9405869.htm#query=gato&position=0&from_view=keyword&track=sph"
    }
```

<br/>

Caso dê tudo certo, a resposta será assim:

```
POST /users - FORMATO DA RESPOSTA - STATUS 201
```

```
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImF5YUBnbWFpbC5jb20iLCJpYXQiOjE2Nzk0MjU3NDIsImV4cCI6MTY3OTQyOTM0Miwic3ViIjoiMiJ9.8Yvti0qw0LRGKDbWNjWCc3FeZtE4bkCC_7Yi0_DQ4Lo",
	"user": {
		"email": "teste@gmail.com",
		"name": "Teste",
		"confirmPassword": "123456",
		"urlPicture": "https://br.freepik.com/fotos-gratis/o-gato-vermelho-ou-branco-eu-no-estudio-branco_9405869.htm#query=gato&position=0&from_view=keyword&track=sph",
		"id": 2
	}
}
```

<br/>

<h2 align="center">Possíveis erros </h2>

Caso você acabe errando e mandando algum campo errado, a resposta de erro será assim:

A senha necessita de 6 caracteres.

`POST /users -   FORMATO DA RESPOSTA - STATUS 400`

`"Password is too short"`

<br/>

Email já cadastrado:

`POST /users -   FORMATO DA RESPOSTA - STATUS 400`

`"Email already exists"`

<br/>

<h2 align="center">Login</h2>

`POST /login - FORMATO DA REQUISIÇÃO`

```
{
  "email": "admin@mail.com",
  "password": "123456"
}
```

Caso dê tudo certo, a resposta será assim:

`POST /login - FORMATO DA RESPOSTA - STATUS 200`

```
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImFkbWluQG1haWwuY29tIiwiaWF0IjoxNjc5NDI1NjcxLCJleHAiOjE2Nzk0MjkyNzEsInN1YiI6IjEifQ.taFUGmX2lLQVbqZfNoVd5yvPRziFnmaz7ZIOFsR28B8",
	"user": {
		"email": "admin@mail.com",
		"name": "Admin",
		"urlPicture": "https://br.freepik.com/fotos-gratis/o-gato-vermelho-ou-branco-eu-no-estudio-branco_9405869.htm#query=gato&position=0&from_view=keyword&track=sph",
		"id": 1
	}
}
```

<br/>

Com essa resposta, vemos que temos duas informações, o user e o token respectivo, dessa forma você pode guardar o token no localStorage para fazer a gestão do usuário no seu frontend.

<br/>

<h2 align="center">Rotas que necessitam de autorização</h2>

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

Authorization: Bearer {token} Após o usuário estar logado, ele deve conseguir buscar os produtos da borscht house:

<br/>

<h2 align="center">Auto login</h2>

`GET /users/{userId}`

É necessario o Authorization: Bearer {token}.

<br/>

Não é necessário um corpo da requisição.

Caso dê tudo certo, a resposta será assim:

```
{
	"email": "teste@mail.com",
	"password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOhkuyt7FO",
	"name": "teste",
	"id": 2,
	"urlPicture": "https://br.freepik.com/fotos-gratis/o-gato-vermelho-ou-branco-eu-no-estudio-branco_9405869.htm#query=gato&position=0&from_view=keyword&track=sph",
}
```

<br/>

<h2 align="center">Editar Usuario</h2>

`PATCH /users/{userId}`

É necessario o Authorization: Bearer {token}.

```
{
  "urlPicture": "https://br.freepik.com/fotos-gratis/o-gato-vermelho-ou-branco-eu-no-estudio-branco_9405869.htm#query=gato&position=0&from_view=keyword&track=sph"
}
```

Caso dê tudo certo, a resposta será assim:

`GET /products - FORMATO DA RESPOSTA - STATUS 200`
<br/>

```
{
	"email": "teste@gmail.com",
	"password": "$2a$10$2VCkYSrs1vDUagvaN.JnpuRdK2gH5Mf71aWDgi84gk5vb7pKGV2Uy",
	"name": "Teste",
	"urlPicture": "https://br.freepik.com/fotos-gratis/o-gato-vermelho-ou-branco-eu-no-estudio-branco_9405869.htm#query=gato&position=0&from_view=keyword&track=sph",
	"id": 2
}
```

<br/>

<h2 align="center">Deletar Usuario</h2>

É necessario o Authorization: Bearer {token}.

`DELETE /users/{userId}`

<br/>
Não é necessário um corpo da requisição.

Caso dê tudo certo, a resposta será assim:

`{}`

<br/>

<h2 align="center">Tarefas</h2>

É necessario o Authorization: Bearer {token}.

`GET /tasks`

Não é necessário um corpo da requisição.
Caso dê tudo certo, a resposta será assim:

`GET /tasks - FORMATO DA RESPOSTA - STATUS 200`

```
[
	  {
      "title": "Responder Email",
      "category": "Anotações",
      "date": "12/05/2023",
      "description": "Responder emails da Laura",
      "value": null,
      "id": 1
    },
    {...}
]

```

<br/>

<h2 align="center">Editar Tarefas</h2>

É necessario o Authorization: Bearer {token}.

`GET /tasks{taskId}`

é necessário um corpo da requisição. Porem esta em desenvolvimento

Caso dê tudo certo, a resposta será assim:

`GET /tasks - FORMATO DA RESPOSTA - STATUS 200`

```
[
	  {
      "title": "Responder Email",
      "category": "Anotações",
      "date": "12/05/2023",
      "description": "Responder emails da Laura",
      "value": null,
      "id": 1
    },
    {...}
]
```

<br/>

<h2 align="center">Deletar Tarefas</h2>

É necessario o Authorization: Bearer {token}.

`DELETE /tasks{taskId}`

é necessário um corpo da requisição. Porem esta em desenvolvimento

Caso dê tudo certo, a resposta será assim:

`GET /tasks - FORMATO DA RESPOSTA - STATUS 200`

```
{}

```
