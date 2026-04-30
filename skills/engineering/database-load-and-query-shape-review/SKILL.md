# Skill — Messaging Justification Review

## Finalidade

Esta skill orienta a decisão sobre uso de mensageria, eventos, filas, pub/sub, brokers e comunicação assíncrona.

Seu papel é impedir que o agente introduza Kafka, RabbitMQ, Azure Service Bus, filas ou eventos apenas por sofisticação arquitetural, sem dor real, sem modelo de falha e sem necessidade operacional.

---

## Quando usar

Use esta skill quando a task propuser ou tocar:

- fila;
- evento;
- broker;
- pub/sub;
- mensageria assíncrona;
- worker consumidor;
- outbox;
- event-driven architecture;
- integração entre módulos via evento;
- desacoplamento temporal;
- processamento eventual;
- retry assíncrono;
- workflow distribuído.

---

## Quando não usar

Não use esta skill quando:

- a comunicação direta já é suficiente e não está em discussão;
- a task apenas consome uma fila já estabelecida;
- não há decisão arquitetural nova;
- a análise só repetiria authority source já existente.

---

## Tese central

Mensageria não é upgrade automático de arquitetura.

Ela resolve dores reais, mas introduz custos reais:

- consistência eventual;
- duplicidade;
- ordenação;
- retry;
- observabilidade;
- dead-letter;
- idempotência;
- operação;
- debugging distribuído;
- custo de infraestrutura.

A pergunta correta é:

“qual dor justifica trocar simplicidade síncrona por complexidade assíncrona?”

---

## Dores que podem justificar mensageria

Mensageria pode ser justificada quando há:

- desacoplamento temporal real;
- trabalho demorado fora da request;
- necessidade de absorver pico;
- integração com sistema instável;
- processamento assíncrono natural;
- fan-out para múltiplos consumidores;
- necessidade de retry controlado;
- isolamento de falha;
- evento de domínio relevante;
- auditoria ou trilha de eventos real.

---

## Dores fracas

Mensageria é suspeita quando a justificativa é:

- “fica mais escalável” sem evidência;
- “é arquitetura moderna”;
- “evita acoplamento” sem dor concreta;
- “podemos precisar no futuro”;
- “microserviços usam”;
- “a IA sugeriu”;
- “deixa mais enterprise”.

---

## Método

### 1. Definir fluxo atual

Mapear:

- produtor;
- consumidor;
- ação desejada;
- necessidade de resposta imediata;
- consistência esperada;
- volume;
- frequência;
- falhas possíveis.

---

### 2. Comparar com alternativa simples

Comparar mensageria com:

- chamada direta;
- transação local;
- job agendado;
- background task local;
- processamento síncrono;
- banco como fonte de estado;
- solução manual temporária.

---

### 3. Avaliar consequências

Se usar mensageria, responder:

- mensagem pode duplicar?
- ordem importa?
- consumidor é idempotente?
- há dead-letter?
- há retry?
- há observabilidade?
- há contrato de mensagem?
- há versionamento?
- há outbox/inbox se necessário?
- o que acontece se broker cair?

---

### 4. Avaliar operação

Perguntar:

- quem opera broker?
- como monitora fila?
- como detecta stuck messages?
- como reprocessa?
- como lida com poison message?
- qual custo cloud/infra?
- qual blast radius?

---

### 5. Decidir

Classificar:

- chamada direta suficiente;
- mensageria justificada;
- adiar e registrar critério;
- escalar para Core Architect.

---

## Output esperado

```md
# Messaging Justification Review

## Fluxo analisado
<produtor, consumidor e operação>

## Dor real alegada
<por que mensageria está sendo considerada>

## Alternativa simples
<chamada direta | job | transação local | outra>

## Justificativa
<forte | fraca | insuficiente>

## Consequências operacionais
- <duplicidade>
- <ordem>
- <retry>
- <DLQ>
- <observabilidade>

## Requisitos mínimos se adotada
- <requisito 1>
- <requisito 2>

## Veredito
<usar chamada direta | adotar mensageria | adiar | escalar>

## Critério de revisão futura
<quando reavaliar>
```

---

## Checklist de qualidade

Antes de aceitar mensageria, verificar:

- há dor real?
- chamada direta falha por quê?
- consistência eventual é aceitável?
- duplicidade foi considerada?
- idempotência existe?
- ordenação importa?
- retry é seguro?
- DLQ foi considerada?
- observabilidade existe?
- contrato de mensagem está claro?
- operação foi considerada?

---

## Critérios de escalonamento

Escalar quando:

- mensageria alterar arquitetura;
- houver integração crítica;
- houver consistência eventual em domínio sensível;
- houver necessidade de outbox;
- houver múltiplos consumidores;
- houver custo operacional relevante;
- houver dúvida entre evento de domínio e evento técnico;
- houver impacto em produto ou SLA.

---

## Anti-patterns

Evitar:

- Kafka para CRUD simples;
- fila para esconder lentidão sem entender causa;
- evento sem consumidor real;
- consumidor não idempotente;
- retry infinito;
- ausência de DLQ;
- contrato de mensagem implícito;
- usar mensageria para compensar modularização ruim;
- distribuir sistema antes de entender domínio.

---

## Declaração operacional curta

Mensageria compra desacoplamento e resiliência pagando com complexidade operacional.  
Só use quando a dor real justificar o custo.