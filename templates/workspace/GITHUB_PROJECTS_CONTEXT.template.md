# GitHub Projects Context

## Finalidade

Este documento descreve como este workspace usa GitHub Projects, issues, PRs e board.

Ele existe para permitir leitura segura e útil do board sem confundir gestão de trabalho com verdade técnica.

---

## Regra central

GitHub Projects organiza trabalho.  
`PROJECT_STATE.md` preserva verdade técnica.

Board não substitui:

- código;
- ADR;
- `PROJECT_STATE.md`;
- `AUTHORITY_SOURCES.md`;
- `OPERATIONAL_REALITY.md`;
- discovery local.

---

## Board principal

```text
Nome:
URL:
Owner/org:
Projeto:
Uso:
```

---

## Repositório

```text
Repo:
Default branch:
Branch policy:
PR policy:
Issue policy:
```

---

## Campos do board

| Campo | Significado | Observações |
|------|-------------|-------------|
| Status | `<como usar>` | `<observação>` |
| Priority | `<como usar>` | `<observação>` |
| Assignee | `<como usar>` | `<observação>` |
| Milestone | `<como usar>` | `<observação>` |
| Labels | `<como usar>` | `<observação>` |

Adicionar campos customizados:

| Campo | Significado | Observações |
|------|-------------|-------------|
| `<campo>` | `<significado>` | `<observação>` |

---

## Status workflow

| Status | Significado | Pode implementar? |
|--------|-------------|-------------------|
| Backlog | `<significado>` | `<sim/não>` |
| Ready | `<significado>` | `<sim/não>` |
| In Progress | `<significado>` | `<sim/não>` |
| Review | `<significado>` | `<sim/não>` |
| Done | `<significado>` | `<sim/não>` |
| Blocked | `<significado>` | `<sim/não>` |

---

## Labels importantes

| Label | Significado | Implicação |
|-------|-------------|------------|
| `<label>` | `<significado>` | `<implicação>` |

Exemplos:

| Label | Significado | Implicação |
|-------|-------------|------------|
| `risk:R3` | Mudança sensível | Requer review/escalonamento |
| `type:bug` | Correção | Exigir reprodução/validação |
| `area:backend` | Backend | Acionar skills de .NET/API/banco |
| `area:frontend` | Frontend | Acionar skills de React/frontend security |

---

## Como agentes devem consultar o board

Permitido em modo read-only:

- listar item;
- ler issue;
- ler status;
- ler prioridade;
- ler comentários relevantes;
- identificar PR vinculado;
- entender dependências.

Não permitido sem autorização:

- mover card;
- editar status;
- alterar label;
- fechar issue;
- comentar;
- criar item;
- alterar prioridade.

---

## Como interpretar issues

Issue pode conter:

- objetivo;
- contexto;
- critério de aceite;
- discussão;
- links;
- prioridade.

Issue não substitui:

- Execution Plan;
- repository discovery;
- validação;
- decisão arquitetural;
- Project State Entry.

---

## Relação issue → execução

Fluxo recomendado:

```text
Issue/board item
↓
Implementation Packet ou intake
↓
Repository discovery
↓
Execution Plan
↓
Implementação
↓
Completion Packet
↓
Review
↓
Sugestão de atualização do board
```

---

## Relação issue → PROJECT_STATE

Uma issue só deve gerar `PROJECT_STATE.md` quando alterar verdade técnica durável.

Exemplo:

```text
Issue: Implementar autenticação
PROJECT_STATE: Auth usa JWT com refresh token; rotação pendente; endpoints privados exigem policy X.
```

Não copiar issue inteira para state.

---

## MCP read-only

Se MCP estiver configurado, agentes podem usar para leitura conforme policy.

### Integrações permitidas

| Integração | Modo | Observação |
|-----------|------|------------|
| GitHub Projects | read-only | `<observação>` |
| GitHub Issues/PRs | read-only | `<observação>` |

### Integrações proibidas/restritas

| Operação | Status | Motivo |
|---------|--------|--------|
| Mover item | `<proibido | exige autorização>` | `<motivo>` |
| Fechar issue | `<proibido | exige autorização>` | `<motivo>` |
| Comentar | `<proibido | exige autorização>` | `<motivo>` |

---

## Sugestão de atualização de board

Ao final da task, o agente pode sugerir:

```md
## Sugestão de atualização do board

Item:
Status sugerido:
Motivo:
PR/commit:
Lacunas:
```

Humano decide se aplica.

---

## Sinais de conflito

Escalar quando:

- board diz Done, mas código não confirma;
- issue pede algo contrário à arquitetura;
- board e `PROJECT_STATE.md` divergem;
- prioridade é ambígua;
- issue está vaga demais para implementar;
- comentários contêm decisão técnica não registrada;
- card exige ação R3/R4.

---

## Última atualização

```text
Data:
Autor:
Motivo:
```