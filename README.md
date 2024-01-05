# **Documentação da API de um sistema de restaurante .**

Esta documentação fornece informações detalhadas sobre a API desenvolvida. Certifique-se de seguir as instruções fornecidas para garantir o correto funcionamento das diferentes funcionalidades.

## **Sumário**

1. [Introdução](#introdução)
2. [Endpoints](#endpoints)
    1. [Usuários](#usuários)
    2. [Pratos](#pratos)
    3. [Sessões](#sessões)
3. [Autenticação e Autorização](#autenticação-e-autorizão)

## **Introdução**

A API foi desenvolvida para gerenciar informações sobre pratos, usuários e sessões. Ela oferece operações básicas de criação, leitura, atualização e exclusão (CRUD) para entidades como pratos e usuários. Além disso, inclui autenticação para usuários e controle de acesso para operações específicas.

## **Endpoints**

### **Usuários**

### 1. Criação de Usuário

- **Endpoint:** **`POST /users`**
- **Descrição:** Cria um novo usuário no sistema.
- **Parâmetros do Corpo (JSON):**
    - **`name`** (string): Nome do usuário.
    - **`email`** (string): E-mail do usuário.
    - **`password`** (string): Senha do usuário.
- **Códigos de Resposta:**
    - 201: Usuário criado com sucesso.
    - 400: Erro de validação ou usuário já existente.

### **Pratos**

### 1. Criação de Prato

- **Endpoint:** **`POST /plates`**
- **Descrição:** Cria um novo prato no sistema.
- **Autenticação Necessária:** Sim (somente administradores).
- **Parâmetros do Corpo (Multipart):**
    - **`title`** (string): Título do prato.
    - **`description`** (string): Descrição do prato.
    - **`ingredients`** (string ou array de strings): Ingredientes do prato.
    - **`category`** (string): Categoria do prato.
    - **`price`** (string): Preço do prato.
    - **`image`** (arquivo): Imagem do prato.
- **Códigos de Resposta:**
    - 201: Prato criado com sucesso.
    - 400: Erro de validação.
    - 401: Acesso não autorizado.

### 2. Atualização de Prato

- **Endpoint:** **`PUT /plates/:id`**
- **Descrição:** Atualiza informações de um prato existente.
- **Autenticação Necessária:** Sim (somente administradores).
- **Parâmetros do Corpo (Multipart):**
    - **`title`** (string): Título do prato.
    - **`description`** (string): Descrição do prato.
    - **`ingredients`** (string ou array de strings): Ingredientes do prato.
    - **`category`** (string): Categoria do prato.
    - **`price`** (string): Preço do prato.
    - **`image`** (arquivo): Nova imagem do prato (opcional).
- **Códigos de Resposta:**
    - 200: Prato atualizado com sucesso.
    - 400: Erro de validação.
    - 401: Acesso não autorizado.

### 3. Listagem de Pratos

- **Endpoint:** **`GET /plates`**
- **Descrição:** Lista todos os pratos disponíveis no sistema.
- **Parâmetros da Consulta (Query String):**
    - **`title`** (string): Filtra pratos por título.
    - **`ingredients`** (string): Filtra pratos por ingredientes (separados por vírgula).
- **Códigos de Resposta:**
    - 200: Lista de pratos recuperada com sucesso.

### 4. Detalhes de Prato

- **Endpoint:** **`GET /plates/:id`**
- **Descrição:** Retorna detalhes de um prato específico.
- **Códigos de Resposta:**
    - 200: Detalhes do prato recuperados com sucesso.
    - 404: Prato não encontrado.

### 5. Exclusão de Prato

- **Endpoint:** **`DELETE /plates/:id`**
- **Descrição:** Exclui um prato do sistema.
- **Autenticação Necessária:** Sim (somente administradores).
- **Códigos de Resposta:**
    - 200: Prato excluído com sucesso.
    - 401: Acesso não autorizado.
    - 404: Prato não encontrado.

### **Sessões**

### 1. Autenticação

- **Endpoint:** **`POST /sessions`**
- **Descrição:** Autentica um usuário no sistema e gera um token JWT.
- **Parâmetros do Corpo (JSON):**
    - **`email`** (string): E-mail do usuário.
    - **`password`** (string): Senha do usuário.
- **Códigos de Resposta:**
    - 200: Autenticação bem-sucedida. Retorna informações do usuário e token JWT.
    - 401: E-mail ou senha incorretos.

## **Autenticação e Autorização**

A API utiliza tokens JWT para autenticação de usuários. Além disso, existem níveis de acesso, onde apenas administradores têm permissão para realizar certas operações, como criar ou atualizar pratos.

- **Token JWT:** O token JWT deve ser incluído no cabeçalho **`Authorization`** para acessar endpoints autenticados.
- **Níveis de Acesso:**
    - **Usuário comum:** Pode autenticar-se e acessar pratos.
    - **Administrador:** Além das permissões do usuário comum, pode criar, atualizar e excluir pratos.

**Observação:** Certifique-se de armazenar e gerenciar adequadamente os tokens JWT para garantir a segurança da aplicação.

Essa documentação fornece uma visão geral da API e de suas operações principais. Certifique-se de adaptar conforme necessário, considerando futuras atualizações e requisitos específicos do projeto.
