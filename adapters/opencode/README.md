# OpenCode Adapter

## Finalidade

Este diretório contém a tradução do harness canônico para o runtime do OpenCode.

O adapter não redefine a engenharia.  
Ele adapta a engenharia para uma ferramenta concreta.

O núcleo canônico continua vivendo em:

```text
core/
skills/
agents/
templates/
```

Este adapter apenas explica como o OpenCode deve carregar, interpretar e aplicar esse sistema.

---

## Princípio central

```text
O núcleo governa.
O adapter traduz.
O runtime executa.
```

Se uma regra continuaria verdadeira ao trocar OpenCode por outro agente, ela pertence ao núcleo.

Se uma regra depende da semântica, configuração, comandos, agentes, permissões ou UX do OpenCode, ela pertence a este adapter.

---

## Estrutura do adapter

```text
adapters/opencode/
├─ README.md
├─ AGENTS.md
├─ opencode.json
├─ agents/
├─ commands/
├─ mcp/
├─ plugins/
└─ permissions/
```

---

## O que pertence a este adapter

Pertence a `adapters/opencode/`:

- rules persistentes para o OpenCode;
- wiring de agentes específicos do runtime;
- comandos operacionais do OpenCode;
- configuração do adapter;
- documentação de MCP no OpenCode;
- permissões específicas de runtime;
- plugins específicos do OpenCode;
- orientações de instalação e uso dentro do OpenCode.

---

## O que não pertence a este adapter

Não pertence a este adapter:

- missão do harness;
- princípios globais;
- policies canônicas;
- protocols canônicos;
- schemas de artifacts;
- skills globais;
- contratos canônicos de agentes;
- templates reutilizáveis;
- decisões específicas de projeto;
- comandos reais de um workspace;
- estado técnico de um projeto.

Esses itens pertencem ao `core/`, `skills/`, `agents/`, `templates/` ou ao workspace concreto.

---

## Fontes canônicas que este adapter deve respeitar

Antes de alterar este adapter, consultar:

```text
core/constitution/
core/protocols/
core/policies/
core/artifacts/
core/taxonomy/
core/observability/
core/governance/
skills/
agents/
templates/
```

Arquivos especialmente relevantes:

```text
core/policies/04-tool-and-runtime-boundaries.md
core/policies/03-mcp-policy.md
core/policies/00-command-safety-policy.md
core/policies/01-file-mutation-policy.md
core/policies/02-git-policy.md
core/policies/05-secret-and-prod-policy.md
core/protocols/00-implementation-flow.md
core/protocols/06-evidence-standard.md
core/protocols/10-entropy-management.md
core/protocols/11-project-state-maintenance.md
core/taxonomy/01-agents-taxonomy.md
core/taxonomy/02-skills-taxonomy.md
core/taxonomy/05-quality-guardrails-catalog.md
```

---

## Como o OpenCode deve usar o harness

O OpenCode deve operar em camadas:

```text
1. AGENTS.md
   Regras persistentes e compactas do runtime.

2. agents/
   Contratos runtime-specific dos papéis operacionais.

3. commands/
   Atalhos de fluxo para plan, investigate, implement, review, handoff e project-state.

4. skills/
   Capacidades acionáveis consultadas sob demanda.

5. templates/
   Moldes para workspace, packets, ADRs e checklists.

6. core/
   Fonte canônica da doutrina, policies, protocols, artifacts e governança.
```

---

## Regra de uso de contexto

O adapter não deve despejar todo o harness no contexto da sessão.

O OpenCode deve carregar:

- regras persistentes mínimas via `AGENTS.md`;
- agente específico quando o papel for acionado;
- skill específica quando a task exigir;
- template específico quando artifact for necessário;
- policy/protocol específico quando houver risco, ambiguidade ou conflito.

Evitar carregar documentação inteira sem necessidade.

---

## Fluxo operacional esperado

### Task funcional comum

```text
Implementation Packet
↓
planner
↓
Execution Plan
↓
implementer
↓
Completion Packet
↓
reviewer, se necessário
↓
delivery-prep
```

### Investigação

```text
Pergunta factual
↓
researcher ou mcp-observer
↓
Investigation Note
↓
planner ou Core Architect
```

### Decisão arquitetural

```text
Execution Plan ou dúvida estrutural
↓
architect-critic
↓
Review Report ou Escalation Note
↓
Core Architect / humano
```

---

## Agentes do adapter

Os contratos canônicos vivem em `agents/` na raiz do harness.

As versões em `adapters/opencode/agents/` devem ser adaptações runtime-specific desses contratos, não reescritas independentes.

Agentes previstos:

```text
planner
researcher
implementer
reviewer
architect-critic
delivery-prep
mcp-observer
```

---

## Comandos do adapter

Comandos previstos:

```text
plan
investigate
implement
review
handoff
project-state
```

Cada comando deve:

- declarar objetivo;
- indicar agente responsável;
- indicar artifacts esperados;
- indicar skills prováveis;
- respeitar classe de risco;
- definir quando escalar.

---

## MCP no OpenCode

MCP deve começar conservador e read-only.

Uso legítimo:

- ler GitHub Projects;
- ler issues e PRs;
- consultar documentação;
- inspecionar cloud metadata;
- consultar observabilidade;
- reduzir incerteza factual.

Uso proibido sem autorização explícita:

- mover cards;
- editar issues;
- comentar em PR;
- disparar workflow;
- alterar recurso cloud;
- aplicar deploy;
- alterar config;
- tocar produção;
- manipular segredo.

---

## Permissões

Permissões devem seguir o princípio de menor privilégio.

Por padrão:

```text
planner          → leitura e plano
researcher       → leitura/investigação
implementer      → mutação local controlada
reviewer         → leitura/review
architect-critic → leitura/crítica arquitetural
delivery-prep    → leitura, handoff, sugestão de state/commit
mcp-observer     → leitura externa read-only
```

Qualquer escrita externa deve ser tratada como exceção governada.

---

## opencode.json

`opencode.json` nesta fase é um placeholder conservador.

Ele existe para marcar a presença do adapter e registrar intenção de configuração, mas não deve inventar schema de runtime sem validação contra a versão real do OpenCode.

Antes de usar `opencode.json` como configuração executável, validar:

```bash
opencode --help
opencode config --help
```

ou a documentação oficial da versão instalada.

---

## Instalação pretendida

A instalação final ainda será definida nas ondas seguintes.

A intenção é permitir dois usos:

### Uso global

O harness vive fora dos projetos, por exemplo:

```text
~/engineering/harness/
```

E o OpenCode referencia suas rules, agents, commands e skills globais.

### Uso por workspace

Cada projeto recebe templates locais em seu próprio repositório:

```text
WORKSPACE_GUIDE.md
PROJECT_CONTEXT.md
AUTHORITY_SOURCES.md
LOCAL_COMMANDS.md
PROJECT_STATE.md
WORKTREE_POLICY.md
RISK_SURFACES.md
DONE_CRITERIA.md
OPERATIONAL_REALITY.md
GITHUB_PROJECTS_CONTEXT.md
```

---

## Regras de evolução do adapter

Antes de adicionar algo ao adapter, perguntar:

1. isso é específico do OpenCode?
2. isso não pertence ao núcleo canônico?
3. isso reduz fricção operacional real?
4. isso preserva portabilidade futura?
5. isso não duplica responsibility já existente?
6. isso não aumenta permissões sem necessidade?

Se a resposta for fraca, não adicionar.

---

## Status

```text
Status: em construção
Fase: adapter OpenCode — onda 1
Próximo bloco: agents runtime-specific
```