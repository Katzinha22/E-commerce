CREATE DATABASE EcommerceDB;
USE EcommerceDB;

CREATE TABLE Clientes (
                          ID_Cliente INT AUTO_INCREMENT PRIMARY KEY,
                          Nome VARCHAR(100) NOT NULL,
                          Email VARCHAR(100) UNIQUE NOT NULL,
                          Endereco VARCHAR(200),
                          Telefone VARCHAR(20),
                          Data_Cadastro DATETIME DEFAULT NOW()
);
INSERT INTO Clientes (Nome, Email, Endereco, Telefone)
VALUES
    ('Ana Beatriz Silva', 'ana.silva@gmail.com', 'Rua das Flores, 120 - São Paulo/SP', '(11) 99874-1123'),
    ('Carlos Pereira', 'carlos.pereira@yahoo.com', 'Av. Central, 876 - Rio de Janeiro/RJ', '(21) 98512-3344'),
    ('Juliana Costa', 'juliana.costa@hotmail.com', 'Rua das Palmeiras, 45 - Belo Horizonte/MG', '(31) 99211-6677');

CREATE TABLE Produtos (
                          ID_Produto INT AUTO_INCREMENT PRIMARY KEY,
                          Nome_Produto VARCHAR(100) NOT NULL,
                          Descricao TEXT,
                          Preco DECIMAL(10,2) NOT NULL,
                          Qtd_Estoque INT NOT NULL,
                          Categoria VARCHAR(50)
);

INSERT INTO Produtos (Nome_Produto, Descricao, Preco, Qtd_Estoque, Categoria)
VALUES
    ('Notebook Dell Inspiron 15', 'Notebook com processador i5, 8GB RAM e SSD 256GB', 3899.90, 20, 'Informática'),
    ('Smartphone Samsung Galaxy S23', 'Celular Android com 256GB de armazenamento', 5499.00, 15, 'Telefonia'),
    ('Fone Bluetooth JBL Tune 510BT', 'Fone sem fio com microfone embutido', 299.99, 50, 'Acessórios'),
    ('Mouse Gamer Redragon', 'Mouse com 7200 DPI e iluminação RGB', 159.90, 35, 'Periféricos');
CREATE TABLE Pedidos (
                         ID_Pedido INT AUTO_INCREMENT PRIMARY KEY,
                         ID_Cliente_FK INT NOT NULL,
                         Data_Pedido DATETIME DEFAULT NOW(),
                         Valor_Total DECIMAL(10,2),
                         Previsao_Entrega DATE,
                         Status_Pedido VARCHAR(50) DEFAULT 'Em Processamento',
                         FOREIGN KEY (ID_Cliente_FK) REFERENCES Clientes(ID_Cliente)
);
INSERT INTO Pedidos (ID_Cliente_FK, Valor_Total, Previsao_Entrega, Status_Pedido)
VALUES
    (1, 4199.80, '2025-11-20', 'Em Transporte'),
    (2, 299.99, '2025-11-18', 'Entregue'),
    (3, 5658.90, '2025-11-22', 'Aguardando Pagamento');

CREATE TABLE Itens_Pedido (
                              ID_Pedido_FK INT NOT NULL,
                              ID_Produto_FK INT NOT NULL,
                              Quantidade INT NOT NULL,
                              Preco_Unitario DECIMAL(10,2) NOT NULL,
                              PRIMARY KEY (ID_Pedido_FK, ID_Produto_FK),
                              FOREIGN KEY (ID_Pedido_FK) REFERENCES Pedidos(ID_Pedido),
                              FOREIGN KEY (ID_Produto_FK) REFERENCES Produtos(ID_Produto)
);

INSERT INTO Itens_Pedido (ID_Pedido_FK, ID_Produto_FK, Quantidade, Preco_Unitario)
VALUES
    (1, 1, 1, 3899.90),
    (1, 4, 2, 159.90),
    (2, 3, 1, 299.99),
    (3, 2, 1, 5499.00),
    (3, 4, 1, 159.90);

ALTER TABLE Clientes
    ADD COLUMN Data_Nascimento DATE AFTER Nome;

UPDATE Clientes
SET Data_Nascimento = '1995-06-12'
WHERE ID_Cliente = 1;

UPDATE Produtos
SET Qtd_Estoque = Qtd_Estoque - 1
WHERE ID_Produto = 2;

SELECT * FROM Clientes;
SELECT * FROM Produtos;
SELECT * FROM Pedidos;
SELECT * FROM Itens_Pedido;



