# OpenCode Permissions

## Finalidade

Este diretório documenta o modelo de permissões do adapter OpenCode.

Permissões existem para impedir que um agente com bom contexto execute uma ação fora do seu papel, fora do escopo, fora da classe de risco ou fora da autorização humana.

---

## Regra central

Permissão segue papel, risco e superfície.

Nenhum agente deve receber autoridade apenas porque tecnicamente consegue executar uma ação.

---

## Fonte canônica

Políticas principais:

```text
core/policies/00-command-safety-policy.md
core/policies/01-file-mutation-policy.md
core/policies/02-git-policy.md
core/policies/03-mcp-policy.md
core/policies/05-secret-and-prod-policy.md
core/policies/07-trusted-integrations-policy.md
core/policies/10-project-state-vs-board-policy.md
```

Contratos de agentes:

```text
agents/
adapters/opencode/agents/
```

MCP:

```text
adapters/opencode/mcp/
```

---

## Arquivos deste diretório

```text
adapters/opencode/permissions/
├─ README.md
├─ agent-permissions-matrix.md
└─ project-board-permissions.md
```

### `agent-permissions-matrix.md`

Define permissões por agente:

- leitura;
- escrita local;
- comandos;
- git;
- MCP;
- produção;
- segredos;
- escalonamento.

### `project-board-permissions.md`

Define permissões específicas para GitHub Projects e board:

- leitura permitida;
- escrita proibida por padrão;
- sugestões permitidas;
- ações que exigem autorização.

---

## Princípios

### Menor privilégio

Cada agente recebe apenas o necessário para cumprir seu papel.

### Read-only first

Toda integração externa começa em leitura.

### Local antes de externo

O workspace local é priorizado antes de MCP, cloud, board ou observabilidade externa.

### Escalonamento antes de risco

Quando uma ação ultrapassa o envelope, o agente deve pausar.

### Evidência acima de confiança

Permissão não substitui validação.

---

## Classes de risco

```text
R0 — leitura/investigação sem mutação
R1 — mudança local pequena e reversível
R2 — mudança funcional relevante
R3 — mudança estrutural, sensível ou sistêmica
R4 — produção, segredo, irreversibilidade ou alto risco
```

Regra:

```text
R0/R1 → autonomia limitada
R2 → autonomia com plano e evidência
R3 → review/escalonamento
R4 → autorização explícita obrigatória
```

---

## Superfícies de permissão

As permissões devem ser analisadas por superfície:

```text
workspace files
shell commands
git local
git remote
MCP read
MCP write
GitHub Projects
issues/PRs
cloud
observability
secrets
production
CI/CD
dependencies
database
IaC
```

---

## Permissões padrão por papel

Resumo:

```text
planner
→ leitura local, discovery, plano, sem mutação.

researcher
→ leitura local/externa, investigação, sem mutação.

implementer
→ mutação local controlada dentro do plano, validação local.

reviewer
→ leitura e análise, sem mutação.

architect-critic
→ leitura e crítica, sem mutação.

delivery-prep
→ leitura, handoff, sugestão de commit/state; mutação documental só se explicitamente autorizada.

mcp-observer
→ leitura externa read-only, sem mutação.
```

Detalhes em:

```text
agent-permissions-matrix.md
```

---

## Operações proibidas por padrão

Sem autorização explícita, nenhum agente deve:

- tocar produção;
- expor segredo;
- alterar cloud config;
- executar deploy;
- disparar workflow;
- aplicar migration em ambiente real;
- deletar recurso;
- mover card;
- fechar issue;
- comentar em PR;
- fazer merge;
- forçar push;
- executar comando destrutivo;
- instalar dependência estrutural sem justificativa;
- alterar IAM/RBAC;
- alterar firewall/rede.

---

## Autorização explícita

Autorização explícita deve conter:

```text
quem autorizou
qual ação
qual ambiente
qual escopo
qual risco aceito
qual rollback/mitigação
qual evidência esperada
```

Autorização genérica como “pode fazer tudo” não deve ser aceita para R3/R4.

---

## Escrita local

Escrita local pode ocorrer quando:

- existe Execution Plan suficiente;
- task é R1/R2 ou R3 autorizado;
- escopo está claro;
- arquivo pertence à task;
- diff é revisável;
- validação está definida.

Escrita local deve parar quando:

- escopo expandir;
- risco subir;
- segredo aparecer;
- produção entrar;
- dependência nova for necessária;
- arquitetura mudar.

---

## Escrita externa

Escrita externa é proibida por padrão.

Exemplos:

- mover board item;
- comentar issue/PR;
- fechar issue;
- criar release;
- disparar pipeline;
- alterar cloud;
- alterar observabilidade;
- modificar config remota.

Toda escrita externa exige autorização explícita e política específica.

---

## Segredos

Nenhum agente deve reproduzir valores reais de:

```text
tokens
keys
passwords
connection strings
certificates
cookies
headers Authorization
secrets de CI/CD
app settings sensíveis
```

Permitido registrar apenas:

```text
secret presente
secret ausente
valor mascarado
risco identificado
```

---

## Produção

Produção é R4 por padrão.

Ações em produção exigem:

- autorização explícita;
- plano;
- mitigação/rollback;
- evidência;
- supervisão humana;
- registro.

Leitura de produção também deve ser restrita quando envolver dados sensíveis.

---

## Git

Permitido com cautela:

```text
git status
git diff
git diff --stat
git diff --check
git log
git branch --show-current
```

Sensível:

```text
git reset --hard
git clean -fd
git push --force
git rebase
git filter-repo
merge em branch compartilhada
exclusão de branch
```

Operações sensíveis exigem autorização.

---

## Comandos

Comandos devem seguir `LOCAL_COMMANDS.md` quando existir.

Antes de comando relevante:

```bash
pwd
git status
```

Depois de mutação:

```bash
git status
git diff --stat
git diff --check
```

---

## Registro de exceções

Qualquer exceção de permissão deve ser registrada no artifact apropriado:

- Execution Plan;
- Escalation Note;
- Completion Packet;
- Review Report;
- Project State Entry, se for durável.

---

## Anti-patterns

Evitar:

- dar permissão ampla “para agilizar”;
- confundir acesso com autorização;
- permitir write externo por padrão;
- deixar implementer decidir arquitetura;
- permitir mcp-observer agir;
- permitir reviewer corrigir diretamente;
- permitir plugin operar sem matriz;
- tratar produção como ambiente comum.

---

## Declaração operacional curta

Permissão é parte da arquitetura do harness.  
O agente só pode fazer o que seu papel, risco e autorização permitem.