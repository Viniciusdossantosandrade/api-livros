# 📚 BookHub — Core Engine & Management Portal

> **Plataforma modular para gestão de acervos e inventários bibliográficos.** Projetada com **FastAPI**, **MySQL** e arquitetura assíncrona orientada a serviços, integrada a um painel web dinâmico e reativo desenvolvido em Vanilla JavaScript.

![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=flat&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat&logo=fastapi&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-8.0+-4479A1?style=flat&logo=mysql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![Pytest](https://img.shields.io/badge/Pytest-0A9EDC?style=flat&logo=pytest&logoColor=white)

---

## 🎯 Visão Geral do Sistema

O **BookHub** é uma solução de nível de produção desenvolvida para resolver problemas de rastreabilidade de inventário em acervos literários. O ecossistema combina um ecossistema backend resiliente e escalável com uma interface web de baixa latência.

### Principais Destaques Arquiteturais

* **Padrão Repository & Service:** Desacoplamento total entre a camada de persistência e as regras de negócio.
* **Segurança & CORS Configurado:** Filtros rigorosos de origem para prevenção de *Cross-Origin Resource Sharing* indevido.
* **Injeção de Dependências Native:** Gerenciamento eficiente de sessões de banco de dados via `Depends` do FastAPI.
* **Resiliência a Falhas:** Tratamento global de exceções HTTP e logs padronizados.

---

## 📊 Modelo de Dados (Entidade Livro)

A tabela principal de persistência segue especificações rigorosas de integridade relacional:

```mermaid
erDiagram
    LIVROS {
        BIGINT id PK "Auto-increment / Primary Key"
        VARCHAR_255 titulo "Not Null / Indexed"
        VARCHAR_255 autor "Not Null"
        INT ano_publicacao "Not Null / Range Check"
        BOOLEAN disponivel "Default: True"
        TIMESTAMP created_at "Default: CURRENT_TIMESTAMP"
    }
    bookhub-core/
├── .github/
│   └── workflows/
│       └── ci.yml             # Pipeline de Integração Contínua (CI)
├── docker/
│   ├── Dockerfile
│   └── docker-compose.yml     # Orquestração do banco e API
├── app/
│   ├── core/
│   │   ├── config.py          # Validação de variáveis de ambiente com Pydantic
│   │   └── database.py        # Configuração da engine SQLAlchemy e SessionLocal
│   ├── models/                # Entidades declarativas da ORM
│   ├── schemas/               # Modelos Pydantic para Request/Response DTOs
│   ├── repositories/          # Queries e persistência direta
│   ├── services/              # Regras de negócio e validações avançadas
│   ├── api/
│   │   └── v1/
│   │       └── endpoints/     # Rotas HTTP versionadas
│   └── main.py                # Bootstrapping e Middlewares
├── tests/                     # Testes automatizados com Pytest e httpx
├── frontend/                  # Dashboard administrativo Vanilla Web
│   ├── assets/
│   ├── index.html
│   └── main.js
├── .env.example
├── requirements.txt
└── README.md