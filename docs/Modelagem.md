# AprendeRPG — Arquitetura e Modelagem do Sistema

> Documento de apoio à Etapa 2 (Planejamento Operacional e Gestão Ágil) do Projeto Integrador.

---

## 1. Modelo de Dados

O modelo inicial possui as entidades básicas necessárias para o funcionamento do jogo.

```mermaid
erDiagram

    JOGADOR ||--o| PERSONAGEM : possui
    EPOCA_HISTORICA ||--o{ MISSAO : possui
    MISSAO ||--o{ PERGUNTA : possui
    JOGADOR ||--o{ PROGRESSO : possui
    MISSAO ||--o{ PROGRESSO : possui

    JOGADOR {
        int id PK
        string nome
        string email
        int idade
    }

    PERSONAGEM {
        int id PK
        int jogador_id FK
        string nome
        string classe
        int nivel
        int experiencia
    }

    EPOCA_HISTORICA {
        int id PK
        string nome
        string descricao
    }

    MISSAO {
        int id PK
        int epoca_id FK
        string titulo
        string descricao
        int dificuldade
        int recompensa
    }

    PERGUNTA {
        int id PK
        int missao_id FK
        string enunciado
        string resposta_correta
        string explicacao
    }

    PROGRESSO {
        int id PK
        int jogador_id FK
        int missao_id FK
        string status
        int percentual
    }
