# 🍺  **DESAFIO DE PROJETO DIO x HEINEKEN** 🍺  


# 📦 Projeto de Banco de Dados Relacional | E-commerce


## 📝 Descrição do Projeto

Este projeto simula a estrutura de um banco de dados relacional para uma aplicação de e-commerce. Foi desenvolvido com foco educacional, para demonstrar boas práticas de modelagem de dados, criação de tabelas, inserção de dados e execução de consultas SQL simples e avançadas.

O banco simula funcionalidades comuns de um sistema de e-commerce: cadastro de clientes, produtos, categorias, pedidos, itens de pedidos e pagamentos.

> **Objetivo:** Demonstrar domínio de SQL (DDL + DML + consultas), modelagem relacional e organização de projetos de dados para fins de portfólio.

---

## 🗂️ Esquema do Banco de Dados 

Contém a definição das seguintes tabelas relacionais:

- `clientes`
- `categorias`
- `produtos`
- `pedidos`
- `itens_pedido`
- `pagamentos`

Chaves primárias e estrangeiras foram criadas conforme o modelo de negócio.

---

## 🧪  Tabelas x Relacionamentos

### 🔹 Tabela `clientes`
### 🔹 Tabela `categorias`
### 🔹 Tabela `produtos`
### 🔹 Tabela `pedidos`
### 🔹 Tabela `itens_pedido` 
### 🔹 Tabela `pagamentos`
### 🔹 Tabela `fornecedores`
 
## 🧩 Relacionamentos

- Cada **cliente** pode fazer vários **pedidos**
- Cada **pedido** pode ter vários **itens de pedido**
- Cada **item de pedido** está relacionado a um **produto**
- Cada **produto** pertence a uma **categoria**
- Cada **pedido** pode ter um **pagamento**


