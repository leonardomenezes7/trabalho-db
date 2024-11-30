# Trabalho banco de dados

### Alunos: Leonardo Menezes, Gabriel Pires, Matheus Okada, Mateus Delmondes, Pedro Spinelli

Desenvolvemos este banco de dados para uma biblioteca simples como parte de um trabalho acadêmico da faculdade. O objetivo foi projetar e implementar uma estrutura eficiente que permita o gerenciamento de livros, usuários e empréstimos,utilizando o PostgreSQL como sistema de gerenciamento de banco de dados.

## Estrutura do banco de dados
<img width="100%" alt="Captura de Tela 2024-11-30 às 13 16 29" src="https://github.com/user-attachments/assets/284d0418-6ff1-4f4f-a479-58494f9aff86">

## Tecnologias Utilizadas
![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)

## Comandos Utilizados para criar o banco
Utilizamos o Docker para criar o banco de dados PostgreSQL do projeto, aproveitando a imagem do Bitnami PostgreSQL para configurar um ambiente seguro e escalável de maneira rápida.
```
docker run -d --name biblioteca-db \
  -e POSTGRESQL_USERNAME=admin \
  -e POSTGRESQL_PASSWORD=adminpassword \
  -e POSTGRESQL_DATABASE=biblioteca \
  -p 5432:5432 \
  bitnami/postgresql:latest
```

```
-- Tabela Livros
CREATE TABLE livros (
    id SERIAL PRIMARY KEY,
    titulo VARCHAR(255) NOT NULL,
    autor VARCHAR(255) NOT NULL,
    ano_publicacao INT,
    disponivel BOOLEAN DEFAULT TRUE
);

-- Tabela Usuários
CREATE TABLE usuarios (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL
);

-- Tabela Empréstimos
CREATE TABLE emprestimos (
    id SERIAL PRIMARY KEY,
    livro_id INT REFERENCES livros(id) ON DELETE CASCADE,
    usuario_id INT REFERENCES usuarios(id) ON DELETE CASCADE,
    data_emprestimo DATE NOT NULL DEFAULT CURRENT_DATE,
    data_devolucao DATE
);
```

## Comandos Utilizados para inserir dados no banco
```
- Livros
INSERT INTO livros (titulo, autor, ano_publicacao)
VALUES
('1984', 'George Orwell', 1949),
('Dom Casmurro', 'Machado de Assis', 1899),
('A Culpa é das Estrelas', 'John Green', 2012);

-- Usuários
INSERT INTO usuarios (nome, email)
VALUES
('João Silva', 'joao@email.com'),
('Maria Oliveira', 'maria@email.com');

-- Empréstimos
INSERT INTO emprestimos (livro_id, usuario_id, data_emprestimo)
VALUES
(1, 1, '2024-01-01'),
(2, 2, '2024-01-03');
```

### Conclusões
O desenvolvimento deste banco de dados para uma biblioteca simples nos permitiu consolidar os conceitos aprendidos em sala de aula e aplicar ferramentas modernas como o PostgreSQL e o Docker. A experiência incluiu a modelagem de um sistema funcional, com tabelas bem definidas para gerenciar livros, usuários e empréstimos, garantindo integridade e consistência dos dados.

Ao utilizar o Docker, pudemos criar um ambiente controlado, portátil e de fácil manutenção, que é essencial para projetos de desenvolvimento modernos. O uso de SQL para a criação e manipulação das tabelas reforçou a compreensão prática sobre consultas, relacionamentos e boas práticas de banco de dados.
