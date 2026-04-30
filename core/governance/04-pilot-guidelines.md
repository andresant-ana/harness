# Diretrizes de Piloto Controlado

## Finalidade

Este documento define como conduzir o piloto controlado do harness antes de considerar a engenharia estável.

Seu papel é validar comportamento real em tasks reais ou simuladas, sem transformar a primeira versão operacional em dogma.

O piloto existe para descobrir:
- o que funciona;
- o que trava;
- o que gera burocracia;
- o que reduz slop;
- o que precisa ser cortado;
- o que precisa ser endurecido.

---

## Tese central

Harness não se valida por documentação.  
Harness se valida por comportamento.

O piloto deve testar se a engenharia melhora:
- planejamento;
- execução;
- evidência;
- review;
- handoff;
- segurança;
- produção;
- controle de entropia;
- continuidade.

---

## Objetivos do piloto

O piloto deve responder:

1. o agente entende e segue o fluxo?
2. o plan melhora a execução?
3. o discovery reduz erro?
4. artifacts ajudam ou burocratizam?
5. review detecta problemas reais?
6. handoff preserva continuidade?
7. policies bloqueiam riscos relevantes?
8. o sistema evita over-engineering?
9. o contexto fica controlado?
10. o humano sente mais controle ou mais fricção?

---

## Escopo do piloto

O piloto deve ser controlado.

Recomenda-se usar:
- projeto pessoal;
- branch separada;
- worktree quando necessário;
- tasks de risco baixo a moderado;
- sem produção real;
- sem segredo real;
- sem MCP write sensível.

O objetivo inicial não é provar tudo.  
É observar comportamento com segurança.

---

## O que não testar no primeiro piloto

Não testar inicialmente:

- deploy real;
- produção;
- segredo;
- automação write;
- MCP write;
- migração de banco real;
- mudança irreversível;
- plugin complexo;
- múltiplos agentes paralelos sem controle;
- tasks R4.

---

## Tipos de task recomendados

O piloto deve incluir cenários como:

### 1. Task R0 investigativa
Objetivo:
- validar Investigation Note;
- avaliar factualidade;
- testar external state reading, se necessário.

### 2. Task R1 simples
Objetivo:
- verificar se o harness não burocratiza demais;
- testar menor diff;
- testar Completion Packet enxuto.

### 3. Task R2 funcional
Objetivo:
- testar Implementation Packet;
- Execution Plan;
- validação;
- Review Report;
- Completion Packet.

### 4. Task com risco de over-engineering
Objetivo:
- testar architecture by pain;
- entropy management;
- architect-critic.

### 5. Task com dependência nova
Objetivo:
- testar dependency policy;
- segurança;
- review.

### 6. Task com banco ou query
Objetivo:
- testar produção, performance, evidência e state.

### 7. Task que deveria escalar
Objetivo:
- verificar se o agente reconhece limite de autonomia.

### 8. Task que exige PROJECT_STATE
Objetivo:
- validar Project State Entry e state maintenance.

---

## Métricas observadas

Durante piloto, observar:

- flow adherence;
- plan specificity;
- evidence strength;
- review decision clarity;
- handoff continuity;
- entropy delta;
- correct escalation;
- context load;
- project state usefulness;
- skill usefulness;
- human friction.

---

## Registro de piloto

Cada task piloto deve registrar:

```md
## Task piloto

### Referência
<issue | branch | worktree | descrição>

### Classe de risco
R0 | R1 | R2 | R3 | R4

### Objetivo
<objetivo da task>

### Artifacts usados
- <artifact 1>
- <artifact 2>

### O que funcionou
- <item 1>
- <item 2>

### O que falhou
- <item 1>
- <item 2>

### Fricções
- <fricção 1>
- <fricção 2>

### Sinais de slop ou entropia
- <sinal 1>
- <sinal 2>

### Ajustes sugeridos
- <ajuste 1>
- <ajuste 2>

### Veredito
<manter | ajustar | cortar | reavaliar>
```

---

## Critério para ajustar durante piloto

Ajustar imediatamente quando:

- policy permite risco alto sem bloqueio;
- agent viola fronteira de autonomia;
- artifact essencial é confuso;
- fluxo causa erro recorrente;
- segurança ou produção ficam mal protegidas.

Não ajustar imediatamente quando:

- a fricção ocorreu uma vez;
- o problema pode ser mau uso;
- ainda não há padrão;
- o ajuste aumentaria complexidade cedo demais.

---

## Critério para sucesso do piloto

O piloto é saudável quando:

- tasks R1 não ficam burocráticas;
- tasks R2 ficam mais claras;
- tasks R3 escalam;
- review pega problemas reais;
- handoff melhora continuidade;
- state update acontece quando necessário;
- o agente reduz slop;
- o humano mantém controle.

---

## Critério para falha do piloto

O piloto falha quando:

- o agente ignora plan;
- artifacts viram ritual;
- contexto explode;
- review aprova tudo;
- policies não bloqueiam risco;
- Core Architect recebe contexto bagunçado;
- o humano trabalha mais para corrigir o harness do que a task;
- a engenharia induz over-engineering.

---

## Saídas esperadas do piloto

Ao final do piloto, produzir:

- lista de peças mantidas;
- lista de peças ajustadas;
- lista de peças removidas;
- backlog pós-piloto;
- decisão de maturidade;
- release candidate do harness.

---

## Declaração operacional curta

Piloto não é celebração.  
Piloto é teste controlado de comportamento real.  
O harness só amadurece quando suas regras melhoram a execução de verdade.