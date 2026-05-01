# Agents

## Finalidade

Este diretório contém os contratos canônicos dos agentes do harness.

Agente não é personalidade.  
Agente é papel operacional.

Cada agente existe para separar responsabilidades, reduzir improviso e impedir que uma única execução misture planejamento, pesquisa, implementação, review, crítica arquitetural, leitura externa e handoff sem disciplina.

---

## Agentes canônicos

```text
agents/
├─ README.md
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
| `architect-critic` | Criticar arquitetura, complexidade e trade-offs | Parecer arquitetural / Escalation Note |
| `delivery-prep` | Preparar fechamento, handoff e continuidade | Completion Packet / Handoff |
| `mcp-observer` | Ler estado externo via MCP/read-only | Investigation Note / contexto factual |

---

## Regra central

Nenhum agente deve fazer tudo.

O harness separa papéis para evitar:

- plano escrito depois da execução;
- implementação sem discovery;
- crítica arquitetural misturada com preferência estética;
- review superficial;
- MCP usado como automação remota sem controle;
- handoff triunfalista escondendo lacunas;
- expansão de escopo não autorizada.

---

## Fluxos principais

### Fluxo de implementação

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

### Fluxo investigativo

```text
Pergunta factual
↓
researcher / mcp-observer
↓
Investigation Note
↓
planner ou Core Architect
```

### Fluxo arquitetural

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

## Relação com core

Os agentes devem obedecer:

- `core/constitution/`;
- `core/protocols/`;
- `core/policies/`;
- `core/artifacts/`;
- `core/taxonomy/`;
- `core/observability/`;
- `core/governance/`.

Agente não pode autorizar comportamento proibido por policy.

---

## Relação com skills

Agentes podem acionar skills quando a task exigir método especializado.

Exemplos:

- `planner` pode usar `implementation-planner`, `risk-classifier`, `task-decomposer`;
- `researcher` pode usar `repository-discovery-operator`, `docs-research-operator`, `mcp-readonly-operator`;
- `implementer` pode usar skills de stack, platform, security e engineering;
- `reviewer` pode usar `testing-verifier`, `secure-coding-baseline`, `architecture-drift-auditor`;
- `architect-critic` pode usar `architecture-tradeoff-analyst`, `architecture-by-pain-check`, `messaging-justification-review`;
- `delivery-prep` pode usar `delivery-wrapup`, `project-state-maintainer`, `doc-gardener`;
- `mcp-observer` pode usar `mcp-readonly-operator`, `github-projects-readonly`, `cloud-readonly-inspection`.

Skill é método acionável.  
Agente é papel responsável por aplicar ou solicitar esse método.

---

## Relação com artifacts

Agentes produzem e consomem artifacts canônicos:

- Implementation Packet;
- Execution Plan;
- Completion Packet;
- Review Report;
- Escalation Note;
- Investigation Note;
- Project State Entry.

Artifacts são memória formal do fluxo.  
Mensagem solta não substitui artifact quando o risco exige formalidade.

---

## Classes de risco

A classe de risco controla autonomia:

- R0: leitura/investigação;
- R1: mudança local pequena;
- R2: mudança funcional relevante;
- R3: mudança estrutural/sensível;
- R4: produção, segredo, irreversibilidade ou alto risco.

Agentes devem escalar quando a task sair do envelope autorizado.

---

## Limites gerais

Nenhum agente deve:

- tocar produção sem autorização explícita;
- manipular segredo real;
- executar comando destrutivo sem policy e aprovação;
- fazer MCP write sem autorização;
- criar dependência sem justificativa;
- expandir escopo silenciosamente;
- ocultar incerteza;
- declarar conclusão sem evidência;
- transformar over-engineering em “boa prática”.

---

## Anti-patterns globais

Evitar:

- um agente fazendo planejamento, implementação e review sozinho;
- `implementer` decidindo arquitetura;
- `planner` escrevendo plano sem discovery;
- `researcher` acumulando contexto sem pergunta;
- `reviewer` aprovando sem evidência;
- `architect-critic` sofisticando sem dor real;
- `delivery-prep` escondendo lacunas;
- `mcp-observer` confundindo board com verdade técnica.

---

## Declaração operacional curta

Agentes são papéis de controle.  
Cada agente reduz um tipo de erro: improviso, suposição, escopo solto, over-engineering, falta de evidência ou perda de continuidade.