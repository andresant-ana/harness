# Skill — Project State Maintainer

## Finalidade

Esta skill orienta a manutenção do `PROJECT_STATE.md` no workspace de um projeto.

Seu papel é garantir que mudanças duráveis, decisões, riscos, limitações, dívidas conscientes e realidade operacional sobrevivam à sessão, ao agente e ao transcript.

---

## Quando usar

Use esta skill quando uma task produzir ou alterar:

- decisão técnica durável;
- estado arquitetural;
- boundary;
- risco conhecido;
- limitação técnica;
- dívida consciente;
- comando local relevante;
- integração;
- execution model;
- operational reality;
- descoberta factual relevante;
- follow-up estrutural;
- divergência entre documentação e código.

---

## Quando não usar

Não use esta skill quando:

- a mudança for trivial;
- a informação for efêmera;
- o Completion Packet já bastar;
- a atualização duplicaria issue ou board;
- o state viraria changelog;
- não houver impacto durável.

---

## Tese central

`PROJECT_STATE.md` não é diário.  
É memória técnica viva.

Ele deve responder:

- em que estado técnico o projeto está?
- que decisões estão ativas?
- que riscos são conhecidos?
- que limitações importam?
- que próximos passos técnicos precisam sobreviver?

---

## Método

### 1. Decidir se deve atualizar

Perguntar:

- isso muda como entender o projeto?
- muda como operar?
- muda como evoluir?
- muda arquitetura ou boundary?
- registra risco ou limitação?
- evita reinvestigação?
- registra dívida consciente?
- altera comando ou integração?

Se não, não atualizar.

---

### 2. Classificar tipo de entrada

Usar uma das categorias:

- estado técnico;
- decisão;
- risco;
- limitação;
- dívida técnica;
- comando;
- integração;
- arquitetura;
- operação;
- segurança;
- follow-up.

---

### 3. Determinar origem

A entrada pode vir de:

- Completion Packet;
- Investigation Note;
- Review Report;
- Escalation Note;
- ADR;
- issue;
- PR;
- decisão humana;
- Core Architect.

---

### 4. Criar ou atualizar entrada

Decidir:

- criar nova entrada;
- atualizar entrada existente;
- marcar entrada como resolvida;
- marcar como substituída;
- marcar como obsoleta;
- consolidar ruído.

---

### 5. Escrever de forma densa e curta

Uma boa entrada deve ser:

- factual;
- durável;
- contextual;
- acionável;
- referenciada;
- útil para futura sessão.

---

### 6. Não duplicar board

Board organiza trabalho.  
`PROJECT_STATE.md` preserva verdade técnica.

Não copiar issue para state.  
Registrar apenas o estado técnico que a issue revelou ou alterou.

---

## Output esperado

```md
# Project State Maintenance

## Deve atualizar PROJECT_STATE?
<sim | não | incerto>

## Motivo
<por que a informação é ou não durável>

## Tipo de atualização
<estado técnico | decisão | risco | limitação | dívida técnica | comando | integração | arquitetura | operação | segurança | follow-up>

## Origem
<Completion Packet | Investigation Note | Review Report | ADR | issue | PR | decisão humana | Core Architect>

## Entrada proposta
<texto proposto para PROJECT_STATE.md>

## Referências
- <arquivo, commit, issue, PR, ADR ou artifact>

## Status
<ativo | resolvido | substituído | obsoleto | em observação | pendente de decisão>

## Risco de ruído
<baixo | moderado | alto>
```

---

## Checklist de qualidade

Antes de atualizar, verificar:

- a informação é durável?
- state é o lugar certo?
- não é changelog?
- não duplica board?
- há origem clara?
- há referência?
- há status?
- há impacto?
- a entrada ajudará futura sessão?
- a entrada é curta o suficiente?

---

## Critérios de escalonamento

Escalar quando:

- a entrada envolve decisão arquitetural não aprovada;
- há conflito entre state e código;
- PROJECT_STATE está obsoleto;
- não está claro se a informação é durável;
- a atualização pode redefinir entendimento do projeto;
- há risco de transformar state em backlog;
- a entrada depende de decisão do Core Architect.

---

## Anti-patterns

Evitar:

- registrar tudo;
- copiar Completion Packet inteiro;
- copiar issue inteira;
- registrar detalhe efêmero;
- transformar PROJECT_STATE em changelog;
- deixar risco durável fora do state;
- registrar decisão sem origem;
- registrar follow-up sem critério;
- manter entradas obsoletas como ativas.

---

## Declaração operacional curta

`PROJECT_STATE.md` preserva verdade técnica durável.  
Atualize quando muda o entendimento futuro; não atualize para registrar ruído.