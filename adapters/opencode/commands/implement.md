# OpenCode Command — implement

## Finalidade

Este comando orienta o OpenCode a executar uma mudança local dentro de um Execution Plan.

O comando `implement` não decide a estratégia.  
Ele executa o plano com escopo, validação e evidência.

---

## Agente responsável

```text
adapters/opencode/agents/implementer.md
```

Contrato canônico:

```text
agents/implementer.md
```

---

## Quando usar

Use este comando quando:

- já existir Execution Plan suficiente;
- a task tiver escopo claro;
- a classe de risco permitir execução;
- a mutação for local;
- os sinais de escalonamento estiverem definidos;
- os comandos de validação forem conhecidos ou dedutíveis de authority sources.

---

## Quando não usar

Não use este comando quando:

- não houver plano;
- a task for R0;
- houver ambiguidade estratégica;
- houver risco R3/R4 sem aprovação;
- houver produção, segredo ou dado real;
- o plano estiver desatualizado;
- a implementação exigir decisão arquitetural nova.

---

## Inputs esperados

```text
Execution Plan:
Task/Issue:
Escopo:
Fora do escopo:
Classe de risco:
Validações planejadas:
Sinais de escalonamento:
```

---

## Fontes que devem ser consultadas

Antes de editar:

```text
Execution Plan
WORKSPACE_GUIDE.md
AUTHORITY_SOURCES.md
LOCAL_COMMANDS.md
PROJECT_STATE.md
DONE_CRITERIA.md
RISK_SURFACES.md
OPERATIONAL_REALITY.md
```

Arquivos globais relevantes:

```text
core/policies/00-command-safety-policy.md
core/policies/01-file-mutation-policy.md
core/policies/02-git-policy.md
core/protocols/06-evidence-standard.md
templates/packets/Completion_Packet.template.md
```

---

## Skills prováveis

Acionar conforme a task:

```text
skills/orchestration/testing-verifier/SKILL.md
skills/engineering/refactoring-safety/SKILL.md
skills/security/secure-coding-baseline/SKILL.md
skills/engineering/architecture-by-pain-check/SKILL.md
skills/platform/bash-linux-ops/SKILL.md
skills/platform/git-github-workflow/SKILL.md
skills/hygiene/consistency-scanner/SKILL.md
```

Stack específica quando aplicável:

```text
skills/stack/dotnet/
skills/stack/react/
skills/stack/postgres/
skills/stack/azure/
```

---

## Processo

### 1. Confirmar envelope

Antes de editar, confirmar:

- objetivo;
- escopo;
- fora de escopo;
- classe de risco;
- arquivos/áreas;
- validação;
- sinais de escalonamento.

### 2. Confirmar estado local

Rodar ou solicitar:

```bash
pwd
git status
git diff --stat
```

### 3. Executar mudança pequena

Aplicar apenas mudanças causais.

Evitar:

- refactor lateral;
- reescrita ampla;
- dependência nova;
- arquitetura nova;
- mudança cosmética sem relação.

### 4. Validar

Usar `LOCAL_COMMANDS.md`.

Se não for possível validar, declarar lacuna.

### 5. Produzir Completion Packet

Registrar:

- o que mudou;
- onde mudou;
- validações executadas;
- validações não executadas;
- riscos remanescentes;
- divergências do plano;
- necessidade de `PROJECT_STATE.md`.

---

## Output obrigatório

Produzir:

```text
diff local
validações executadas
Completion Packet
```

Usar:

```text
templates/packets/Completion_Packet.template.md
```

---

## Prompt operacional sugerido

```text
Use o comando implement.

Execute o Execution Plan abaixo com escopo restrito.

Execution Plan:
<colar plano>

Regras:
- Não redesenhe a solução.
- Não expanda escopo.
- Não crie dependência sem justificativa e policy.
- Não toque produção.
- Não exponha segredo.
- Pare se o risco subir.
- Valide com comandos locais.
- Produza Completion Packet.
```

---

## Escalonamento obrigatório

Pausar e escalar se:

- o plano não bater com a realidade;
- a classe de risco subir;
- surgir decisão arquitetural;
- for necessária dependência nova;
- validação essencial falhar;
- houver risco de dados, segurança ou produção;
- a mudança exigir escrita externa;
- o diff começar a misturar escopos.

---

## Critério de sucesso

O comando foi bem-sucedido quando:

- o plano foi executado dentro do escopo;
- o diff é revisável;
- validações foram executadas ou lacunas declaradas;
- riscos remanescentes estão explícitos;
- Completion Packet foi produzido.

---

## Anti-patterns

Evitar:

- “já que estou aqui”;
- alterar antes de entender;
- corrigir bug com arquitetura nova;
- instalar package por conveniência;
- mascarar teste quebrado;
- declarar sucesso sem evidência;
- esconder divergência do plano.