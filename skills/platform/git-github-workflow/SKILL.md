# Skill — Git GitHub Workflow

## Finalidade

Esta skill orienta o uso disciplinado de Git e GitHub no fluxo do harness.

Seu papel é preservar histórico, isolamento de mudança, rastreabilidade, review e segurança antes de commits, pushes, PRs ou interações com repositório remoto.

---

## Quando usar

Use esta skill quando a task envolver:

- `git status`;
- `git diff`;
- staging;
- commit;
- push;
- branch;
- worktree;
- merge;
- rebase;
- pull;
- PR;
- issue;
- GitHub Projects;
- revisão pré-commit;
- análise de histórico;
- resolução de conflito.

---

## Quando não usar

Não use esta skill quando:

- não houver operação Git/GitHub;
- a task for puramente local e sem versionamento;
- a operação já estiver coberta por policy específica e não houver decisão.

---

## Tese central

Git é a trilha factual da mudança.

Um bom fluxo Git deve deixar claro:

- o que mudou;
- por que mudou;
- em qual escopo;
- com qual validação;
- e qual próximo passo.

---

## Método

### 1. Verificar estado antes de agir

Sempre começar com:

```bash
git status
```

Quando houver mudança:

```bash
git diff --stat
git diff --check
```

---

### 2. Revisar diff antes de staging

Antes de `git add`, verificar se o diff:

- pertence à task;
- não inclui segredo;
- não inclui arquivo acidental;
- não contém ruído de formatação;
- não mistura assuntos;
- não altera line endings desnecessariamente.

---

### 3. Stage por escopo

Preferir:

```bash
git add <path>
```

em vez de:

```bash
git add .
```

quando a task exigir controle fino.

---

### 4. Commit causal

Mensagem de commit deve explicar o efeito real.

Bons exemplos:

```text
adiciona skills de platform do harness
normaliza quebras de linha do repositório
fecha núcleo canônico inicial do harness
```

Exemplos ruins:

```text
update
fix
ajustes
mudanças
```

---

### 5. Push consciente

Antes de push:

```bash
git status
git log --oneline -5
```

Verificar se o branch correto está sendo enviado.

---

### 6. PR quando aplicável

PR deve conter:

- objetivo;
- escopo;
- validações;
- riscos;
- lacunas;
- referência a issue;
- observação de state/doc update se necessário.

---

## Output esperado

```md
# Git/GitHub Workflow Note

## Estado atual
<limpo | mudanças locais | branch divergente | conflito | incerto>

## Escopo do commit/PR
<o que será versionado>

## Arquivos incluídos
- <arquivo/área 1>
- <arquivo/área 2>

## Validações antes do commit
- <validação 1>
- <validação 2>

## Mensagem sugerida
<mensagem de commit>

## Riscos
- <risco 1>
- <risco 2>

## Próximo passo
<commit | push | PR | review | escalar>
```

---

## Checklist de qualidade

Antes de commit/push, verificar:

- `git status` foi visto?
- `git diff --check` foi executado?
- diff pertence ao escopo?
- não há segredo?
- não há arquivo acidental?
- não há mudança massiva de line ending?
- commit message é causal?
- branch está correto?
- validações foram registradas?

---

## Critérios de escalonamento

Escalar quando:

- houver segredo em histórico;
- houver conflito complexo;
- branch estiver divergente de forma não trivial;
- o commit misturar tasks;
- houver risco de sobrescrever trabalho alheio;
- push puder disparar deploy;
- PR envolver mudança R3/R4.

---

## Anti-patterns

Evitar:

- `git add .` sem revisar;
- commit gigante sem escopo;
- mensagem genérica;
- push em branch errada;
- resolver conflito no chute;
- rebase/reset sem entender impacto;
- commit de secrets;
- usar Git para esconder falta de handoff.

---

## Declaração operacional curta

Git registra a história da engenharia.  
Cada commit deve ser pequeno, causal, revisável e seguro.