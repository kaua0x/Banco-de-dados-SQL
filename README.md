CREATE TABLE Cliente (
    id_cliente INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    cpf VARCHAR(11) NOT NULL UNIQUE, 
    email VARCHAR(100),
    endereco VARCHAR(255),
    telefone VARCHAR(15)
);

CREATE TABLE Fornecedor (
    id_fornecedor INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    contato VARCHAR(100),
    endereco VARCHAR(255)
);

CREATE TABLE Produto (
    id_produto INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    categoria VARCHAR(100),
    preco DECIMAL(10, 2) NOT NULL,
    id_fornecedor INT,
    FOREIGN KEY (id_fornecedor) REFERENCES Fornecedor(id_fornecedor)
);

CREATE TABLE Vendedor (
    id_vendedor INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100),
    telefone VARCHAR(15)
);

CREATE TABLE Pedido (
    id_pedido INT PRIMARY KEY,
    data_pedido DATE NOT NULL,
    status VARCHAR(50),
    id_cliente INT,
    id_vendedor INT,
    FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente),
    FOREIGN KEY (id_vendedor) REFERENCES Vendedor(id_vendedor)
);

CREATE TABLE Item_Pedido (
    id_item_pedido INT PRIMARY KEY,
    id_pedido INT,
    id_produto INT,
    quantidade INT NOT NULL,
    preco_por_unidade DECIMAL(10, 2),
    FOREIGN KEY (id_pedido) REFERENCES Pedido(id_pedido),
    FOREIGN KEY (id_produto) REFERENCES Produto(id_produto)
);


INSERT INTO Cliente (id_cliente, nome, cpf, email, endereco, telefone)
VALUES (1, 'JOADSON', '5328899124', 'joadson@gmail.com', 'Rua A, 123', '99999-9999');

INSERT INTO Fornecedor (id_fornecedor, nome, contato, endereco)
VALUES (1, 'Fornecedor 1', 'contato@fornecedor1.com', 'Av. Central, 456');

INSERT INTO Produto (id_produto, nome, categoria, preco, id_fornecedor)
VALUES (1, 'Bola', 'Categoria "Futebol"', 70.00, 1),
       (2, 'Tênis', 'Categoria "Esportivo"', 250.00, 1);

INSERT INTO Vendedor (id_vendedor, nome, email, telefone)
VALUES (1, 'Tulio', 'tuliosouza@gmail.com', '98888-8888');

INSERT INTO Pedido (id_pedido, data_pedido, status, id_cliente, id_vendedor)
VALUES (1, '2024-11-14', 'Em andamento', 1, 1);

INSERT INTO Item_Pedido (id_item_pedido, id_pedido, id_produto, quantidade, preco_por_unidade)
VALUES (1, 1, 1, 2, 50.00),
       (2, 1, 2, 1, 30.00);


SELECT *
FROM Cliente
JOIN Pedido ON Cliente.id_cliente = Pedido.id_cliente
JOIN Vendedor ON Pedido.id_vendedor = Vendedor.id_vendedor
JOIN Item_Pedido ON Pedido.id_pedido = Item_Pedido.id_pedido
JOIN Produto ON Item_Pedido.id_produto = Produto.id_produto
JOIN Fornecedor ON Produto.id_fornecedor = Fornecedor.id_fornecedor;

DROP TABLE IF EXISTS Item_Pedido;
DROP TABLE IF EXISTS Pedido;
DROP TABLE IF EXISTS Vendedor;
DROP TABLE IF EXISTS Produto;
DROP TABLE IF EXISTS Fornecedor;
DROP TABLE IF EXISTS Cliente;
