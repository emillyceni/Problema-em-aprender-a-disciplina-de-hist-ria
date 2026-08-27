# Fluxogramas dos Requisitos — AprendeRPG

> Um fluxograma para cada Requisito Funcional (RF), detalhando o comportamento esperado do sistema. Local sugerido no repositório: `/docs/fluxogramas_requisitos.md`

---

## RF01 — Mecânica de Quiz em Batalhas

```mermaid
flowchart TD
    Start([Início do combate]) --> Encontro[Jogador encontra\ninimigo/desafio]
    Encontro --> Pergunta[Sistema apresenta\npergunta histórica]
    Pergunta --> Resposta{Jogador responde\ncorretamente?}
    Resposta -- Sim --> Ataca[Personagem executa\nataque/magia com sucesso]
    Resposta -- Não --> Falha[Ataque falha ou\npersonagem sofre dano]
    Ataca --> Continua{Inimigo/desafio\nderrotado?}
    Falha --> Continua
    Continua -- Não --> Pergunta
    Continua -- Sim --> Vitoria[Batalha vencida]
    Vitoria --> Fim([Fim do combate])
```

---

## RF02 — Sistema de Linha do Tempo Visual

```mermaid
flowchart TD
    Start([Jogador acessa o mapa]) --> Verifica{Era histórica\ndesbloqueada?}
    Verifica -- Não --> Bloqueado[Exibe era bloqueada\ncom requisito para liberar]
    Verifica -- Sim --> Selecionar[Seleciona a era histórica]
    Selecionar --> Entrar[Entra no cenário da era]
    Entrar --> Progresso[Explora e completa\nmissões da era]
    Progresso --> Requisito{Cumpriu requisitos\nda próxima era?}
    Requisito -- Sim --> Libera[Desbloqueia próxima\nera no mapa]
    Requisito -- Não --> Permanece[Permanece\nna era atual]
    Bloqueado --> Fim([Retorna ao mapa])
    Libera --> Fim
    Permanece --> Fim
```

---

## RF03 — Diálogos com Figuras Históricas

```mermaid
flowchart TD
    Start([Jogador encontra NPC histórico]) --> Iniciar[Inicia o diálogo]
    Iniciar --> Fala[NPC apresenta\ncontexto da época]
    Fala --> Opcao{Jogador escolhe\numa opção de diálogo}
    Opcao -- Perguntar sobre a época --> Pista[NPC fornece\npista ou contexto extra]
    Opcao -- Aceitar missão --> Missao[Nova missão\né adicionada ao jogador]
    Opcao -- Encerrar conversa --> Fim([Fim do diálogo])
    Pista --> Opcao
    Missao --> Fim
```

---

## RF04 — Diário/Inventário do Conhecimento

```mermaid
flowchart TD
    Start([Jogador encontra item\nou fato histórico]) --> Coletar[Coleta o item\nou registro]
    Coletar --> Salvar[Item é salvo no\nDiário do Conhecimento]
    Salvar --> Categoriza[Item categorizado\npor época e tema]
    Categoriza --> Consulta{Jogador deseja\nconsultar o diário?}
    Consulta -- Sim --> Abre[Abre o Diário/Inventário]
    Abre --> Visualiza[Visualiza itens,\ndescrições e curiosidades]
    Visualiza --> Fim([Fecha o diário])
    Consulta -- Não --> Fim
```

---

## RF05 — Níveis de Dificuldade Adaptativos

```mermaid
flowchart TD
    Start([Jogador responde\nperguntas no jogo]) --> Avalia[Sistema avalia\nacertos e erros recentes]
    Avalia --> Nivel{Qual o padrão\nde desempenho?}
    Nivel -- Muitos acertos --> Aumenta[Aumenta a dificuldade\ndas próximas perguntas]
    Nivel -- Muitos erros --> Diminui[Reduz a dificuldade e\nsimplifica a linguagem]
    Nivel -- Desempenho estável --> Mantem[Mantém o\nnível atual]
    Aumenta --> Ajusta[Ajusta banco de perguntas\npor idade e nível do jogador]
    Diminui --> Ajusta
    Mantem --> Ajusta
    Ajusta --> Fim([Próxima pergunta é gerada])
```

---

## RF06 — Feedback Educativo Imediato

```mermaid
flowchart TD
    Start([Jogador responde\numa pergunta]) --> Verifica{Resposta\ncorreta?}
    Verifica -- Sim --> Positivo[Exibe feedback positivo]
    Positivo --> Continua([Jogo segue normalmente])
    Verifica -- Não --> Explicacao[Exibe explicação contextualizada\ndo fato histórico]
    Explicacao --> NovaTentativa[Permite nova tentativa\nda pergunta]
    NovaTentativa --> Continua
```

---

## RF07 — Relatório de Desempenho

```mermaid
flowchart TD
    Start([Fim de uma sessão\nou missão]) --> Coleta[Sistema coleta todas\nas respostas do jogador]
    Coleta --> Analisa[Analisa acertos e erros\npor tópico histórico]
    Analisa --> Gera[Gera relatório com pontos\nfortes e pontos de dificuldade]
    Gera --> Envia{Enviar relatório para\nresponsável/professor?}
    Envia -- Sim --> Notifica[Notifica responsável\nou professor]
    Envia -- Não --> Salva[Salva relatório\nno perfil do jogador]
    Notifica --> Fim([Fim])
    Salva --> Fim
```

---

## RNF05 — Funcionamento Offline (complemento)

Fluxo de apoio ao requisito não funcional de funcionamento offline, mostrando como o progresso é tratado sem conexão.

```mermaid
flowchart TD
    Start([Jogador abre o jogo]) --> Conexao{Há conexão\ncom a internet?}
    Conexao -- Não --> ModoOffline[Jogo carrega dados\nlocais já baixados]
    ModoOffline --> JogaOffline[Jogador joga normalmente\nmissões e quizzes]
    JogaOffline --> SalvaLocal[Progresso salvo\nlocalmente no dispositivo]
    SalvaLocal --> Espera{Conexão\nrestabelecida?}
    Espera -- Não --> SalvaLocal
    Espera -- Sim --> Sincroniza[Sincroniza progresso\ncom o servidor]

    Conexao -- Sim --> ModoOnline[Jogo carrega dados\ndo servidor]
    ModoOnline --> JogaOnline[Jogador joga normalmente]
    JogaOnline --> SalvaServidor[Progresso salvo\nno servidor em tempo real]

    Sincroniza --> Fim([Progresso atualizado])
    SalvaServidor --> Fim
```
