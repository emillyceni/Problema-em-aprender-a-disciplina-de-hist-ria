# Modelagem Inicial — AprendeRPG

## Fluxograma Inicial

```mermaid
flowchart TD
    A([Início]) --> B[Jogador entra no jogo]
    B --> C[Escolhe uma época histórica]
    C --> D[Escolhe uma missão]
    D --> E[Responde uma pergunta]
    
    E --> F{Resposta correta?}
    
    F -- Sim --> G[Ganha recompensa]
    F -- Não --> H[Recebe explicação]
    
    H --> E
    G --> I[Atualiza progresso]
    I --> J([Fim])
Funcionamento

O jogador entra no jogo, escolhe uma época histórica e inicia uma missão.

Durante a missão, ele responde perguntas relacionadas ao conteúdo de História.

Se acertar, recebe uma recompensa e avança.
Se errar, recebe uma explicação e pode tentar novamente.
O progresso é atualizado ao longo da missão.
Entidades Principais
Jogador: usuário que utiliza o jogo.
Personagem: personagem controlado pelo jogador.
Época Histórica: período histórico disponível.
Missão: atividade realizada dentro de uma época.
Pergunta: desafio histórico da missão.
Progresso: registra o avanço do jogador.
Modelo Inicial
Estrutura Básica
Jogador
   ↓
Personagem
   ↓
Época Histórica
   ↓
Missão
   ↓
Pergunta
   ↓
Progresso


    JOGADOR ||--|| PERSONAGEM : possui
    EPOCA_HISTORICA ||--o{ MISSAO : possui
    MISSAO ||--o{ PERGUNTA : possui
    JOGADOR ||--o{ PROGRESSO : possui
    MISSAO ||--o{ PROGRESSO : registra
