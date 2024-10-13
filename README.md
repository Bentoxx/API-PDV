# API de Ponto de Venda (PDV) - NestJS, Prisma, PostgreSQL, Docker

## Descrição

Este projeto é uma **API** para um sistema de Ponto de Venda (PDV) desenvolvida com **NestJS**, utilizando **Prisma** como ORM e **PostgreSQL** como banco de dados. A API permite o gerenciamento de usuários, produtos, categorias, clientes e pedidos, além de fornecer autenticação via **JWT**. Ela foi desenvolvida com as melhores práticas de segurança, escalabilidade e desempenho, e é totalmente integrada com **Docker** para facilitar o desenvolvimento e o deploy.

## Tecnologias Utilizadas

- **Typescript** - Linguagem utilizada no projeto.
- **NestJS** - Framework Node.js para construção de APIs escaláveis e robustas.
- **Prisma** - ORM para interagir com o banco de dados de maneira intuitiva e segura.
- **PostgreSQL** - Banco de dados relacional utilizado para persistência de dados.
- **JWT** - Token para autenticação segura dos usuários.
- **Docker** - Containerização do ambiente para garantir consistência entre desenvolvimento e produção.
- **BCrypt** - Biblioteca para criptografia de senhas.

## Funcionalidades

A API oferece as seguintes funcionalidades principais:

- **Usuários**:
  - Cadastro de novos usuários.
  - Login de usuários com autenticação JWT.
  - Atualização de perfil e redefinição de senha.
  
- **Categorias**:
  - Listagem de categorias previamente cadastradas.

- **Produtos**:
  - CRUD de produtos com integração a categorias.
  - Upload de imagens de produtos.
  - Validação de estoque e exclusão segura (não permite exclusão de produtos vinculados a pedidos).

- **Clientes**:
  - CRUD de clientes com validação de e-mail e CPF únicos.
  
- **Pedidos**:
  - Cadastro de pedidos com múltiplos produtos e cálculo automático do valor total.

## Pré-requisitos

Antes de começar, você precisará ter as seguintes ferramentas instaladas:

- [Node.js](https://nodejs.org/en/) - Versão 16.x ou superior.
- [Docker](https://www.docker.com/) - Para rodar o ambiente de desenvolvimento em containers.
- [PostgreSQL](https://www.postgresql.org/) - Caso queira rodar o banco de dados localmente.

## Instalação

### Passos para rodar o projeto:

1. Clone este repositório:
   ```bash
   git clone https://github.com/seuusuario/seuprojeto.git
   cd seuprojeto
   ```

2. Crie um arquivo .env baseado no .env.example:
  ```bash
  cp .env.example .env
  ```
3. Configure suas variáveis de ambiente no arquivo .env (ex: configuração do banco de dados, JWT secret, etc.).

4. Inicie os containers Docker:
  ```bash
  docker-compose up -d
  ```

5. Instale as dependências dos projeto:
  ```bash
  npm install
  ````

6. Execute as migrações do Prisma para criar o esquema do banco de dados:
  ```bash
  npx prisma migrate dev
  ````

7. Inicie a aplicação:
  ```bash
  npm run start:dev
  ```

###Estrutura de Arquivos
Abaixo está uma visão geral da estrutura de arquivos do projeto:
  ```bash
  .
├── src
│   ├── app.module.ts            # Módulo principal da aplicação
│   ├── main.ts                  # Arquivo de entrada da aplicação
│   ├── auth                     # Módulo de autenticação (JWT)
│   │   ├── auth.module.ts
│   │   ├── auth.service.ts
│   │   └── jwt.strategy.ts
│   ├── usuarios                 # Módulo de usuários
│   │   ├── usuarios.controller.ts
│   │   ├── usuarios.service.ts
│   │   ├── dto
│   │   │   ├── create-usuario.dto.ts
│   │   │   └── update-usuario.dto.ts
│   ├── produtos                 # Módulo de produtos
│   ├── categorias               # Módulo de categorias
│   ├── clientes                 # Módulo de clientes
│   └── pedidos                  # Módulo de pedidos
├── prisma
│   ├── schema.prisma            # Definição do esquema Prisma
│   └── migrations               # Migrações geradas pelo Prisma
├── docker-compose.yml           # Configuração do Docker
├── Dockerfile                   # Dockerfile da aplicação
├── package.json                 # Configurações e dependências do Node.js
└── README.md                    # Documentação do projeto
````
Endpoints
Autenticação
POST /login
Realiza o login do usuário e retorna um token JWT.
Usuários
POST /usuarios
Cadastra um novo usuário.

GET /usuarios
Detalha o perfil do usuário autenticado.

PATCH /usuarios/redefinir
Redefine a senha do usuário autenticado.

Categorias
GET /categorias
Lista todas as categorias cadastradas.
Produtos
POST /produtos
Cadastra um novo produto.

GET /produtos
Lista todos os produtos cadastrados.

GET /produtos/:id
Detalha um produto específico.

DELETE /produtos/:id
Exclui um produto, desde que ele não esteja vinculado a nenhum pedido.

Clientes
POST /clientes
Cadastra um novo cliente.

GET /clientes
Lista todos os clientes cadastrados.

GET /clientes/:id
Detalha um cliente específico.

Pedidos
POST /pedidos
Cadastra um novo pedido com múltiplos produtos.

GET /pedidos
Lista todos os pedidos cadastrados.

Segurança
Autenticação JWT: Todos os endpoints (exceto login e cadastro) exigem um token JWT válido.
BCrypt: Todas as senhas são criptografadas antes de serem armazenadas no banco de dados.

Contribuição
Contribuições são bem-vindas! Por favor, siga os passos abaixo:

Faça um fork do projeto.
Crie uma branch para sua feature (git checkout -b feature/nova-feature).
Commit suas alterações (git commit -m 'Adiciona nova feature').
Envie sua branch para o repositório remoto (git push origin feature/nova-feature).
Abra um Pull Request.