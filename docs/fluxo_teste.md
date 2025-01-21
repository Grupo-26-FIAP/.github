# Usuários para Testes

- **Usuário Administrador**

  - E-mail: admin@gmail.com
  - Senha: admin@123

- **Usuário Cozinha**

  - E-mail: cozinha@gmail.com
  - Senha: cozinha@123

- **Usuário Cliente**
  - CPF: 35281866079

---

# Fluxo de Cliente

1. **POST /auth/identify/customer**

   - Inserir um CPF válido.
   - Copiar o token retornado.
   - Adicioná-lo no authorize do Swagger.

2. **GET /products** - Executar a listagem de produtos.

   - Escolher o ID dos produtos para utilizar no pedido.

3. **POST /order** - Fazer o pedido com os produtos selecionados.

   - Inserir o CPF do cliente (se for se identificar).
   - Inserir os IDs dos produtos com a quantidade respectiva.

4. **POST /checkout** - Simulação de pagamento do pedido.
   - Realiza o pagamento e altera o status do pedido para `RECEIVED` (fica visível para cozinha).

> Para gerar CPFs válidos: [Gerador de CPF](https://www.4devs.com.br/gerador_de_cpf)

- **O pedido será aprovado ou não baseado no CPF:**
  - **CPF:** 52998224725 - Aprova o pedido.
  - **CPF:** 11144477735 - Nega o pedido.
  - **CPF:** Qualquer outro CPF (válido) aprova o pedido.

---

# Fluxo da Cozinha

1. **POST /auth/login**

   - Inserir o e-mail e senha do usuário da linha de produção.
   - Copiar o token retornado.
   - Adicioná-lo no authorize do Swagger.

2. **GET /orders** - Lista os pedidos de acordo com a role do usuário autenticado.

   - Serão exibidos todos os pedidos com status diferente de `none` e `finished`.

3. **PUT /orders**
   - Inserir o status de atualização do pedido (`received`, `in_preparation`, `ready`, `finished`).

---

# Acompanhamento do Pedido

_O cliente poderá acompanhar o andamento do seu pedido através de um monitor no estabelecimento._

1. **POST /auth/login**

   - Inserir o e-mail e senha do usuário de administrador.
   - Copiar o token retornado.
   - Adicioná-lo no authorize do Swagger.

2. **GET /orders** - Lista os pedidos de acordo com a role do usuário autenticado.
   - Serão exibidos todos os pedidos.

---

# Administrador

O administrador pode gerenciar todo o sistema, atualizar pedido, produto, categoria...
