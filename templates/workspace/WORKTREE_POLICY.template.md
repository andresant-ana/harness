# Worktree Policy

## Finalidade

Este documento define a política local de branch, worktree e isolamento de tasks neste workspace.

Seu papel é impedir mistura de escopos, perda de trabalho, conflitos desnecessários e mutações fora do envelope da task.

---

## Regra central

Uma task relevante deve ter escopo isolado e diff revisável.

Não misturar:

- feature com refactor amplo;
- bugfix com reorganização estrutural;
- documentação com mudança funcional não relacionada;
- alteração de infra com alteração de produto;
- múltiplas issues sem justificativa.

---

## Modelo de trabalho

```text
Branch principal:
Branch de trabalho:
Uso de worktree:
PR obrigatório:
Push direto permitido:
```

---

## Quando criar branch dedicada

Criar branch dedicada quando:

- task for R1+;
- houver múltiplos arquivos;
- houver risco de conflito;
- houver alteração funcional;
- houver mudança de schema;
- houver mudança em CI/CD/IaC;
- houver review humano;
- houver PR.

Padrão sugerido:

```text
feature/<descricao-curta>
fix/<descricao-curta>
chore/<descricao-curta>
docs/<descricao-curta>
```

---

## Quando usar git worktree

Usar worktree quando:

- houver tasks paralelas;
- houver investigação que não deve poluir branch atual;
- houver risco de conflito;
- for necessário comparar branches;
- uma task estiver bloqueada e outra precisar avançar.

Não usar worktree para esconder falta de organização.

---

## Estrutura sugerida para worktrees

```text
~/engineering/<project>/
~/engineering/<project>-worktrees/<branch-name>/
```

Adaptar para realidade local:

```text
<estrutura local>
```

---

## Antes de iniciar task

Rodar:

```bash
git status
git branch --show-current
git log --oneline -5
```

Verificar:

- branch correta;
- working tree limpa ou mudanças conhecidas;
- remoto atualizado;
- task/issue associada;
- escopo claro.

---

## Durante a task

Regras:

- manter diff pequeno;
- checar `git diff` periodicamente;
- não editar arquivos fora do escopo sem registrar motivo;
- não fazer rebase/reset destrutivo sem autorização;
- não misturar tasks;
- se o risco subir, pausar e escalar.

---

## Antes de commit

Rodar:

```bash
git status
git diff --stat
git diff --check
```

Quando necessário:

```bash
git diff
```

Verificar:

- sem segredo;
- sem arquivo acidental;
- sem line ending massivo;
- sem mudança lateral;
- validação executada;
- Completion Packet preparado.

---

## Política de commits

Commits devem ser:

- causais;
- pequenos;
- revisáveis;
- ligados ao escopo;
- com mensagem clara.

Exemplos bons:

```text
adiciona templates de workspace do harness
corrige validação de endpoint de login
documenta comandos locais de build e test
```

Exemplos ruins:

```text
update
fix
ajustes
mudanças
wip
```

---

## Push e PR

Antes de push:

```bash
git status
git log --oneline -5
```

PR deve conter:

- objetivo;
- escopo;
- validações;
- riscos;
- lacunas;
- issue relacionada;
- state update, se aplicável.

---

## Operações sensíveis

Exigem autorização explícita:

```bash
git reset --hard
git clean -fd
git push --force
git rebase
git filter-repo
git cherry-pick em branch compartilhada
exclusão de branch remota
```

---

## Como agir em conflito

Quando houver conflito:

1. não resolver no chute;
2. identificar arquivos conflitantes;
3. entender intenção dos dois lados;
4. preservar mudanças fora do escopo;
5. rodar validações;
6. registrar risco se a resolução for não trivial.

---

## Relação com board/issues

Branch pode referenciar issue, mas issue não substitui plano.

```text
Issue:
Branch:
PR:
Board item:
```

---

## Exceções permitidas

Exceções devem ser explícitas:

| Exceção | Motivo | Autorização |
|--------|--------|-------------|
| `<exceção>` | `<motivo>` | `<quem autorizou>` |

---

## Última atualização

```text
Data:
Autor:
Motivo:
```