# OpenCode Command — project-state

## Finalidade

Este comando orienta o OpenCode a avaliar, propor ou preparar atualização do `PROJECT_STATE.md` de um workspace.

O comando `project-state` preserva memória técnica durável.  
Ele não atualiza state por ritual.

---

## Agente responsável

Primário:

```text
adapters/opencode/agents/delivery-prep.md
```

Apoio quando necessário:

```text
adapters/opencode/agents/architect-critic.md
adapters/opencode/agents/reviewer.md
```

Contrato canônico relacionado:

```text
agents/delivery-prep.md
```

---

## Quando usar

Use este comando quando uma task, investigação ou review revelar:

- decisão técnica durável;
- mudança arquitetural;
- alteração de boundary;
- nova integração;
- mudança operacional;
- risco conhecido;
- limitação técnica;
- dívida consciente;
- comando relevante;
- divergência entre documentação e realidade;
- follow-up estrutural.

---

## Quando não usar

Não use este comando quando:

- a mudança for trivial;
- o detalhe pertencer apenas ao diff;
- o Completion Packet já bastar;
- a informação for efêmera;
- a entrada duplicar board/issue;
- a atualização transformaria `PROJECT_STATE.md` em changelog.

---

## Fontes que devem ser consultadas

Workspace:

```text
PROJECT_STATE.md
WORKSPACE_GUIDE.md
PROJECT_CONTEXT.md
AUTHORITY_SOURCES.md
OPERATIONAL_REALITY.md
GITHUB_PROJECTS_CONTEXT.md
```

Artifacts:

```text
Completion Packet
Investigation Note
Review Report
Escalation Note
ADR
issue/PR/commit
```

Globais:

```text
core/protocols/11-project-state-maintenance.md
core/policies/10-project-state-vs-board-policy.md
core/artifacts/06-project-state-entry.schema.md
templates/workspace/PROJECT_STATE.template.md
```

---

## Skills prováveis

```text
skills/hygiene/project-state-maintainer/SKILL.md
skills/hygiene/doc-gardener/SKILL.md
skills/hygiene/consistency-scanner/SKILL.md
skills/engineering/architecture-by-pain-check/SKILL.md
skills/platform/git-github-workflow/SKILL.md
```

---

## Processo

### 1. Identificar mudança durável

Perguntar:

```text
Isso muda como uma futura sessão deve entender o projeto?
Isso evita reinvestigação?
Isso muda arquitetura, operação, risco ou comando?
Isso é decisão durável?
```

Se a resposta for fraca, não atualizar.

### 2. Classificar entrada

Tipos possíveis:

```text
estado técnico
decisão
risco
limitação
dívida técnica
comando
integração
arquitetura
operação
segurança
follow-up
```

### 3. Decidir ação

Escolher:

```text
criar nova entrada
atualizar entrada existente
marcar entrada como resolvida
marcar entrada como substituída
não atualizar
escalar
```

### 4. Preparar entrada

A entrada deve ser curta, densa e referenciada.

Não copiar Completion Packet inteiro.

### 5. Verificar board vs state

Board responde:

```text
O que estamos fazendo?
```

`PROJECT_STATE.md` responde:

```text
Em que estado técnico o sistema está?
```

Não misturar responsabilidades.

---

## Output esperado

Produzir uma proposta de `Project State Entry`:

```text
Tipo:
Status:
Origem:
Área:
Resumo:
Impacto:
Risco:
Próxima revisão:
Referências:
```

Ou declarar:

```text
Não atualizar PROJECT_STATE.md
Motivo:
```

---

## Prompt operacional sugerido

```text
Use o comando project-state.

Avalie se a informação abaixo deve atualizar PROJECT_STATE.md.

Contexto:
<colar Completion Packet, Review Report, Investigation Note, ADR ou decisão>

Regras:
- Não transforme PROJECT_STATE em changelog.
- Registre apenas memória técnica durável.
- Separe board de verdade técnica.
- Proponha entrada curta e referenciada.
- Se depender de decisão estratégica, escale.
```

---

## Critérios para atualizar

Atualizar quando a informação for:

- durável;
- técnica;
- útil para futura sessão;
- referenciada;
- não duplicada;
- relevante para decisão, operação, risco ou arquitetura.

---

## Critérios para não atualizar

Não atualizar quando a informação for:

- efêmera;
- puramente operacional do momento;
- detalhe granular de diff;
- item de backlog;
- status de board;
- duplicação de Completion Packet;
- nota de sessão sem valor futuro.

---

## Escalonamento

Escalar quando:

- a entrada envolve decisão arquitetural;
- há conflito entre `PROJECT_STATE.md` e código;
- board e state divergem;
- a entrada pode registrar dívida técnica relevante;
- o estado atual parece obsoleto;
- há risco de transformar hipótese em fato.

---

## Anti-patterns

Evitar:

- copiar issue inteira;
- copiar Completion Packet inteiro;
- registrar cada commit;
- transformar state em diário;
- duplicar board;
- registrar hipótese como decisão;
- manter entrada obsoleta como ativa;
- esconder risco aceito.