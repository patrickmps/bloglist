# BlogList API

![bloglist-api](https://github.com/patrickmps/bloglist/assets/58093259/41c6893e-ffe8-45e2-8ce5-cde5b6433c70)

<div align="center">
  
![MongoDB](https://img.shields.io/badge/MongoDB-%234ea94b.svg?style=for-the-badge&logo=mongodb&logoColor=white)
![NodeJS](https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white)
![Nodemon](https://img.shields.io/badge/NODEMON-%23323330.svg?style=for-the-badge&logo=nodemon&logoColor=%BBDEAD)
![Express.js](https://img.shields.io/badge/express.js-%23404d59.svg?style=for-the-badge&logo=express&logoColor=%2361DAFB)
![NPM](https://img.shields.io/badge/NPM-%23CB3837.svg?style=for-the-badge&logo=npm&logoColor=white)
![Visual Studio Code](https://img.shields.io/badge/Visual%20Studio%20Code-0078d7.svg?style=for-the-badge&logo=visual-studio-code&logoColor=white)
![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)
![Jest](https://img.shields.io/badge/-jest-%23C21325?style=for-the-badge&logo=jest&logoColor=white)
![Git](https://img.shields.io/badge/git-%23F05033.svg?style=for-the-badge&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)

</div>

## Sobre

O BlogList API permite aos usuários salvar informações sobre blogs interessantes que encontram pela internet. Com o BlogList, você pode criar sua própria biblioteca pessoal de blogs favoritos, mantendo o controle de autores, títulos, URLs e a quantidade de votos positivos de outros usuários da aplicação.

## Rodando localmente

Clone o projeto

```bash
  git clone https://github.com/patrickmps/bloglist.git
```

Entre no diretório do projeto

```bash
  cd bloglist
```

Instale as dependências

```bash
  npm install
```

Inicie o servidor

```bash
  npm start
```

## Variáveis de Ambiente

Para rodar esse projeto, você vai precisar adicionar as seguintes variáveis de ambiente no seu .env

`MONGODB_URI` - uri do banco MongoDB

`PORT` - porta na qual irá rodar o server, por padrão está 3001

`TEST_MONGODB_URI` - uri do banco MongoDB para testes

`SECRET` - string usada para gerar o token JWT

## Documentação da API

### Blogs

#### Retorna todos os blogs

```http
  GET /api/blogs
```

- Response 200 (application/json)

      [
        {
          "title": "React patterns",
          "author": "Michael Chan",
          "url": "https://reactpatterns.com/",
          "likes": 7,
          "user": {
            "username": "root",
            "name": "Superuser",
            "id": "65232e0901ea275e5bc8531b"
          },
          "id": "6523554c0aa5a2931c23e086"
        },
        {
          "title": "React patterns",
          "author": "Michael Chan",
          "url": "https://reactpatterns.com/",
          "likes": 7,
          "user": {
            "username": "root",
            "name": "Superuser",
            "id": "65232e0901ea275e5bc8531b"
          },
          "id": "652359374dd34402dbb0321c"
        },
      ...
      ]

#### Adiciona um blog

```http
  POST /api/blogs
```

- Request (application/json)

  - Headers

          Authorization: Bearer [access_token]

  - Body

        {
          "title": "Tulio Calil Dev",
          "author": "Tulio Calil",
          "url": "https://tuliocalil.com",
          "likes": 29
        }

- Response 201 (application/json)

      {
        "title": "Tulio Calil Dev",
        "author": "Tulio Calil",
        "url": "https://tuliocalil.com",
        "likes": 29,
        "user": "652be8b022111afd709708b5",
        "id": "652d7c3d3839ac5b34e1d3ad"
      }

#### Retorna um blog

```http
  GET /api/blogs/${id}
```

| Parâmetro | Tipo     | Descrição                                   |
| :-------- | :------- | :------------------------------------------ |
| `id`      | `string` | **Obrigatório**. O ID do blog que você quer |

- Response 200 (application/json)

      {
        "title": "Tulio Calil Dev",
        "author": "Tulio Calil",
        "url": "https://tuliocalil.com",
        "likes": 29,
        "user": "652be8b022111afd709708b5",
        "id": "652d7c3d3839ac5b34e1d3ad"
      }

#### Atualiza um blog

```http
  PUT /api/blogs/${id}
```

| Parâmetro | Tipo     | Descrição                                   |
| :-------- | :------- | :------------------------------------------ |
| `id`      | `string` | **Obrigatório**. O ID do blog que você quer |

- Request (application/json)

  - Body

        {
          "likes": 35
        }

- Response 200 (application/json)

      {
        "title": "Tulio Calil Dev",
        "author": "Tulio Calil",
        "url": "https://tuliocalil.com",
        "likes": 35,
        "user": "652be8b022111afd709708b5",
        "id": "652d7c3d3839ac5b34e1d3ad"
      }

#### Deleta um blog

```http
  DEL /api/blogs/${id}
```

| Parâmetro | Tipo     | Descrição                                   |
| :-------- | :------- | :------------------------------------------ |
| `id`      | `string` | **Obrigatório**. O ID do blog que você quer |

**Obs.:** para deletar um blog é preciso ser o usuário que o adicionou.

- Request (application/json)

  - Headers

          Authorization: Bearer [access_token]

- Response 204

### Users

#### Retorna todos os usuários

```http
  GET /api/users
```

- Response 200 (application/json)

      [
        {
          "username": "root",
          "name": "Superuser",
          "blogs": [
            {
              "title": "React patterns",
              "author": "Michael Chan",
              "url": "https://reactpatterns.com/",
              "likes": 7,
              "id": "652359374dd34402dbb0321c"
            }
          ]
        },
        {
          "username": "superroot",
          "name": "Superuser",
          "blogs": [],
          "id": "652c592fe49c2dc01a25c681"
        }
      ]

#### Cria um usuário

```http
  POST /api/users
```

- Request (application/json)

  - Body

        {
        	"username": "patrickmps",
        	"name": "Patrick Mota",
        	"password": "senha321"
        }

- Response 201 (application/json)

      {
      	"username": "patrickmps",
      	"name": "Patrick Mota",
      	"blogs": [],
      	"id": "652d88d5b79d74c37e6ce558"
      }

### Login

#### Faz login na api

```http
  POST /api/login
```

- Request (application/json)

  - Body

        {
        	"username": "patrickmps",
        	"password": "senha321"
        }

- Response 201 (application/json)

      {
      	"token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImthbGlsMzIiLCJpZCI6IjY1MmJlOGIwMjIxMTFhZmQ3MDk3MDhiNSIsImlhdCI6MTY5NzQ3OTYyMSwiZXhwIjoxNjk3NDgzMjIxfQ.xkOd_EdpfdIs_cbNJInwEWmrPKauLCOznyYL8zFnSII",
      	"username": "patrickmps",
      	"name": "Patrick Mota"
      }

## Rodando os testes

Para rodar os testes, rode o seguinte comando

```bash
  npm run test
```

## Licença

[MIT](https://choosealicense.com/licenses/mit/)
