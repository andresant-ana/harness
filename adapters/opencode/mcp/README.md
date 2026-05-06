# OpenCode MCP Adapter

## Finalidade

Este diretório documenta como o OpenCode deve usar MCP dentro do harness.

MCP amplia o alcance do agente para consultar fontes externas, mas não amplia automaticamente sua autonomia.

A regra padrão é:

```text
read-only first
```

O OpenCode pode usar MCP para observar, consultar e reduzir incerteza.  
Ele não deve usar MCP para escrever, mover, alterar, publicar, reiniciar, deletar ou operar recursos externos sem autorização explícita.

---

## Fonte canônica

Políticas e protocolos principais:

```text
core/policies/03-mcp-policy.md
core/policies/07-trusted-integrations-policy.md
core/policies/10-project-state-vs-board-policy.md
core/policies/05-secret-and-prod-policy.md
core/protocols/12-external-state-reading.md
core/protocols/06-evidence-standard.md
```

Skills relacionadas:

```text
skills/integration/mcp-readonly-operator/SKILL.md
skills/integration/github-projects-readonly/SKILL.md
skills/integration/github-readonly-ops/SKILL.md
skills/integration/cloud-readonly-inspection/SKILL.md
skills/integration/observability-readonly-inspection/SKILL.md
skills/integration/docs-research-operator/SKILL.md
skills/security/secrets-and-config-hygiene/SKILL.md
```

Agente responsável:

```text
adapters/opencode/agents/mcp-observer.md
```

---

## Regra central

MCP no OpenCode serve para:

- ler contexto externo;
- reduzir incerteza;
- confirmar estado remoto;
- consultar documentação;
- observar board/issues/PRs;
- inspecionar cloud metadata;
- ler sinais de observabilidade;
- produzir evidência factual.

MCP não serve, por padrão, para:

- alterar estado remoto;
- mover cards;
- fechar issues;
- comentar em PR;
- disparar workflows;
- alterar cloud config;
- reiniciar serviços;
- fazer deploy;
- manipular segredos;
- tocar produção.

---

## Modo padrão

```text
default_mode: read-only
```

Operações permitidas:

```text
listar
buscar
abrir
ler
consultar
inspecionar
resumir
```

Operações proibidas sem autorização explícita:

```text
criar
editar
deletar
mover
fechar
comentar
aplicar label
alterar status
disparar workflow
alterar configuração
alterar recurso cloud
reiniciar recurso
fazer deploy
executar ação destrutiva
```

---

## Integrações documentadas

```text
adapters/opencode/mcp/
├─ README.md
├─ github-projects.md
├─ github-issues-prs.md
├─ cloud-readonly.md
└─ observability-readonly.md
```

---

## Quando usar MCP

Use MCP quando houver uma pergunta externa clara.

Exemplos:

```text
Qual é o status deste item no board?
Esta issue tem critério de aceite adicional?
Este PR já tem comentário relevante?
Qual branch/commit está no remoto?
O recurso cloud existe e em qual ambiente?
Há erro recente nos logs filtrados?
A documentação oficial confirma esse comportamento?
```

Não use MCP quando:

- a resposta já está no workspace;
- a consulta é curiosidade;
- não há pergunta clara;
- a fonte externa não muda a decisão;
- o uso só aumentaria contexto;
- a operação exigiria escrita.

---

## Separação entre fontes

### Workspace local

Fonte principal para verdade técnica:

```text
código
testes
PROJECT_STATE.md
AUTHORITY_SOURCES.md
LOCAL_COMMANDS.md
OPERATIONAL_REALITY.md
ADRs
```

### GitHub Projects

Fonte de coordenação:

```text
status
prioridade
sequência
issue relacionada
dependências de trabalho
```

### GitHub issues/PRs

Fonte de contexto de trabalho:

```text
pedido
discussão
critérios de aceite
comentários
diff remoto
estado de review
```

### Cloud

Fonte de realidade operacional externa:

```text
recursos
metadata
ambientes
status
configuração não sensível
identidade sem segredo
```

### Observabilidade

Fonte de evidência operacional:

```text
logs filtrados
métricas
traces
alertas
health signals
```

---

## Board não é verdade técnica

GitHub Projects organiza trabalho.

`PROJECT_STATE.md` preserva verdade técnica.

O board pode dizer:

```text
o que está planejado
o que está em progresso
o que foi marcado como done
qual prioridade existe
```

O board não prova:

```text
que o código está correto
que a arquitetura mudou
que a validação passou
que a decisão técnica está registrada
que a task está realmente concluída
```

---

## Evidência via MCP

Leitura MCP pode contar como evidência quando:

- a fonte é confiável;
- a pergunta era clara;
- o escopo foi limitado;
- o achado foi registrado;
- limitações foram declaradas;
- dados sensíveis foram protegidos.

Toda evidência MCP relevante deve indicar:

```text
fonte
escopo
achado
limitação
impacto na task
```

---

## Proteção de dados

Nunca reproduzir:

```text
secrets
tokens
connection strings
cookies
headers Authorization
payload sensível
dados pessoais desnecessários
logs brutos extensos
stack traces com segredo
```

Quando necessário, mascarar:

```text
<redacted>
<masked>
<secret-present-but-not-shown>
```

---

## Escalonamento obrigatório

Pausar e escalar quando:

- a próxima ação exigir escrita externa;
- a integração não estiver registrada ou confiável;
- houver produção;
- houver segredo;
- houver dado real sensível;
- houver risco de segurança;
- fonte externa contradizer authority source local;
- board e `PROJECT_STATE.md` divergirem;
- observabilidade indicar incidente ativo;
- cloud inspection revelar risco alto.

---

## Output recomendado

Para consultas MCP relevantes, produzir:

```md
# MCP Read-Only Note

## Pergunta externa
<o que precisava ser consultado>

## Fonte/integração
<GitHub Projects | Issues/PRs | Cloud | Observability | Docs | outro>

## Escopo
<repo, issue, PR, board, ambiente, janela, recurso>

## Modo
read-only

## Achados factuais
- <achado 1>
- <achado 2>

## Limitações
- <limitação 1>
- <limitação 2>

## Dados sensíveis
<não acessados | mascarados | risco identificado>

## Implicação para a task
<como isso afeta plan, review, handoff ou escalonamento>

## Veredito
<suficiente | investigar mais | escalar>
```

---

## Declaração operacional curta

MCP no OpenCode observa primeiro.  
Se a próxima ação altera algo fora do workspace, já não é observação: é escalonamento.