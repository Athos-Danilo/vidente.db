# Vidente.db

Um projeto acadêmico integrado para as disciplinas de Web II e Banco de Dados II.

## O Projeto

**Vidente.db** é um sistema web interativo onde os usuários podem fazer perguntas sobre o futuro, o universo e tudo mais. 

O personagem central que fornece as respostas é inspirado no **C-3PO** (da franquia Star Wars). Famoso por sua preocupação constante, ele irá calcular as probabilidades matemáticas de forma dramática para as perguntas enviadas pelos usuários.

## Tecnologias e Arquitetura

Este projeto utiliza uma arquitetura moderna dividida entre Front-end e Back-end, aplicando o conceito de **persistência poliglota** (usando múltiplos paradigmas de banco de dados para diferentes necessidades):

- **Front-end (Web II):** React.js 
- **Back-end:** Node.js com Express
- **Banco de Dados SQL (BD II):** Gerenciará os dados relacionais e estruturados, como as contas de Usuários e perfis.
- **Banco de Dados NoSQL (BD II):** Gerenciará as Previsões, guardando os históricos de perguntas, respostas e as probabilidades calculadas de forma flexível (via documentos JSON).

