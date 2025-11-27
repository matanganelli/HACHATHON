📌 MVP – Hub Financeiro

Sistema de banco digital completo com contas, transações, PIX, pagamentos, recargas, cashback, seguros e empréstimos.

Este projeto implementa um banco de dados robusto em SQL Server, com tabelas normalizadas, relacionamentos, dados fictícios para testes e stored procedures que executam automaticamente operações financeiras.

🚀 Tecnologias Utilizadas

SQL Server

T-SQL

Stored Procedures

Modelagem Relacional (DER)

MER (Modelo Conceitual)

🗄️ Estrutura Geral do Banco de Dados

O banco MVP_HubFinanceiro é composto pelos seguintes módulos:

👤 Usuários

Armazenamento dos clientes do sistema.

💳 Contas

Contas digitais, correntes e poupança vinculadas a usuários.

🏷️ Categorias

Classificação de transações como entrada ou saída.

🔄 Transações

Movimentações financeiras com atualização automática de saldo de conta.

⚡ PIX

Operações de envio e recebimento.

🧾 Pagamentos

Boletos pagos, pendentes ou cancelados.

📱 Recargas

Recargas de celular feitas pelo usuário.

🎁 Cashback

Créditos retornados ao usuário.

🛡️ Seguros

Contratação de seguros diversos.

💵 Empréstimos

Solicitações com juros, parcelas e controle de status.

🧩 DER – Diagrama Entidade-Relacionamento (Lógico)
USUARIOS 1─N CONTAS 1─N TRANSACOES N─1 CATEGORIAS
USUARIOS 1─N SEGUROS
USUARIOS 1─N EMPRESTIMOS

CONTAS 1─N PIX
CONTAS 1─N PAGAMENTOS
CONTAS 1─N RECARGAS
CONTAS 1─N CASHBACK

📘 MER – Modelo Conceitual (Simplificado)
           [USUÁRIO]
               |
   ---------------------------------
   |               |               |
[CONTA]        [SEGURO]     [EMPRESTIMO]
   |
   -----------------------------------------------------------------
   |        |           |            |                |
[TRANS]   [PIX]    [PAGAMENTO]   [RECARGA]       [CASHBACK]
   |
[CATEGORIA]

🛠 Stored Procedures Implementadas
👤 Usuários

sp_criar_usuario

sp_listar_usuarios

sp_atualizar_usuario

sp_desativar_usuario

💳 Contas

sp_criar_conta

sp_listar_contas_usuario

🏷️ Categorias

sp_criar_categoria

sp_listar_categorias

🔄 Transações

sp_registrar_transacao (atualiza saldo automaticamente)

sp_extrato_conta

⚡ PIX

sp_registrar_pix (debitando ou creditando o saldo)

🧾 Pagamentos

sp_registrar_pagamento

📱 Recargas

sp_fazer_recarga

🎁 Cashback

sp_adicionar_cashback

🛡️ Seguros

sp_contratar_seguro

💵 Empréstimos

sp_solicitar_emprestimo

📦 Como Executar

Abra o SQL Server Management Studio ou Azure Data Studio

Execute o script completo .sql contido neste repositório

O banco será criado automaticamente com:

tabelas

relacionamentos

dados fictícios

procedures funcionais

🧪 Dados de Teste Incluídos

5 usuários cadastrados

Contas digitais, poupança e corrente

Categorias de entrada e saída

Transações financeiras reais

PIX enviados/recebidos

Pagamentos variados

Recargas de operadoras

Cashback de diversas compras

Seguros de vida, residencial, celular e automóvel

Empréstimos com juros e status

📄 Licença

Este projeto é livre para uso acadêmico e de demonstração.
