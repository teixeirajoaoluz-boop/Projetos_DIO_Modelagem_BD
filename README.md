# Projetos_DIO_Modelagem_BD

# 🛒 Sistema de Banco de Dados para E‑commerce  
### Modelo Relacional + Refinamentos (Cliente PF/PJ, Pagamento, Entrega)

Este projeto apresenta o modelo de banco de dados para um sistema de **e‑commerce**, incluindo entidades principais, relacionamentos, regras de negócio e refinamentos estruturais. O objetivo é fornecer uma base sólida para implementação em SGBDs como MySQL, PostgreSQL ou SQL Server.

---

## 📌 Visão Geral do Projeto

O banco de dados foi projetado para atender às necessidades de um e‑commerce completo, incluindo:

- Cadastro de clientes (Pessoa Física e Jurídica)  
- Gestão de produtos, fornecedores e vendedores terceiros  
- Controle de estoque e localização  
- Registro de pedidos e itens do pedido  
- Múltiplas formas de pagamento  
- Acompanhamento de entrega com rastreamento  

---

## 🧱 Entidades Principais

### **Cliente**
Armazena informações comuns a qualquer tipo de cliente.

| Campo | Tipo | Descrição |
|-------|------|-----------|
| idCliente | INT | Identificador único |
| endereco | VARCHAR(45) | Endereço completo |
| dataNascimento | DATE | Data de nascimento (PF) ou fundação (PJ) |

---

## 👤 Especialização: Cliente PF e Cliente PJ

Para garantir que um cliente seja **Pessoa Física OU Jurídica**, mas nunca ambos, foi aplicada **especialização total e exclusiva**.

### **ClientePF**
| Campo | Tipo |
|-------|------|
| idCliente (PK/FK) | INT |
| Pnome | VARCHAR(10) |
| Nome_do_meio | VARCHAR(10) |
| Sobrenome | VARCHAR(20) |
| CPF | CHAR(11) UNIQUE |

### **ClientePJ**
| Campo | Tipo |
|-------|------|
| idCliente (PK/FK) | INT |
| RazaoSocial | VARCHAR(45) |
| CNPJ | CHAR(15) UNIQUE |

---

## 📦 Produto

| Campo | Tipo |
|-------|------|
| idProduto | INT |
| Categoria | VARCHAR(45) |
| Descrição | VARCHAR(45) |
| Valor | DECIMAL |

---

## 🏬 Fornecedor

| Campo | Tipo |
|-------|------|
| idFornecedor | INT |
| Razão Social | VARCHAR(45) |
| CNPJ | CHAR(15) UNIQUE |
| Contato | VARCHAR(45) |

---

## 🛍️ Vendedor Terceiro

| Campo | Tipo |
|-------|------|
| idTerceiro | INT |
| Razão Social | VARCHAR(45) |
| Nome Fantasia | VARCHAR(45) |
| CNPJ | CHAR(15) UNIQUE |
| CPF | CHAR(11) UNIQUE |

---

## 📦 Estoque e Localização

### **Estoque**
| Campo | Tipo |
|-------|------|
| idEstoque | INT |
| Local | VARCHAR(45) |
| Quantidade | INT |

### **Produto_em_Estoque**
Relaciona produtos com locais de estoque.

| Campo | Tipo |
|-------|------|
| Produto_idProduto | INT |
| Estoque_idEstoque | INT |
| Localização | VARCHAR(45) |

---

## 🔗 Relacionamentos de Produto

### **Produto_fornecedor**
Define quais fornecedores fornecem quais produtos.

### **Produtos_vendedor**
Relaciona produtos vendidos por terceiros.

---

## 🧾 Pedido

| Campo | Tipo |
|-------|------|
| idPedido | INT |
| Status | ENUM(...) |
| Descrição | VARCHAR(45) |
| Cliente_idCliente | INT |
| Frete | FLOAT |

---

## 📦 Itens do Pedido

Tabela intermediária entre Pedido e Produto.

| Campo | Tipo |
|-------|------|
| Produto_idProduto | INT |
| Pedido_idPedido | INT |
| Quantidade | INT |
| Status | ENUM(...) |

---

# 💳 Refinamento 1: Múltiplas Formas de Pagamento

Um pedido pode ter **uma ou mais formas de pagamento**.

### **Pagamento**
| Campo | Tipo |
|-------|------|
| idPagamento | INT |
| tipoPagamento | ENUM('Cartão de Crédito','Boleto','Pix','Transferência') |
| detalhes | VARCHAR(100) |

### **Pedido_Pagamento**
Relacionamento N:N entre Pedido e Pagamento.

| Campo | Tipo |
|-------|------|
| idPedido | INT |
| idPagamento | INT |

---

# 🚚 Refinamento 2: Entrega com Status e Rastreamento

Cada pedido pode ter uma entrega associada.

### **Entrega**
| Campo | Tipo |
|-------|------|
| idEntrega | INT |
| idPedido | INT UNIQUE |
| statusEntrega | ENUM('Em preparação','Enviado','Em trânsito','Entregue','Cancelado') |
| codigoRastreio | VARCHAR(30) |

---

# 🧩 Resumo dos Refinamentos Aplicados

- ✔ Cliente agora possui especialização PF/PJ garantindo exclusividade  
- ✔ Pedido pode ter múltiplas formas de pagamento  
- ✔ Entrega possui status e código de rastreio  
- ✔ Modelo atualizado segue boas práticas de normalização  

---

# 📘 Como Usar Este Modelo

Você pode:

- Implementar o banco em MySQL, PostgreSQL ou SQL Server  
- Criar o DER com base nas tabelas acima  
- Expandir o sistema para incluir carrinho, cupons, avaliações etc.  
  
