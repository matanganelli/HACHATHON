# 📱 MVP Hub Financeiro - Banco de Dados

![SQL Server](https://img.shields.io/badge/Database-SQL_Server-CC2927?style=for-the-badge&logo=microsoft-sql-server&logoColor=white)
![Status](https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge)

## 📘 Sobre o Projeto

Este projeto consiste na modelagem e implementação de um banco de dados relacional para um **Hub Financeiro Móvel** (Fintech). O sistema centraliza operações como PIX, pagamentos, recargas e empréstimos, utilizando **Stored Procedures** para garantir a integridade das regras de negócio (como atualização automática de saldos).

## 🧠 Modelagem de Dados

### 1. MER - Modelo Entidade-Relacionamento (Conceitual)

Abaixo estão as regras de negócio que definem os relacionamentos entre as entidades:

* **Usuários e Contas:** Um usuário pode possuir várias contas (ex: Corrente e Poupança), mas uma conta pertence a apenas um usuário **(1:N)**.
* **Contas e Transações:** Uma conta pode ter diversas transações, mas uma transação pertence a uma única conta **(1:N)**.
* **Transações e Categorias:** Uma transação deve ter uma categoria (ex: Alimentação), e uma categoria pode classificar várias transações **(1:N)**.
* **Contas e Serviços (Pix, Pagamentos, Recargas, Cashback):** Todos esses serviços são vinculados diretamente a uma conta específica. Se a conta for excluída, o histórico é removido (Cascade) **(1:N)**.
* **Usuários e Produtos Financeiros (Seguros, Empréstimos):** Estes produtos são vinculados ao CPF do usuário (Pessoa), e não à conta bancária específica **(1:N)**.

---

### 2. DER - Diagrama Entidade-Relacionamento (Lógico)

O diagrama abaixo representa a estrutura lógica do banco de dados gerado pelo script.

```mermaid
erDiagram
    USUARIOS ||--o{ CONTAS : possui
    USUARIOS ||--o{ SEGUROS : contrata
    USUARIOS ||--o{ EMPRESTIMOS : solicita
    
    CONTAS ||--o{ TRANSACOES : realiza
    CONTAS ||--o{ PIX : envia_recebe
    CONTAS ||--o{ PAGAMENTOS : efetua
    CONTAS ||--o{ RECARGAS : faz
    CONTAS ||--o{ CASHBACK : ganha
    
    CATEGORIAS ||--o{ TRANSACOES : classifica

    USUARIOS {
        int id_usuario PK
        string nome
        string email
        string senha_hash
    }

    CONTAS {
        int id_conta PK
        int id_usuario FK
        decimal saldo
        string tipo_conta
    }

    TRANSACOES {
        int id_transacao PK
        int id_conta FK
        int id_categoria FK
        decimal valor
        string descricao
    }

    CATEGORIAS {
        int id_categoria PK
        string nome
        string tipo
    }

    PIX {
        int id_pix PK
        int id_conta FK
        string chave_destino
        string tipo_operacao
    }

🗂 Estrutura das Tabelas
O banco MVP_HubFinanceiro segue a 3ª Forma Normal (3FN).

⚙️ Stored Procedures (Automação)
O diferencial deste projeto é que o saldo não é manipulado manualmente. Utilizamos Procedures para garantir que toda operação financeira reflita imediatamente no saldo da conta.

🔄 Operações que atualizam saldo automaticamente:
sp_registrar_transacao:

Se a categoria for 'entrada' ➝ Soma ao saldo.

Se a categoria for 'saida' ➝ Subtrai do saldo.

sp_registrar_pix:

Identifica se é 'envio' (subtrai) ou 'recebimento' (soma).

sp_registrar_pagamento:

Registra o boleto como 'pago' e desconta o valor.

sp_fazer_recarga:

Debita o valor da recarga da conta.

sp_adicionar_cashback:

Credita o valor do benefício na conta.

📋 Procedures de Leitura e Gestão:
sp_criar_usuario / sp_listar_usuarios

sp_extrato_conta (Relatório completo com JOINs)

sp_solicitar_emprestimo

🛠 Como Executar o Projeto
Clone o repositório:

Bash

git clone [https://github.com/SEU-USUARIO/MVP_HubFinanceiro.git](https://github.com/SEU-USUARIO/MVP_HubFinanceiro.git)
Abra o SGBD: Utilize o SQL Server Management Studio (SSMS) ou Azure Data Studio.

Execute o Script: Abra o arquivo script_completo.sql e execute (F5). O script irá:

Criar o banco e as tabelas.

Inserir dados de teste (Seed Data).

Criar as Stored Procedures.

Teste uma operação:

SQL

-- Exemplo: Fazer um PIX de R$ 50,00
EXEC sp_registrar_pix 1, 'ana@email.com', 'email', 'envio', 50.00;

-- Verifique o saldo atualizado
SELECT * FROM contas WHERE id_conta = 1;
✒️ Autor Matheus grigorio de sousa
Desenvolvido como parte do estudo de Arquitetura de Banco de Dados e SQL Server.
