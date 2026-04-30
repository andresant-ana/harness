# Skill — Architecture by Pain Check

## Finalidade

Esta skill verifica se uma decisão arquitetural, abstração, camada, interface, integração ou padrão está sendo introduzido por dor real ou por antecipação especulativa.

Seu papel é proteger o projeto contra over-engineering, abstraction bloat e cerimônia arquitetural sem benefício proporcional.

---

## Quando usar

Use esta skill quando a task propuser:

- nova camada;
- nova interface;
- novo serviço;
- novo mapper;
- novo DTO;
- novo adapter;
- novo módulo;
- novo padrão arquitetural;
- nova dependência;
- mensageria;
- CQRS;
- event sourcing;
- microserviço;
- repository abstraction;
- separação estrutural relevante;
- refactor com aumento de arquivos.

---

## Quando não usar

Não use esta skill quando:

- a mudança for puramente local;
- a arquitetura já estiver definida por authority source;
- a alteração não introduzir complexidade nova;
- a task for correção simples sem decisão estrutural.

---

## Tese central

Complexidade só entra quando paga aluguel.

Uma abstração boa reduz dor real.  
Uma abstração ruim cria custo futuro para resolver problema imaginário.

O objetivo não é evitar arquitetura.  
O objetivo é evitar arquitetura sem causa.

---

## Perguntas centrais

Antes de aceitar complexidade nova, responder:

1. qual dor real esta complexidade resolve?
2. essa dor já aconteceu ou é imaginada?
3. há segunda ocorrência concreta?
4. há variação real que justifique abstração?
5. há dependência externa frágil que precisa ser isolada?
6. há boundary de domínio sendo protegido?
7. qual custo essa abstração adiciona?
8. o sistema fica mais fácil ou mais difícil para humanos e agentes?
9. qual seria a solução simples?
10. por que a solução simples não basta?

---

## Método

### 1. Identificar a complexidade proposta

Declarar exatamente o que está sendo introduzido.

Exemplos:

- interface;
- camada;
- evento;
- broker;
- módulo;
- wrapper;
- service;
- mapper;
- pattern;
- dependência externa.

---

### 2. Identificar a dor alegada

A dor precisa ser concreta.

Boas dores:

- duplicação real;
- acoplamento que já atrapalha;
- boundary violado;
- dependência externa instável;
- risco de segurança;
- necessidade de observabilidade;
- mudança recorrente;
- limitação operacional confirmada.

Dores fracas:

- “pode precisar no futuro”;
- “é mais limpo”;
- “é padrão de mercado”;
- “fica enterprise”;
- “a IA sugeriu”;
- “vi em arquitetura X”.

---

### 3. Avaliar evidência da dor

Perguntar:

- onde a dor aparece?
- em quais arquivos?
- em quais fluxos?
- que bug, retrabalho ou risco ela causa?
- há registro no PROJECT_STATE?
- há issue, review ou observação concreta?

Sem evidência, tratar como hipótese.

---

### 4. Comparar com solução simples

A solução simples deve ser considerada antes da complexa.

Perguntar:

- resolver localmente basta?
- encapsulamento simples basta?
- função simples basta?
- recurso nativo da stack basta?
- documentação ou teste bastam?
- adiar com critério de revisão basta?

---

### 5. Avaliar custo de navegação

Toda complexidade afeta agentes e humanos.

Verificar se a proposta:

- aumenta número de arquivos por feature;
- exige mais contexto;
- cria indireção;
- dificulta grep;
- torna o fluxo menos óbvio;
- aumenta chance de o agente ignorar arquivos críticos.

---

### 6. Decidir

Classificar a proposta como:

- justificada agora;
- aceitável com ressalvas;
- adiar até segunda ocorrência;
- rejeitar por over-engineering;
- escalar para Core Architect.

---

## Output esperado

```md
# Architecture by Pain Check

## Complexidade proposta
<o que está sendo introduzido>

## Dor alegada
<qual problema isso resolveria>

## Evidência da dor
- <evidência 1>
- <evidência 2>

## Solução simples considerada
<alternativa mais simples>

## Custo da complexidade
- <custo 1>
- <custo 2>

## Impacto em navegação/contexto
<como afeta humanos e agentes>

## Veredito
<justificada agora | aceitar com ressalvas | adiar | rejeitar | escalar>

## Critério para revisitar
<quando a complexidade passaria a ser justificada>
```

---

## Checklist de qualidade

Antes do veredito, confirmar:

- a dor é real?
- há evidência?
- existe solução simples?
- a complexidade reduz risco ou só parece elegante?
- o custo de manutenção foi considerado?
- o custo de contexto foi considerado?
- há critério de revisão futura?
- o Core Architect precisa arbitrar?

---

## Critérios de aceitação

Aceitar complexidade quando:

- há dor real;
- a solução simples é insuficiente;
- o custo é proporcional;
- a decisão preserva clareza;
- há validação ou review;
- o risco reduzido compensa o peso estrutural.

---

## Critérios de rejeição

Rejeitar ou adiar quando:

- a dor é hipotética;
- não há segunda ocorrência;
- a abstração só melhora estética;
- o número de arquivos aumenta sem ganho;
- a solução simples resolveria;
- a complexidade piora contexto para agentes;
- a decisão parece induzida por padrão de treinamento da IA.

---

## Anti-patterns

Evitar:

- interface para tudo;
- camada para cada conceito;
- mapper sem boundary real;
- repository genérico sem necessidade;
- CQRS para CRUD simples;
- event sourcing sem auditoria/event history real;
- mensageria para evitar chamada direta sem dor concreta;
- microserviço antes de boundary e escala justificarem;
- refactor preventivo dentro de feature pequena.

---

## Declaração operacional curta

Arquitetura entra por dor, não por vaidade.  
Se a complexidade não paga aluguel, ela é dívida.