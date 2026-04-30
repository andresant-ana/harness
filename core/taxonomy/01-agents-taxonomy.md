# Taxonomia de Agentes

## Finalidade

Este documento classifica os agentes canônicos do harness, explicando o papel de cada um, quando devem ser usados, quais artifacts produzem ou consomem e quais limites devem respeitar.

A taxonomia não substitui os contratos completos em `agents/`.  
Ela funciona como mapa de papéis.

---

## Tese central

Agente não é personalidade.  
Agente é papel operacional.

Cada agente existe para reduzir ambiguidade no fluxo, separar responsabilidades e impedir que um único executor misture planejamento, pesquisa, implementação, review, crítica arquitetural e handoff sem disciplina.

---

## Agentes canônicos

```text
agents/
├─ planner.md
├─ researcher.md
├─ implementer.md
├─ reviewer.md
├─ architect-critic.md
├─ delivery-prep.md
└─ mcp-observer.md
```

---

## Visão geral

| Agente | Função principal | Saída típica |
|--------|------------------|--------------|
| `planner` | Converter demanda em plano executável | Execution Plan |
| `researcher` | Investigar fatos, docs e contexto | Investigation Note |
| `implementer` | Executar mudança dentro do envelope | Diff + Completion Packet |
| `reviewer` | Revisar plano, mudança ou saída | Review Report |
| `architect-critic` | Criticar arquitetura, complexidade e trade-offs | Review estratégico ou Escalation Note |
| `delivery-prep` | Preparar fechamento, handoff e continuidade | Completion Packet / Handoff |
| `mcp-observer` | Ler estado externo via MCP/read-only | Investigation Note / contexto factual |

---

## `planner`

### Função

Transformar Implementation Packet, contexto e discovery inicial em Execution Plan.

### Quando usar

Usar quando:
- a task não é trivial;
- há risco R1+;
- há múltiplos caminhos possíveis;
- o executor precisa de plano antes de mutar;
- a tarefa exige validação ou review.

### Quando não usar

Não usar quando:
- a task é leitura simples R0;
- a saída esperada é apenas investigação;
- já existe Execution Plan aprovado e ainda válido.

### Artifacts típicos

Consome:
- Implementation Packet;
- Investigation Note;
- authority sources;
- Project State Entry relevante.

Produz:
- Execution Plan;
- Escalation Note, se o plano não puder ser fechado.

### Limites

O `planner` não deve:
- implementar;
- decidir arquitetura estrutural sozinho;
- esconder incerteza;
- transformar plano em manifesto abstrato.

---

## `researcher`

### Função

Investigar fatos, documentação, repositório, dependências, issues, PRs ou comportamento antes de execução.

### Quando usar

Usar quando:
- a task é R0;
- há dúvida factual;
- há comportamento desconhecido;
- é necessário investigar antes de planejar;
- docs, issues ou código precisam ser analisados sem mutação.

### Quando não usar

Não usar para:
- implementar mudança;
- substituir plan;
- justificar decisão sem evidência;
- fazer leitura externa sem pergunta clara.

### Artifacts típicos

Consome:
- pergunta de investigação;
- authority sources;
- docs;
- código;
- MCP read-only.

Produz:
- Investigation Note;
- Escalation Note, quando investigação revelar decisão fora do envelope.

### Limites

O `researcher` separa fato de hipótese.  
Não deve converter hipótese em conclusão sem evidência.

---

## `implementer`

### Função

Executar a mudança aprovada dentro do envelope do plan.

### Quando usar

Usar quando:
- há Execution Plan suficiente;
- a task tem escopo claro;
- a classe de risco permite execução;
- mutação local está autorizada.

### Quando não usar

Não usar quando:
- falta plan;
- a task é estrutural sem aprovação;
- a classe de risco subiu para R3/R4;
- há ambiguidade estratégica;
- a execução exigiria segredo, produção ou ação sensível.

### Artifacts típicos

Consome:
- Execution Plan;
- authority sources;
- protocols;
- policies;
- skills aplicáveis.

Produz:
- diff;
- validações;
- Completion Packet;
- Escalation Note, se necessário.

### Limites

O `implementer` não deve:
- expandir escopo;
- redesenhar arquitetura;
- adicionar dependência sem policy;
- tocar produção;
- ocultar lacunas.

---

## `reviewer`

### Função

Avaliar plano, mudança, artifacts ou handoff de forma conservadora e baseada em evidência.

### Quando usar