[LINK PARA O MODELO AQUI] (https:// https://github.com/SMGC-GIT/Projeto_Logico_de_BD_ECOMMERCE/diagrama.png)

[📎 Clique aqui para ver o diagrama do banco de dados]([img/diagrama.png](https://github.com/SMGC-GIT/Projeto_Logico_de_BD_ECOMMERCE/blob/main/diagrama.png))

---


## 📦 Estrutura do Banco de Dados (Schema)

O banco de dados foi modelado para representar um sistema de e-commerce completo, com entidades como clientes, produtos, categorias, pedidos, itens de pedidos, pagamentos, fornecedores e o relacionamento entre produtos e fornecedores.

Abaixo está o esquema lógico com os comandos SQL para criação das tabelas:

```sql
-- Criação das tabelas do banco de dados de e-commerce

🔹 Tabela `clientes`
CREATE TABLE clientes (
    id_cliente INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    telefone VARCHAR(20),
    endereco VARCHAR(255),
    data_cadastro DATE DEFAULT CURRENT_DATE
);

🔹 Tabela `categorias`
CREATE TABLE categorias (
    id_categoria INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    descricao TEXT
);

🔹 Tabela `produtos`
CREATE TABLE produtos (
    id_produto INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    descricao TEXT,
    preco DECIMAL(10, 2) NOT NULL,
    estoque INT DEFAULT 0,
    id_categoria INT,
    FOREIGN KEY (id_categoria) REFERENCES categorias(id_categoria)
);

🔹 Tabela `pedidos`
CREATE TABLE pedidos (
    id_pedido INT PRIMARY KEY,
    id_cliente INT,
    data_pedido DATE DEFAULT CURRENT_DATE,
    status VARCHAR(50),
    valor_total DECIMAL(10, 2),
    FOREIGN KEY (id_cliente) REFERENCES clientes(id_cliente)
);

🔹 Tabela `itens_pedido`
CREATE TABLE itens_pedido (
    id_item_pedido INT PRIMARY KEY,
    id_pedido INT,
    id_produto INT,
    quantidade INT NOT NULL,
    preco_unitario DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (id_pedido) REFERENCES pedidos(id_pedido),
    FOREIGN KEY (id_produto) REFERENCES produtos(id_produto)
);

🔹 Tabela `pagamentos`
CREATE TABLE pagamentos (
    id_pagamento INT PRIMARY KEY,
    id_pedido INT,
    data_pagamento DATE,
    valor_pago DECIMAL(10, 2),
    forma_pagamento VARCHAR(50),
    status_pagamento VARCHAR(50),
    FOREIGN KEY (id_pedido) REFERENCES pedidos(id_pedido)
);

🔹 Tabela `fornecedores`
CREATE TABLE fornecedores (
    id_fornecedor INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    contato VARCHAR(100),
    telefone VARCHAR(20),
    email VARCHAR(100),
    endereco VARCHAR(255)
);
```

---

## 🧪 Inserção de Dados

Inclui dados fictícios para simular a operação de um e-commerce com:

- 4 clientes
- 3 categorias de produtos
- 5 produtos
- 3 pedidos (vinculados aos clientes)
- 4 itens de pedidos
- 3 pagamentos
- 3 fornecedores

---

## 📄 Inserção de dados nas tabelas 

```sql
-- Inserção de dados na tabela clientes
INSERT INTO clientes (id_cliente, nome, email, telefone, endereco)
VALUES
(1, 'João Silva', 'joao.silva@email.com', '11999999999', 'Rua das Flores, 123'),
(2, 'Maria Oliveira', 'maria.oliveira@email.com', '21988888888', 'Av. Central, 456'),
(3, 'Carlos Souza', 'carlos.souza@email.com', '31977777777', 'Rua B, 789'),
(4, 'Ana Costa', 'ana.costa@email.com', '21966666666', 'Rua Nova, 321');

-- Inserção de dados na tabela categorias
INSERT INTO categorias (id_categoria, nome, descricao)
VALUES
(1, 'Eletrônicos', 'Dispositivos eletrônicos em geral'),
(2, 'Roupas', 'Moda masculina e feminina'),
(3, 'Livros', 'Livros de diversos gêneros');

-- Inserção de dados na tabela produtos
INSERT INTO produtos (id_produto, nome, descricao, preco, estoque, id_categoria)
VALUES
(1, 'Smartphone X', 'Smartphone com 128GB', 1999.90, 50, 1),
(2, 'Notebook Y', 'Notebook com 16GB RAM', 3599.00, 30, 1),
(3, 'Camiseta Básica', 'Camiseta de algodão', 49.90, 100, 2),
(4, 'Livro SQL Avançado', 'Aprenda SQL com exemplos', 89.90, 70, 3),
(5, 'Fone Bluetooth', 'Fone de ouvido sem fio', 159.90, 80, 1);

-- Inserção de dados na tabela pedidos
INSERT INTO pedidos (id_pedido, id_cliente, data_pedido, status, valor_total)
VALUES
(1, 1, '2025-04-01', 'Enviado', 2049.80),
(2, 2, '2025-04-02', 'Processando', 3599.00),
(3, 3, '2025-04-03', 'Cancelado', 89.90);

-- Inserção de dados na tabela itens_pedido
INSERT INTO itens_pedido (id_item_pedido, id_pedido, id_produto, quantidade, preco_unitario)
VALUES
(1, 1, 1, 1, 1999.90),
(2, 1, 5, 1, 49.90),
(3, 2, 2, 1, 3599.00),
(4, 3, 4, 1, 89.90);

-- Inserção de dados na tabela pagamentos
INSERT INTO pagamentos (id_pagamento, id_pedido, data_pagamento, valor_pago, forma_pagamento, status_pagamento)
VALUES
(1, 1, '2025-04-01', 2049.80, 'Cartão de Crédito', 'Aprovado'),
(2, 2, '2025-04-02', 3599.00, 'PIX', 'Pendente'),
(3, 3, '2025-04-03', 89.90, 'Boleto', 'Cancelado');

-- Inserção de dados na tabela fornecedores
INSERT INTO fornecedores (id_fornecedor, nome, contato, telefone, email, endereco)
VALUES
(1, 'Tech Distribuidora', 'André Lima', '1133333333', 'andre@techdist.com', 'Rua da Tecnologia, 1000'),
(2, 'Moda Center', 'Fernanda Alves', '1144444444', 'fernanda@modacenter.com', 'Av. das Confecções, 2000'),
(3, 'Editora Saber', 'Bruno Rocha', '1155555555', 'bruno@sabereditora.com', 'Rua dos Livros, 3000');

```

---

## 🔍 Consultas SQL 

Consultas úteis extraídas do modelo, com seus resultados esperados.

### 1. Listar todos os clientes

```sql
SELECT * FROM clientes;
```
**Resultado esperado:**
| cliente_id | nome           | email               | telefone     |
|------------|----------------|---------------------|--------------|
| 1          | João Silva     | joao@email.com      | 11999999991  |
| 2          | Maria Souza    | maria@email.com     | 11999999992  |
| 3          | Ana Pereira    | ana@email.com       | 11999999993  |
| 4          | Carlos Costa   | carlos@email.com    | 11999999994  |
| 5          | Paula Andrade  | paula@email.com     | 11999999995  |


### 2. Listar todos os produtos com suas categorias

```sql
SELECT p.nome AS produto, c.nome AS categoria
FROM produtos p
JOIN categorias c ON p.categoria_id = c.categoria_id;
```
**Resultado esperado:**
| produto       | categoria    |
|---------------|--------------|
| Notebook      | Eletrônicos  |
| Smartphone    | Eletrônicos  |
| Camiseta      | Vestuário    |
| Calça Jeans   | Vestuário    |
| Micro-ondas   | Casa         |
| Liquidificador| Casa         |

### 3. Listar todos os pedidos com nome do cliente

```sql
SELECT p.pedido_id, c.nome AS cliente, p.data_pedido
FROM pedidos p
JOIN clientes c ON p.cliente_id = c.cliente_id;
```
**Resultado esperado:**
| pedido_id | cliente       | data_pedido |
|-----------|---------------|-------------|
| 1         | João Silva    | 2024-01-01  |
| 2         | Maria Souza   | 2024-01-03  |
| 3         | Ana Pereira   | 2024-01-05  |

### 4. Valor total de cada pedido

```sql
SELECT 
  p.pedido_id,
  SUM(ip.quantidade * ip.preco_unitario) AS total
FROM pedidos p
JOIN itens_pedido ip ON p.pedido_id = ip.pedido_id
GROUP BY p.pedido_id;
```
**Resultado esperado:**
| pedido_id | total   |
|-----------|---------|
| 1         | 6600.00 |
| 2         | 950.00  |
| 3         | 1600.00 |

### 5. Produtos mais vendidos (quantidade total)

```sql
SELECT 
  pr.nome AS produto, 
  SUM(ip.quantidade) AS quantidade_vendida
FROM itens_pedido ip
JOIN produtos pr ON ip.produto_id = pr.produto_id
GROUP BY pr.nome
ORDER BY quantidade_vendida DESC;
```
**Resultado esperado:**
| produto        | quantidade_vendida |
|----------------|--------------------|
| Camiseta       | 3                  |
| Calça Jeans    | 2                  |
| Smartphone     | 2                  |
| Notebook       | 1                  |
| Micro-ondas    | 1                  |
| Liquidificador | 1                  |

### 6. (Consulta Avançada) Clientes que já compraram produtos da categoria "Eletrônicos"

```sql
SELECT DISTINCT c.nome AS cliente
FROM clientes c
JOIN pedidos p ON c.cliente_id = p.cliente_id
JOIN itens_pedido ip ON p.pedido_id = ip.pedido_id
JOIN produtos pr ON ip.produto_id = pr.produto_id
JOIN categorias cat ON pr.categoria_id = cat.categoria_id
WHERE cat.nome = 'Eletrônicos';
```
**Resultado esperado:**
| cliente       |
|---------------|
| João Silva    |
| Maria Souza   |

---

## 📌 Créditos

> Criado por **SILVIA GUIMARÃES** como parte de portfólio de projetos SQL e modelagem relacional.

---

## **Agradecimentos**

Agradeço à equipe da **DIO** e **HEINEKEN** pela oportunidade de participar deste desafio e ampliar minhas habilidades em modelagem de banco de dados e organização estrutural de informações.  
Este projeto reflete o aprendizado prático e meu compromisso com boas práticas na área de tecnologia.

---

## Contato

Para dúvidas ou sugestões, entre em contato:
- **E-mail:** (sguimaraes1004@gmail.com)
- **Redes Sociais:** (https://www.linkedin.com/in/silvia-maria-guimar%C3%A3es-costa-3a01b423b)

---

🍺 _A parceria com a Heineken reforça o compromisso de promover a inovação e o aprendizado na área de tecnologia._

---


# ![DIO Logo](https://hermes.digitalinnovation.one/assets/diome/logo.png)


