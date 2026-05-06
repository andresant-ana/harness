# Agent Permissions Matrix — OpenCode

## Finalidade

Esta matriz define as permissões operacionais dos agentes do OpenCode adapter.

Ela traduz os contratos canônicos de agentes para limites práticos de leitura, escrita, comandos, git, MCP, produção e segredos.

---

## Regra central

Agente não recebe permissão por capacidade técnica.  
Agente recebe permissão por responsabilidade operacional.

---

## Legenda

```text
ALLOW      → permitido no fluxo padrão
LIMITED    → permitido com escopo, plano ou condição
ESCALATE   → exige escalonamento antes de agir
FORBIDDEN  → proibido no fluxo padrão
```

---

## Matriz resumida

| Agente | Leitura local | Escrita local | Comandos locais | Git local | Git remoto | MCP read | MCP write | Produção | Segredos |
|--------|---------------|---------------|-----------------|-----------|------------|----------|-----------|----------|----------|
| planner | ALLOW | FORBIDDEN | LIMITED | LIMITED | FORBIDDEN | LIMITED | FORBIDDEN | FORBIDDEN | FORBIDDEN |
| researcher | ALLOW | FORBIDDEN | LIMITED | LIMITED | FORBIDDEN | LIMITED | FORBIDDEN | FORBIDDEN | FORBIDDEN |
| implementer | ALLOW | LIMITED | LIMITED | LIMITED | ESCALATE | LIMITED | FORBIDDEN | FORBIDDEN | FORBIDDEN |
| reviewer | ALLOW | FORBIDDEN | LIMITED | LIMITED | FORBIDDEN | LIMITED | FORBIDDEN | FORBIDDEN | FORBIDDEN |
| architect-critic | ALLOW | FORBIDDEN | LIMITED | LIMITED | FORBIDDEN | LIMITED | FORBIDDEN | FORBIDDEN | FORBIDDEN |
| delivery-prep | ALLOW | LIMITED | LIMITED | LIMITED | ESCALATE | LIMITED | FORBIDDEN | FORBIDDEN | FORBIDDEN |
| mcp-observer | LIMITED | FORBIDDEN | FORBIDDEN | FORBIDDEN | FORBIDDEN | ALLOW | FORBIDDEN | FORBIDDEN | FORBIDDEN |

---

## Planner

### Permitido

- ler arquivos locais relevantes;
- ler workspace docs;
- fazer discovery proporcional;
- ler `git status`, `git diff --stat`, `git log`;
- consultar MCP read-only quando necessário;
- produzir Execution Plan;
- sugerir skills e artifacts.

### Limitado

Comandos locais apenas para descoberta segura, por exemplo:

```bash
pwd
git status
find . -maxdepth 3 -type f | sort
```

### Proibido

- editar arquivos;
- implementar;
- criar dependência;
- alterar git remoto;
- mover board;
- tocar produção;
- manipular segredo.

### Escalar quando

- risco R3/R4;
- decisão arquitetural;
- validação essencial ausente;
- conflito entre sources;
- produção/segredo/dado real.

---

## Researcher

### Permitido

- ler código;
- ler docs;
- ler erros/logs locais fornecidos;
- consultar docs oficiais;
- consultar GitHub read-only;
- consultar observabilidade/cloud read-only quando autorizado e necessário;
- produzir Investigation Note.

### Limitado

Comandos locais de investigação devem ser não destrutivos.

### Proibido

- editar arquivos;
- executar correção;
- alterar GitHub;
- alterar cloud;
- comentar em PR/issue;
- tocar segredo;
- tocar produção.

### Escalar quando

- investigação revelar risco R3/R4;
- fonte externa contradizer código;
- evidência insuficiente para impacto alto;
- próxima ação exigir escrita.

---

## Implementer

### Permitido

- ler workspace docs;
- editar arquivos locais dentro do Execution Plan;
- rodar validações locais;
- produzir Completion Packet;
- sugerir commit.

### Limitado

Escrita local exige:

- Execution Plan suficiente;
- escopo claro;
- classe de risco compatível;
- arquivos dentro da task;
- validação planejada.

Comandos permitidos devem vir de `LOCAL_COMMANDS.md` ou ser seguros e explícitos.

Git local permitido:

```bash
git status
git diff
git diff --stat
git diff --check
git log
```

### Proibido

- expandir escopo;
- decidir arquitetura estrutural sozinho;
- instalar dependência sem policy;
- executar comando destrutivo;
- alterar git remoto sem autorização;
- fazer MCP write;
- tocar produção;
- manipular segredo real.

### Escalar quando

- plano ficar inválido;
- risco subir;
- dependência nova for necessária;
- validação essencial falhar;
- mudança exigir ação externa;
- dados/segurança/produção entrarem no escopo.

---

## Reviewer

### Permitido

- ler plano;
- ler diff;
- ler Completion Packet;
- ler artifacts;
- ler validações;
- consultar MCP read-only quando necessário para evidência;
- produzir Review Report.

