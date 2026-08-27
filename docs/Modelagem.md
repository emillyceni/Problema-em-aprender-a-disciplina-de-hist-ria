# Arquitetura da Solução — RPG Educativo de História

## 1. Fluxo do sistema

```mermaid
flowchart TD
    A[Aluno] --> B{Login / Cadastro}
    B --> C[Selecionar fase de história]
    C --> D[Jogar fase - RPG interativo]
    D --> E[Responder desafios e quizzes]
    E --> F{Acertou?}
    F -->|Sim| G[Ganha pontos e avança de fase]
    F -->|Não| H[Recebe dica e tenta novamente]
    G --> I[(Banco de dados)]
    H --> D
    I --> J[Salvar progresso do aluno]
    J --> K[Professor acompanha desempenho]
```

## 2. Arquitetura em camadas

```mermaid
graph LR
    Frontend[Frontend - Jogo Web/Mobile] --> API[Backend API]
    API --> Auth[Módulo de autenticação]
    API --> Fases[Módulo de fases e conteúdo histórico]
    API --> Progresso[Módulo de progresso e pontuação]
    API --> Acess[Módulo de acessibilidade]
    Auth --> DB[(Banco de dados)]
    Fases --> DB
    Progresso --> DB
    Acess --> DB
```

## 3. Modelo de dados (entidades principais)

```mermaid
erDiagram
    ALUNO ||--o{ PROGRESSO : possui
    FASE ||--o{ PROGRESSO : referencia
    FASE ||--o{ DESAFIO : contem
    ALUNO {
        int id PK
        string nome
        string email
        int idade
        string tipo_acessibilidade "nenhum, baixa visao, daltonismo, outro"
    }
    FASE {
        int id PK
        string titulo "ex: Historia do Brasil, Guerra Fria"
        string descricao
        int ordem
        string tema_visual "cores claras e simples"
    }
    DESAFIO {
        int id PK
        int fase_id FK
        string pergunta
        string tipo "quiz, escolha, arraste e solte"
        string resposta_correta
    }
    PROGRESSO {
        int id PK
        int aluno_id FK
        int fase_id FK
        int pontuacao
        boolean concluida
        date data_ultima_jogada
    }
```

## 4. Justificativa das escolhas

- **Frontend web/mobile**: garante que o jogo funcione tanto em computadores da escola quanto em celulares e tablets em casa.
- **Módulo de autenticação**: permite identificar o aluno e salvar seu progresso individual, além de diferenciar o acesso do professor.
- **Módulo de fases e conteúdo histórico**: organiza o jogo em fases temáticas (História do Brasil, Guerra Fria, etc.), permitindo expandir o conteúdo facilmente com novos temas no futuro.
- **Módulo de progresso e pontuação**: registra o desempenho de cada aluno, permitindo que o professor acompanhe a evolução da turma e identifique dificuldades específicas.
- **Módulo de acessibilidade**: cobre o requisito de cores claras, simples e de fácil entendimento, adaptando o jogo para alunos com deficiência visual ou outras necessidades.
- **Desafios em formato de quiz e interações lúdicas**: tornam o aprendizado mais intuitivo e engajador, reforçando o conteúdo através da prática e repetição espaçada.
- **Link para o Trello:** https://trello.com/invite/b/6a904838e8e74e40bcb39308/ATTIe9681c31babd2c278316ce89ad6a2d9dFDE12283/jogo-rpg
