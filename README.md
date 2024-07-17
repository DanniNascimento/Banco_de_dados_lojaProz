# Praticando SQL Curso Proz Banco de dados Simples...

Lembre-se, cada desafio é uma chance de crescer. Não se desanime com os erros; eles são degraus no caminho do aprendizado. E acima de tudo, divirta-se! 
O aprendizado mais eficaz acontece quando nos engajamos e nos interessamos pelo que estamos fazendo.


Vamos criar um banco de dados para a loja, com tabelas para Clientes e Vendas. Em seguida, criaremos uma função que retorna o número de clientes cadastrados em um determinado dia

#### Criando uma base de banco de dados
```sql
CREATE DATABASE Loja;
```

#### Criando tabelas na base de dados(clientes)
```sql
CREATE TABLE Clientes (
    ClienteID INT PRIMARY KEY AUTO_INCREMENT,
    Nome VARCHAR(100),
    DataCadastro DATE
);
```

#### Criando tabela (vendas)
```sql
CREATE TABLE Vendas (
    VendaID INT PRIMARY KEY AUTO_INCREMENT,
    ClienteID INT,
    ProdutoID INT,
    Quantidade INT,
    DataVenda DATE,
    FOREIGN KEY (ClienteID) REFERENCES Clientes(ClienteID)
);
```

#### Vamos Inserir dados nas tabelas (clientes)
```sql
INSERT INTO Clientes (Nome, DataCadastro) VALUES
('João Silva', '2024-07-14'),
('Maria Souza', '2024-07-14'),
('Pedro Oliveira', '2024-07-15'),
('Ana Paula', '2024-07-15'),
('Lucas Santos', '2024-07-16');
```

#### Inserindo dados na tabela (vendas)
```sql
INSERT INTO Vendas (ClienteID, ProdutoID, Quantidade, DataVenda) VALUES
(1, 1, 2, '2024-07-14'),
(2, 2, 1, '2024-07-14'),
(3, 3, 3, '2024-07-15'),
(4, 1, 1, '2024-07-15'),
(5, 2, 2, '2024-07-16');
```

#### Criando uma funcao para realizar a contagem de todos os clientes cadastro no dia especifico
```sql
DELIMITER //

CREATE FUNCTION ContarClientesPorDia(data DATE) RETURNS INT
BEGIN
    DECLARE totalClientes INT;
    SELECT COUNT(*) INTO totalClientes
    FROM Clientes
    WHERE DataCadastro = data;
    RETURN totalClientes;
END //

DELIMITER ;
```

#### Utilizando a funcao para contar clientes cadastrados em um dia especifico
```sql
SELECT ContarClientesPorDia('2024-07-14') AS TotalClientesEm14072024;
```

#### Resultado

Com a execução da função ContarClientesPorDia para a data 2024-07-14 ele deve retornar o número de clientes cadastrados nesse dia...

```sql
+--------------------------+
| TotalClientesEm14072024  |
+--------------------------+
|                        2 |
+--------------------------+
```