Usar quando:
- há Execution Plan a validar;
- há diff relevante;
- há Completion Packet;
- a task é R2+;
- há risco de segurança, operação ou slop;
- a entrega precisa de parecer.

### Quando não usar

Não usar como:
- segunda implementação disfarçada;
- comentário superficial;
- aprovação automática;
- substituto de Core Architect em decisão estratégica pesada.

### Artifacts típicos

Consome:
- Execution Plan;
- diff;
- Completion Packet;
- authority sources;
- Evidence Standard.

Produz:
- Review Report.

### Limites

O `reviewer` deve decidir, não apenas comentar.

Vereditos esperados:
- aprovado;
- aprovado com ressalvas;
- reavaliar;
- bloquear.

---

## `architect-critic`

### Função

Avaliar decisões arquiteturais, complexidade, boundaries, abstrações, trade-offs e risco de over-engineering.

### Quando usar

Usar quando:
- há nova abstração;
- há mudança estrutural;
- há risco de cerimônia arquitetural;
- há decisão entre simples e sofisticado;
- há dúvida sobre CQRS, mensageria, event sourcing, microserviço, cloud runtime ou boundary;
- há suspeita de arquitetura por vaidade.

### Quando não usar

Não usar para:
- microdetalhe tático;
- code style;
- task trivial;
- implementação local sem impacto arquitetural.

### Artifacts típicos

Consome:
- Execution Plan;
- ADR;
- Investigation Note;
- Review Report;
- contexto arquitetural.

Produz:
- parecer arquitetural;
- Review Report;
- Escalation Note;
- recomendação de ADR.

### Limites

O `architect-critic` não deve sofisticar por prazer.  
Sua função é proteger proporcionalidade.

---

## `delivery-prep`

### Função

Preparar encerramento da task, handoff, atualização de state e sugestão de commit/PR.

### Quando usar

Usar quando:
- a task foi concluída;
- há necessidade de Completion Packet;
- há necessidade de state update;
- há continuidade futura;
- a entrega precisa ser organizada para humano ou Core Architect.

### Quando não usar

Não usar para:
- validar tecnicamente sozinho;
- substituir reviewer;
- escrever narrativa triunfal;
- esconder lacunas.

### Artifacts típicos

Consome:
- Completion Packet parcial;
- diff;
- validações;
- Review Report;
- Project State Entry schema.

Produz:
- Completion Packet final;
- sugestão de Project State Entry;
- handoff;
- sugestão de commit message.

### Limites

O `delivery-prep` organiza, não absolve.  
Se há lacuna, ela deve aparecer.

---

## `mcp-observer`

### Função

Consultar estado externo via MCP ou integrações read-only.

### Quando usar

Usar quando:
- é preciso ler GitHub Projects;
- é preciso consultar issue, PR ou board;
- há necessidade de contexto externo factual;
- observabilidade ou cloud metadata read-only ajudam a reduzir incerteza.

### Quando não usar

Não usar quando:
- a informação está no repositório;
- a consulta externa é curiosidade;
- a fonte não é confiável;
- exigiria escrita;
- substituiria discovery local.

### Artifacts típicos

Consome:
- pergunta externa clara;
- policy de MCP;
- trusted integrations;
- scope da consulta.

Produz:
- Investigation Note;
- trecho factual para Execution Plan;
- input para Escalation Note.

### Limites

O `mcp-observer` observa.  
Não age.

---

## Relação entre agentes no fluxo

Fluxo típico:

```text
Implementation Packet
↓
planner
↓
Execution Plan
↓
implementer
↓
Completion Packet
↓
reviewer
↓
delivery-prep
```

Fluxo investigativo:

```text
Pergunta factual
↓
researcher / mcp-observer
↓
Investigation Note
↓
planner ou Core Architect
```

Fluxo arquitetural:

```text
Execution Plan ou dúvida estrutural
↓
architect-critic
↓
Review Report ou Escalation Note
↓
humano / Core Architect
```

---

## Anti-patterns de agentes

Evitar:

- um agente fazendo tudo;
- `implementer` decidindo arquitetura;
- `planner` escrevendo plano sem discovery;
- `reviewer` aprovando sem evidência;
- `architect-critic` sofisticando sem dor real;
- `mcp-observer` usando board como arquitetura;
- `delivery-prep` escondendo lacunas.

---

## Declaração operacional curta

Agentes são papéis, não avatares.  
Cada agente existe para separar responsabilidade, reduzir improviso e preservar qualidade.