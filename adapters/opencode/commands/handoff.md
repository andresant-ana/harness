# OpenCode Command — handoff

## Finalidade

Este comando orienta o OpenCode a preparar o fechamento factual de uma task, investigação, review ou execução.

O comando `handoff` organiza continuidade.  
Ele não substitui validação nem review técnico.

---

## Agente responsável

```text
adapters/opencode/agents/delivery-prep.md
```

Contrato canônico:

```text
agents/delivery-prep.md
```

---

## Quando usar

Use este comando quando:

- uma implementação terminou;
- uma investigação terminou;
- uma review foi feita;
- houver necessidade de Completion Packet final;
- houver lacunas a registrar;
- houver sugestão de commit ou PR;
- houver possível atualização de `PROJECT_STATE.md`;
- outra sessão/agente/humano precisará continuar.

---

## Quando não usar

Não use este comando para:

- validar tecnicamente sozinho;
- esconder lacunas;
- transformar falha em sucesso;
- atualizar board sem autorização;
- substituir Review Report em task sensível.

---

## Inputs esperados

```text
Objetivo original:
Execution Plan:
Completion Packet:
Review Report:
Diff:
Validações:
Riscos:
Lacunas:
Próximo passo esperado:
```

---

## Fontes que devem ser consultadas

```text
DONE_CRITERIA.md
PROJECT_STATE.md
WORKTREE_POLICY.md
GITHUB_PROJECTS_CONTEXT.md
LOCAL_COMMANDS.md
```

Fontes globais:

```text
core/protocols/08-handoff-protocol.md
core/protocols/11-project-state-maintenance.md
core/policies/10-project-state-vs-board-policy.md
templates/packets/Completion_Packet.template.md
templates/workspace/PROJECT_STATE.template.md
```

---

## Skills prováveis

```text
skills/orchestration/delivery-wrapup/SKILL.md
skills/hygiene/project-state-maintainer/SKILL.md
skills/hygiene/doc-gardener/SKILL.md
skills/platform/git-github-workflow/SKILL.md
skills/orchestration/testing-verifier/SKILL.md
skills/hygiene/consistency-scanner/SKILL.md
```

---

## Processo

### 1. Reconstituir objetivo

Registrar o objetivo original e a classe de risco.

### 2. Consolidar mudanças

Listar apenas mudanças factuais.

Evitar:

```text
ajustes gerais
melhorias diversas
refatorações necessárias
```

### 3. Consolidar validações

Separar:

```text
validações executadas
validações não executadas
motivo das lacunas
risco residual
```

### 4. Avaliar PROJECT_STATE

Propor atualização se houve:

- decisão durável;
- risco novo;
- limitação;
- dívida consciente;
- mudança arquitetural;
- mudança operacional;
- integração nova;
- comando relevante;
- follow-up estrutural.

### 5. Sugerir commit/PR

Mensagem deve ser causal e pequena.

### 6. Indicar próximo passo

Exemplos:

```text
review
commit
push
PR
nova task
atualizar PROJECT_STATE
escalar
```

---

## Output esperado

Produzir `Delivery Prep` contendo:

```text
Status da task
Objetivo
Mudanças realizadas
Validações executadas
Validações não executadas
Lacunas e riscos remanescentes
Divergências do plano
Project State
Sugestão de commit
Handoff
Próximo passo
```

---

## Prompt operacional sugerido

```text
Use o comando handoff.

Prepare o fechamento factual da task abaixo.

Contexto:
<colar Execution Plan, Completion Packet, Review Report, diff ou validações>

Regras:
- Não esconda lacunas.
- Não transforme handoff em propaganda.
- Separe validações executadas e não executadas.
- Avalie necessidade de PROJECT_STATE.
- Sugira mensagem de commit causal.
- Indique próximo passo acionável.
```

---

## Sugestão de commit

Bons exemplos:

```text
adiciona commands operacionais do adapter OpenCode
documenta MCP read-only do OpenCode
define permissões dos agentes do adapter
```

Evitar:

```text
update
fix
ajustes
mudanças
wip
```

---

## Critério de sucesso

O comando foi bem-sucedido quando o próximo humano/agente consegue continuar sem reconstruir contexto a partir do zero.

---

## Anti-patterns

Evitar:

- handoff triunfalista;
- esconder teste não rodado;
- registrar tudo em `PROJECT_STATE.md`;
- copiar issue inteira;
- commit genérico;
- próximo passo vago;
- fechar task bloqueada como concluída.