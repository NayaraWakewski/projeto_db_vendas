<!-- Imagem redimensionada -->
<img src="https://digitalcollege.com.br/wp-content/webp-express/webp-images/uploads/2022/05/logo-digital.png.webp" alt="texto alt" width="300">

# 🚀 Projeto de Migração de Banco de Dados e ETL com Pentaho e SQL Server

Bem-vindo à documentação do projeto de migração de banco de dados relacional no Postgres para um banco de dados dimensional, usando o Pentaho para ETL e migrando para o SQL Server.

## 🚀 Visão Geral do Projeto

Este projeto teve três principais fases:

1. **Migração Inicial para Banco de Dados Dimensional no PostgreSQL:**
As tabelas `tbpro`, `tbven_item`, `tbvdd`, `tbdep`, `tbven` foram transformadas em tabelas dimensionais (`dim_produto`, `dim_vendedor`, `dim_dependente`, `dim_cliente`, `dim_canal`, `dim_status`, `dim_data`) no PostgreSQL.
Essa primeira etapa do projeto consta no repositório: [tabelas_dim](https://github.com/NayaraWakewski/tabelas_dim.git)

2. **Consultas Avançadas em SQL:** Realizou-se consultas avançadas na estrutura dimensional criada no PostgreSQL, explorando análises e agregações complexas.
Essa segunda etapa do projeto consta no repositório: [Desafio_SQL_Avancado](https://github.com/NayaraWakewski/Desafio_SQL_Avancado)
   
3. **Migração para SQL Server com ETL Pentaho:** As tabelas originais (`tbpro`, `tbven_item`, `tbvdd`, `tbdep`, `tbven`) foram importadas para o Pentaho, para realizar o processo ETL. As tabelas dimensionais criadas (`dim_produto`, `dim_vendedor`, `dim_dependente`, `dim_cliente`, `dim_canal`, `dim_status`, `dim_data`) foram migradas para o banco de dados SQL Server.


## 🚀 Transformações Pentaho

Aqui estão alguns exemplos de transformações realizadas no Pentaho:

### Fluxo da Transformação e Migração de Dados

![Transformação de Migração de Dados](https://user-images.githubusercontent.com/79403619/260829897-29118a28-26c5-44b8-8eaa-d8ad74da34a8.jpg)


## 🚀 Sql Server Banco de Dados

Aqui esta a tela do banco de dados no SQL Server:

![SQL Server Banco de Dados](https://user-images.githubusercontent.com/79403619/260829972-0e7aa705-c737-43da-9c67-65f73ac42088.jpg)


### Alguns exemplos de consultas no SQL Server

### Atualização da Coluna `valor_total_vendas` na Tabela `fato_vendas`

Para iniciar as consultas, devemos primeiro calcular o valor total das vendas em na tabela `fato_vendas`, onde podemos executar um comando UPDATE que multiplica a coluna `quantidade_vendas` pela coluna `valor_unitario_vendido` e armazena o resultado na coluna `valor_total_vendas`.

Primeiro, devemos acessar o banco de dados onde a tabela `fato_vendas` está localizada. No exemplo, usaremos o banco de dados `db_vendas_nayara`. Você pode fazer isso usando o comando `USE`:

```sql
USE db_vendas_nayara;
```

Em seguida, executamos o comando UPDATE para calcular o valor total das vendas e atualizar a coluna valor_total_vendas na tabela fato_vendas:


```sql
UPDATE fato_vendas
SET valor_total_vendas = quantidade_vendas * valor_unitario_vendido;
```

### Medidas na Tabela `fato_vendas` no SQL Server.

> Consulta de Vendas por Canal e Cliente

```sql
Use db_vendas_nayara

SELECT
    dc.descricao_canal,
    dcl.nome_cliente,
    SUM(fato.valor_total_vendas) AS total_vendas
FROM
    fato_vendas AS fato
    INNER JOIN dim_canal AS dc ON fato.codigo_canal = dc.codigo_canal
    INNER JOIN dim_cliente AS dcl ON fato.codigo_cliente = dcl.codigo_cliente
GROUP BY
    dc.descricao_canal,
    dcl.nome_cliente
ORDER BY
    dc.descricao_canal, dcl.nome_cliente;gora vamos ver o exemplo de uma Medida no SQL Server:
```


> Consulta de Vendas por Produto e Data

```sql
Use db_vendas_nayara
SELECT
    dp.nome_produto,
    dd.data,
    SUM(fato.valor_total_vendas) AS total_vendas
FROM
    fato_vendas AS fato
    INNER JOIN dim_produto AS dp ON fato.codigo_produto = dp.codigo_produto
    INNER JOIN dim_data AS dd ON fato.data_venda = dd.Data
GROUP BY
    dp.nome_produto,
    dd.data
ORDER BY
    dd.data, dp.nome_produto;
```

## ⚙️ Configuração do Ambiente

Para reproduzir este projeto, você precisará das seguintes ferramentas instaladas:

- PostgreSQL.
- SQL Server.
- Pentaho Data Integration.


## 🎁 Expressões de gratidão

* Compartilhe com outras pessoas esse projeto 📢;
* Quer saber mais sobre o projeto? Entre em contato para tomarmos um :coffee:;

---
⌨️ com ❤️ por [Nayara Vakevskii](https://github.com/NayaraWakewski) 😊


