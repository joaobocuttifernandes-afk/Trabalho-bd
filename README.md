# Trabalho-bd
banco-de-dados
-- Criação do banco de dados
CREATE DATABASE ecommerce_alura;
USE ecommerce_alura;

-- Tabela Geral (Generalização)
CREATE TABLE Cliente (
    id_cliente INT PRIMARY KEY AUTO_INCREMENT,
    nome_completo VARCHAR(100) NOT NULL,
    email VARCHAR(50) UNIQUE NOT NULL,
    data_cadastro DATE DEFAULT (CURRENT_DATE)
);

-- Especialização: Pessoa Física
CREATE TABLE Pessoa_Fisica (
    id_cliente INT PRIMARY KEY,
    cpf VARCHAR(11) UNIQUE NOT NULL,
    FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente)
);

-- Especialização: Pessoa Jurídica
CREATE TABLE Pessoa_Juridica (
    id_cliente INT PRIMARY KEY,
    cnpj VARCHAR(14) UNIQUE NOT NULL,
    FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente)
);

-- Entidade Fraca: Endereco (Relacionamento Identificador)
CREATE TABLE Endereco (
    id_endereco INT AUTO_INCREMENT,
    id_cliente INT,
    logradouro VARCHAR(100) NOT NULL,
    numero VARCHAR(10),
    cep VARCHAR(8),
    PRIMARY KEY (id_endereco, id_cliente), -- Chave composta caracteriza entidade fraca
    FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente) ON DELETE CASCADE
);

-- Entidade Forte: Produto
CREATE TABLE Produto (
    id_produto INT PRIMARY KEY AUTO_INCREMENT,
    descricao VARCHAR(150) NOT NULL,
    preco DECIMAL(10, 2) NOT NULL,
    estoque INT DEFAULT 0
);

-- Relacionamento N:M entre Pedido e Produto (Tabela Associativa)
CREATE TABLE Pedido (
    id_pedido INT PRIMARY KEY AUTO_INCREMENT,
    id_cliente INT,
    data_pedido DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente)
);

CREATE TABLE Item_Pedido (
    id_pedido INT,
    id_produto INT,
    quantidade INT NOT NULL,
    preco_unitario DECIMAL(10, 2),
    PRIMARY KEY (id_pedido, id_produto),
    FOREIGN KEY (id_pedido) REFERENCES Pedido(id_pedido),
    FOREIGN KEY (id_produto) REFERENCES Produto(id_produto)
);
