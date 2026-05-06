# OpenCode MCP — GitHub Projects Read-Only

## Finalidade

Este arquivo orienta o uso de MCP para leitura de GitHub Projects no OpenCode.

GitHub Projects deve ser usado para entender coordenação de trabalho: status, prioridade, sequencing, issue vinculada e dependências.

Ele não substitui `PROJECT_STATE.md`, código, ADRs ou discovery local.

---

## Modo permitido

```text
read-only
```

Operações permitidas:

```text
listar projects
listar items
ler item
ler status
ler prioridade
ler campos
ler labels
ler issue vinculada
ler links para PRs
resumir contexto
```

Operações proibidas sem autorização explícita:

```text
mover item
alterar status
alterar prioridade
editar campo
criar item
deletar item
fechar issue
aplicar label
comentar
arquivar item
```

---

## Agente responsável

```text
adapters/opencode/agents/mcp-observer.md
```

Skills relacionadas:

```text
skills/integration/github-projects-readonly/SKILL.md
skills/integration/mcp-readonly-operator/SKILL.md
skills/hygiene/project-state-maintainer/SKILL.md
```

---

## Quando usar

Use quando a task precisar entender:

- qual item do board está relacionado;
- status atual;
- prioridade;
- milestone;
- issue vinculada;
- dependências;
- ordem sugerida;
- se algo está bloqueado;
- se há comentário relevante de escopo.

---

## Quando não usar

Não use quando:

- a task já estiver clara localmente;
- o board não for fonte relevante;
- o uso seria apenas curiosidade;
- a consulta substituiria discovery no workspace;
- o objetivo for atualizar status do card;
- a próxima ação exigiria escrita.

---

## Pergunta obrigatória antes da consulta

Antes de usar MCP, declarar:

```text
Que informação do board precisamos obter?
Por que ela importa?
Que decisão depende dela?
Qual item/project será consultado?
```

Sem pergunta clara, não consultar.

---

## Interpretação correta

GitHub Projects pode informar:

```text
planejamento
prioridade
status de coordenação
sequência de trabalho
issue vinculada
dependência organizacional
```

GitHub Projects não prova:

```text
estado real do código
qualidade da implementação
decisão arquitetural
validação técnica
prontidão de release
estado operacional real
```

---

## Relação com PROJECT_STATE

Board responde:

```text
O que estamos fazendo?
```

`PROJECT_STATE.md` responde:

```text
Em que estado técnico o sistema está?
```

Se o board disser `Done`, mas o código ou `PROJECT_STATE.md` não confirmarem, registrar divergência e escalar se isso afetar a task.

---

## Processo

### 1. Identificar item

Registrar:

```text
project
board
item
issue vinculada
status
prioridade
```

### 2. Ler contexto mínimo

Consultar apenas:

- título;
- descrição;
- status;
- prioridade;
- labels;
- issue vinculada;
- comentários relevantes;
- PRs vinculados.

### 3. Separar coordenação de técnica

Classificar achados como:

```text
coordenação
intenção
prioridade
escopo planejado
fato técnico confirmado
lacuna
```

### 4. Validar contra workspace

Quando o board indicar algo técnico, validar contra:

```text
código
PROJECT_STATE.md
ADRs
docs locais
commits/PRs
```

### 5. Sugerir, não escrever

O agente pode sugerir:

```text
mover para Review
adicionar link para PR
criar follow-up
marcar bloqueio
```

Mas não deve executar sem autorização.

---

## Output recomendado

```md
# GitHub Projects Read-Only Note

## Pergunta
<o que precisava ser entendido no board>

## Project/item
<project, item, issue vinculada>

## Estado no board
<status, prioridade, milestone, labels>

## Achados
- <achado 1>
- <achado 2>

## Separação board vs verdade técnica
<o que é coordenação e o que é fato técnico confirmado>

## Divergências
<nenhuma | descrita | incerta>

## Sugestão de atualização
<nenhuma | sugestão para humano>

## Implicação para a task
<como isso afeta plan, implement, review ou handoff>

## Veredito
<suficiente | checar workspace | investigar mais | escalar>
```

---

## Escalonamento

Escalar quando:

- board e `PROJECT_STATE.md` divergirem;
- issue vinculada estiver vaga;
- status indicar bloqueio;
- card exigir risco R3/R4;
- próximo passo exigir atualização do board;
- comentário de board contiver decisão técnica não registrada;
- prioridade depender de decisão humana.

---

## Anti-patterns

Evitar:

- implementar apenas pelo título do card;
- tratar `Done` como validação técnica;
- mover card automaticamente;
- fechar issue automaticamente;
- copiar board para `PROJECT_STATE.md`;
- usar board como arquitetura;
- ignorar issue vinculada;
- ignorar divergência entre board e código.

---

## Declaração operacional curta

GitHub Projects é coordenação.  
O OpenCode pode ler o board, mas a verdade técnica continua no workspace.