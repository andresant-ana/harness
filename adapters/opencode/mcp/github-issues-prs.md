# OpenCode MCP — GitHub Issues and PRs Read-Only

## Finalidade

Este arquivo orienta o uso de MCP para leitura de GitHub Issues, Pull Requests, commits remotos, comentários, diffs e checks no OpenCode.

Issues e PRs ajudam a entender contexto de trabalho, critérios de aceite, discussão e estado remoto.

Eles não substituem discovery local, validação local ou review técnico.

---

## Modo permitido

```text
read-only
```

Operações permitidas:

```text
buscar issue
ler issue
ler comentários
ler labels
ler milestone
ler PR
ler diff
ler commits
ler checks/status
ler arquivos remotos
resumir contexto
```

Operações proibidas sem autorização explícita:

```text
criar issue
editar issue
fechar issue
comentar
aplicar label
remover label
criar PR
editar PR
aprovar PR
request changes
mergear PR
fechar PR
disparar workflow
alterar branch
```

---

## Agente responsável

```text
adapters/opencode/agents/mcp-observer.md
```

Skills relacionadas:

```text
skills/integration/github-readonly-ops/SKILL.md
skills/integration/mcp-readonly-operator/SKILL.md
skills/platform/git-github-workflow/SKILL.md
```

---

## Quando usar

Use quando for necessário consultar:

- issue relacionada à task;
- critérios de aceite;
- comentários de discussão;
- histórico de decisão;
- PR vinculado;
- diff remoto;
- status de checks;
- branch remota;
- commit específico;
- divergência local/remoto.

---

## Quando não usar

Não use quando:

- a informação já está no workspace;
- a consulta não muda decisão;
- o objetivo é agir no GitHub;
- a issue é irrelevante para a task;
- o remoto seria usado para sobrescrever verdade local sem checagem.

---

## Pergunta obrigatória antes da consulta

Antes de usar MCP, declarar:

```text
Que issue/PR/commit precisamos consultar?
Que pergunta essa consulta deve responder?
A resposta afetará plan, implementation, review ou handoff?
```

---

## Separação local vs remoto

O OpenCode deve diferenciar:

```text
workspace local
branch atual
branch remota
default branch
PR branch
commit específico
issue
comentário
check de CI
```

Nunca assumir que `main` remoto é igual ao estado local.

---

## Issues

Issues podem conter:

- objetivo;
- motivação;
- critérios de aceite;
- discussão;
- links;
- decisões preliminares;
- prioridade;
- contexto de produto.

Issues não provam:

- arquitetura final;
- implementação correta;
- validação executada;
- estado técnico atual;
- ausência de regressão.

---

## Pull Requests

PRs podem informar:

- diff remoto;
- comentários de review;
- commits;
- checks;
- arquivos alterados;
- discussão técnica.

PR verde não prova:

- arquitetura correta;
- segurança suficiente;
- ausência de over-engineering;
- prontidão operacional;
- ausência de lacunas.

---

## Checks/CI

Ao ler checks, registrar:

```text
workflow
commit
status
conclusão
falha
limitação
```

Não usar CI verde como substituto de review.

Não usar CI vermelho como diagnóstico completo sem investigar logs ou contexto.

---

## Processo

### 1. Identificar referência

Registrar:

```text
repo
issue
PR
branch
commit
check
```

### 2. Ler com escopo

Preferir leitura específica:

- issue exata;
- PR exato;
- comentário relevante;
- commit específico;
- check específico.

Evitar varredura ampla.

### 3. Separar pedido de fato técnico

Classificar conteúdo como:

```text
pedido
critério de aceite
comentário
hipótese
decisão
fato técnico confirmado
lacuna
```

### 4. Cruzar com workspace

Quando houver implicação técnica, validar contra:

```text
código local
PROJECT_STATE.md
ADRs
LOCAL_COMMANDS.md
diff local
testes
```

### 5. Registrar limitações

Se o remoto não estiver sincronizado com local, declarar.

---

## Output recomendado

```md
# GitHub Issues/PRs Read-Only Note

## Pergunta
<o que precisava ser verificado>

## Referência
<repo, issue, PR, branch, commit ou check>

## Fontes consultadas
- <issue/PR/comment/check/commit>

## Achados
- <achado 1>
- <achado 2>

## Local vs remoto
<alinhado | divergente | incerto>

## Checks/CI
<status, commit e limitação, se aplicável>

## Implicação para a task
<como afeta plan, implementation, review ou handoff>

## Limitações
- <limitação 1>
- <limitação 2>

## Veredito
<suficiente | checar workspace | investigar mais | escalar>
```

---

## Escalonamento

Escalar quando:

- issue e código divergirem;
- PR tocar R3/R4;
- CI falhar sem causa clara;
- comentário de review indicar risco sério;
- issue pedir algo contrário à arquitetura;
- próximo passo exigir comentário, merge, label ou fechamento;
- remoto e local divergirem em decisão relevante.

---

## Anti-patterns

Evitar:

- implementar só pelo título da issue;
- aceitar comentário antigo como decisão atual;
- tratar PR verde como prova final;
- ignorar comentários de review;
- ler branch errada;
- comparar local com remoto sem confirmar ref;
- comentar em issue automaticamente;
- fechar issue automaticamente.

---

## Declaração operacional curta

Issues e PRs informam contexto remoto.  
O OpenCode deve ler com ref correta, escopo claro e validação contra o workspace.