# Especificação Técnica - Vidente.db

## Sumário
1. [Visão Geral do Projeto](#1-visão-geral-do-projeto)
2. [Justificativa e Objetivos](#2-justificativa-e-objetivos)
3. [Arquitetura do Sistema](#3-arquitetura-do-sistema)
4. [Requisitos do Sistema](#4-requisitos-do-sistema)
    - [Requisitos Funcionais (RF)](#requisitos-funcionais-rf)
    - [Requisitos Não Funcionais (RNF)](#requisitos-não-funcionais-rnf)
5. [Regras de Negócio](#5-regras-de-negócio)
6. [Modelagem de Dados (Persistência Poliglota)](#6-modelagem-de-dados-persistência-poliglota)
    - [Banco de Dados Relacional (SQL)](#banco-de-dados-relacional-sql)
    - [Banco de Dados Não Relacional (NoSQL)](#banco-de-dados-não-relacional-nosql)
7. [Tecnologias Utilizadas](#7-tecnologias-utilizadas)

---

## 1. Visão Geral do Projeto
O **Vidente.db** é um sistema web interativo com temática humorística voltada ao universo de tecnologia/nerd. O personagem central, inspirado no droide C-3PO de Star Wars, atua como um "oráculo" calculista e fatalista, fornecendo probabilidades dramáticas para perguntas feitas pelos usuários. O sistema será construído integrando conceitos de desenvolvimento web moderno (Web II) e persistência de dados híbrida (BD II).

## 2. Justificativa e Objetivos
Este projeto tem como principal objetivo acadêmico aplicar na prática os conceitos estudados nas disciplinas de **Web II** e **Banco de Dados II**.
A obrigatoriedade de adotar uma arquitetura de **persistência poliglota** justifica-se pela necessidade técnica de compreender e implementar múltiplos paradigmas de banco de dados (Relacional e Não Relacional) dentro do mesmo ecossistema, utilizando a ferramenta mais adequada para cada tipo de carga de trabalho e modelagem.

## 3. Arquitetura do Sistema
O sistema adota o modelo Cliente-Servidor baseado em API REST:
- **Client-side (Front-end):** Interface desenvolvida em React.js utilizando **TypeScript** (Single Page Application). É a camada encarregada de coletar as perguntas do usuário, exibir as animações do "Oráculo" e renderizar de forma reativa os retornos do sistema.
- **Server-side (Back-end):** API estruturada em Node.js com Express utilizando **JavaScript**, atuando como o elo de lógica de negócio e interfaceamento com a camada de persistência.
- **Database Layer:** Camada dividida estrategicamente entre um Sistema de Gerenciamento de Banco de Dados Relacional (SGBD) e um banco de dados NoSQL Orientado a Documentos.

## 4. Requisitos do Sistema

### Requisitos Funcionais (RF)
*(Ações e comportamentos que o sistema deve obrigatoriamente executar)*
- **RF01:** O sistema deve permitir que um usuário crie uma conta fornecendo Nome, E-mail e Senha.
- **RF02:** O sistema deve permitir a autenticação do usuário.
- **RF03:** O usuário poderá enviar uma pergunta em formato de texto livre para o Oráculo.
- **RF04:** O sistema deverá processar a requisição e retornar uma probabilidade (%) calculada e uma mensagem de resposta baseada no estilo do personagem.
- **RF05:** O sistema deve registrar e salvar um histórico das interações (perguntas, previsões e datas).
- **RF06:** O sistema deve expor um *feed* (lista pública ou privada) com as consultas recentes feitas ao Oráculo.
- **RF07:** O sistema deve permitir login e cadastro simplificado utilizando contas do Google (OAuth2).

### Requisitos Não Funcionais (RNF)
*(Restrições técnicas, performance, usabilidade e qualidade)*
- **RNF01:** A interface de usuário deve ser construída exclusivamente com a biblioteca React.js e padronizada com **TypeScript**.
- **RNF02:** O backend deve ser uma API RESTful escrita em **JavaScript**, utilizando Node.js e Express.
- **RNF03:** O armazenamento de dados deve ser híbrido (Poliglota), integrando um banco de dados relacional e um não relacional simultaneamente.
- **RNF04:** O sistema deve manter as senhas dos usuários criptografadas no banco (utilizando *hashes* como o bcrypt).

## 5. Regras de Negócio
- **RN01:** Não será permitido o cadastro de dois usuários com o mesmo endereço de e-mail.
- **RN02:** Toda previsão retornada pelo oráculo deverá conter uma taxa de probabilidade gerada de forma lógica e arbitrária variando entre 0% e 100%.
- **RN03:** O "tom" da mensagem retornada ao usuário deverá variar dependendo da faixa da probabilidade (Ex: Se probabilidade < 15%, a mensagem deverá ser excessivamente dramática e pessimista).

## 6. Modelagem de Dados (Persistência Poliglota)

### Banco de Dados Relacional (SQL)
Responsável por dados altamente estruturados e relacionamentos estáveis (Ex: Dados administrativos).
- **Entidades Foco:** `Usuarios`
- **Por que SQL?** Porque entidades de usuários exigem um esquema rígido (colunas fixas: id, nome, email, senha), integridade referencial forte e propriedades ACID para garantir que não haja duplicação ou anomalias nos logins.

### Banco de Dados Não Relacional (NoSQL)
Responsável pelo registro de alto volume e esquema flexível (Ex: Feed e Histórico).
- **Coleções Foco:** `Previsoes` (contendo o id do usuário associado, a pergunta, a probabilidade calculada e as palavras do oráculo).
- **Por que NoSQL?** As previsões podem ser consideradas *documentos*. O esquema não precisa ser engessado, facilitando a adição de novos metadados (como "humor do oráculo" ou "tempo de resposta") no futuro sem quebrar tabelas existentes. E possibilita altíssima velocidade para a leitura do "feed" na página inicial.

## 7. Tecnologias Utilizadas
- **Front-end:** React.js, TypeScript, HTML5, CSS3.
- **Back-end:** Node.js, Express, JavaScript.
- **Bancos de Dados:** PostgreSQL ou MySQL (SQL) + MongoDB (NoSQL).
- **Outros:** Git e GitHub (Versionamento).