### Limitado

Comandos permitidos devem ser de inspeção ou validação não destrutiva.

### Proibido

- corrigir diretamente;
- editar arquivos;
- aprovar sem evidência;
- alterar board;
- comentar PR;
- mergear PR;
- tocar produção;
- manipular segredo.

### Escalar quando

- risco residual alto;
- decisão estratégica pendente;
- R3/R4;
- conflito entre sources;
- review exigir Core Architect.

---

## Architect Critic

### Permitido

- ler plano;
- ler diff;
- ler ADRs;
- ler `PROJECT_STATE.md`;
- ler arquitetura local;
- consultar contexto read-only;
- produzir crítica arquitetural;
- recomendar ADR ou Project State Entry;
- recomendar simplificação.

### Limitado

Pode sugerir mudanças, mas não aplicá-las.

### Proibido

- implementar;
- reescrever arquitetura diretamente;
- impor preferência estética;
- criar dependência;
- tocar produção;
- manipular segredo.

### Escalar quando

- decisão alterar boundary;
- houver trade-off forte;
- solução exigir ADR;
- risco R3/R4;
- houver dados/segurança/produção.

---

## Delivery Prep

### Permitido

- ler artifacts;
- ler diff;
- ler validações;
- preparar handoff;
- sugerir commit;
- sugerir PR description;
- sugerir Project State Entry;
- preparar Completion Packet final.

### Limitado

Escrita local documental só deve ocorrer se explicitamente solicitada ou prevista no fluxo.

Exemplos condicionais:

```text
atualizar PROJECT_STATE.md
atualizar changelog local
ajustar doc de handoff
```

### Proibido

- declarar sucesso sem validação;
- esconder lacunas;
- mover board automaticamente;
- fechar issue;
- fazer commit/push sem autorização;
- tocar produção;
- manipular segredo.

### Escalar quando

- task não pode ser fechada honestamente;
- state update envolve decisão estratégica;
- risco residual alto;
- commit misturaria escopos;
- há possível segredo no diff.

---

## MCP Observer

### Permitido

- consultar MCP read-only;
- ler GitHub Projects;
- ler issues/PRs;
- ler cloud metadata;
- ler observabilidade filtrada;
- resumir achados;
- produzir MCP Read-Only Note ou Investigation Note.

### Limitado

Deve ter pergunta externa clara antes de consultar.

### Proibido

- editar externo;
- mover card;
- comentar issue/PR;
- fechar issue;
- aplicar label;
- disparar workflow;
- alterar cloud;
- reiniciar recurso;
- fazer deploy;
- ler segredo;
- executar comandos locais.

### Escalar quando

- próxima ação exigir escrita;
- integração não for confiável;
- produção aparecer;
- segredo ou dado sensível aparecer;
- fonte externa contradizer workspace;
- observabilidade indicar incidente ativo.

---

## Comandos por categoria

### Permitidos por padrão para leitura

```bash
pwd
git status
git diff --stat
git diff --check
git log --oneline -5
find . -maxdepth 3 -type f | sort
```

Ainda assim, respeitar contexto e tamanho do repo.

### Permitidos com plano/escopo

```bash
dotnet build
dotnet test
npm test
npm run lint
docker compose up
docker compose logs
```

Apenas quando forem authority commands ou adequados ao workspace.

### Sensíveis

```bash
git reset --hard
git clean -fd
git push --force
docker volume rm
terraform apply
terraform destroy
az deployment ...
dotnet ef database update <ambiente real>
curl | bash
rm -rf
```

Exigem autorização ou são proibidos no fluxo padrão.

---

## MCP por categoria

### Read permitido

```text
GitHub Projects read
GitHub Issues/PRs read
docs read
cloud metadata read
observability read
```

### Write proibido por padrão

```text
board move
issue close
PR comment
workflow dispatch
cloud update
deploy
config change
secret update
```

---

## Produção

Produção é sempre R4.

Nenhum agente tem autonomia padrão para:

- alterar produção;
- aplicar migration em produção;
- fazer deploy em produção;
- reiniciar produção;
- alterar config de produção;
- alterar segredo de produção;
- ler dado sensível de produção sem autorização.

---

## Segredos

Nenhum agente pode reproduzir valor real de segredo.

Se segredo for encontrado:

1. não copiar;
2. mascarar;
3. pausar se estiver no diff;
4. escalar;
5. registrar risco sem expor valor.

---

## Exceções

Exceções devem ser documentadas em Escalation Note ou Execution Plan.

Formato mínimo:

```text
Ação:
Agente:
Autorizador:
Ambiente:
Escopo:
Risco:
Mitigação:
Evidência esperada:
```

---

## Declaração operacional curta

A matriz de permissões existe para impedir que papel vire poder ilimitado.  
No harness, autonomia é concedida por escopo, risco e evidência.