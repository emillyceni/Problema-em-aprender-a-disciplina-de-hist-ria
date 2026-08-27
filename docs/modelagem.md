erDiagram
    JOGADOR ||--|| PERSONAGEM : "controla"
    JOGADOR ||--o{ PROGRESSO_MISSAO : "possui"
    JOGADOR ||--o{ CONQUISTA_OBTIDA : "recebe"
    JOGADOR }o--o| RESPONSAVEL : "acompanhado por"

    EPOCA_HISTORICA ||--o{ MISSAO : "contextualiza"
    MISSAO ||--o{ PERGUNTA : "contém"
    MISSAO ||--o{ PROGRESSO_MISSAO : "gera"
    PERGUNTA ||--o{ RESPOSTA_JOGADOR : "recebe"
    CONQUISTA ||--o{ CONQUISTA_OBTIDA : "é concedida em"

    JOGADOR {
        int id PK
        string nome
        int idade
        string nivel_dificuldade
        int xp_total
        datetime criado_em
    }

    PERSONAGEM {
        int id PK
        int jogador_id FK
        string nome_personagem
        string classe
        string avatar_url
        int nivel
    }

    RESPONSAVEL {
        int id PK
        string nome
        string email
        string tipo
    }

    EPOCA_HISTORICA {
        int id PK
        string nome
        string periodo
        string descricao
        string imagem_capa_url
    }

    MISSAO {
        int id PK
        int epoca_id FK
        string titulo
        string narrativa
        string objetivo_pedagogico
        string dificuldade
    }

    PERGUNTA {
        int id PK
        int missao_id FK
        string enunciado
        string tipo
        string alternativa_correta
        string dica
    }

    RESPOSTA_JOGADOR {
        int id PK
        int pergunta_id FK
        int jogador_id FK
        string resposta_dada
        boolean correta
        datetime respondido_em
    }

    PROGRESSO_MISSAO {
        int id PK
        int jogador_id FK
        int missao_id FK
        string status
        int pontuacao
        int tentativas
        datetime atualizado_em
    }

    CONQUISTA {
        int id PK
        string nome
        string descricao
        string icone_url
    }

    CONQUISTA_OBTIDA {
        int id PK
        int jogador_id FK
        int conquista_id FK
        datetime obtido_em
    }
