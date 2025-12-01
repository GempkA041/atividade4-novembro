# 📚 Sistema de Gestão - Livraria Saber

Bem-vindo ao repositório oficial do banco de dados da **Livraria Saber**. Este projeto consiste na modelagem e implementação SQL de um sistema para gerenciar uma loja que comercializa tanto Livros quanto produtos de Papelaria.

## 🎯 Objetivo

O sistema foi projetado para garantir a integridade das operações de venda e estoque, resolvendo o desafio de gerenciar dois tipos de produtos distintos (Livros e Papelaria) em um único fluxo de caixa.

**O sistema gerencia:**
* **Vendas:** Processamento de itens variados com cálculo de total e registro de forma de pagamento.
* **Estoque Híbrido:** Controle de Livros (ISBN, Editora, Autor) e Papelaria (Marca, Categoria).
* **Atores:** Clientes, Vendedores (com comissão), Fornecedores e Editoras.

## 🛠️ Tecnologias Utilizadas

* **Banco de Dados:** MySQL (Compatível com versão 8.0+)
* **Modelagem:** dbdiagram.io (para DER)
* **Linguagem:** SQL (DDL e DML)

## 📂 Estrutura do Repositório

O repositório contém os scripts de criação das tabelas e população de dados (inserts):

* `Livraria_s.sql`: **Arquivo principal** (Dump completo com todas as tabelas e dados).
* `livraria_saber_*.sql`: Arquivos modulares separados por entidade (ex: `livraria_saber_cliente.sql`, `livraria_saber_venda.sql`) para manutenção específica.

## 💻 Como Executar (Importar o Banco)

Para testar este projeto em sua máquina, você precisará do MySQL Workbench ou qualquer cliente SQL.

1.  **Clone o repositório:**
    ```bash
    git clone [https://github.com/GempkA041/atividade4-novembro.git](https://github.com/GempkA041/atividade4-novembro.git)
    ```

2.  **Crie o Banco de Dados:**
    Abra seu terminal MySQL ou Workbench e execute:
    ```sql
    CREATE DATABASE livraria_saber;
    USE livraria_saber;
    ```

3.  **Importe as Tabelas:**
    Recomendo importar o arquivo completo. No seu cliente SQL (ou via linha de comando), execute o arquivo:
    * Arquivo: `Livraria_s.sql`

    *Exemplo via linha de comando:*
    ```bash
    mysql -u seu_usuario -p livraria_saber < Livraria_s.sql
    ```

## 🔍 Destaques da Modelagem

Algumas decisões técnicas importantes implementadas neste banco:

* **Restrição de Exclusividade (Constraint Check):** Na tabela `item_venda`, foi implementada uma lógica para garantir que um item vendido seja *ou* um Livro *ou* um item de Papelaria, nunca ambos no mesmo registro, nem nenhum.
    ```sql
    CONSTRAINT `item_venda_chk_1` CHECK (((`id_livro` is not null) xor (`id_papelaria` is not null)))
    ```
* **Normalização:** O banco está normalizado até a 3FN, separando `AUTOR`, `EDITORA` e `FORNECEDOR` para evitar redundância de dados.
---
*Projeto desenvolvido como parte da Atividade 04 de Novembro.* 🚀
