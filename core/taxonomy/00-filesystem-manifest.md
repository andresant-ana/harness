# Manifesto Interno do Filesystem

## Finalidade

Este documento descreve a estrutura canônica de diretórios e arquivos do harness.

Seu papel é servir como mapa interno do repositório, explicando o que pertence a cada camada, qual é a função de cada diretório e quais fronteiras não devem ser misturadas.

Este arquivo não substitui a documentação oficial do harness.  
Ele materializa, dentro do próprio repositório, a topologia estrutural que o sistema deve respeitar.

---

## Tese central

A estrutura do harness não é uma coleção de pastas.

Ela é uma separação deliberada entre:

- doutrina;
- protocolo;
- política;
- artefato;
- taxonomia;
- observabilidade;
- governança;
- capacidade acionável;
- contrato de agente;
- adaptação por runtime;
- template reutilizável.

Cada camada existe para reduzir entropia, evitar mistura de responsabilidades e permitir evolução controlada.

---

## Visão geral

```text
harness/
├─ README.md
├─ VERSION
├─ CHANGELOG_HARNESS.md
├─ ROADMAP.md
├─ core/
├─ skills/
├─ agents/
├─ adapters/
└─ templates/
```

---

## Raiz do repositório

A raiz contém identidade, versionamento e direção macro do harness.

```text
harness/
├─ README.md
├─ VERSION
├─ CHANGELOG_HARNESS.md
└─ ROADMAP.md
```

### `README.md`

Documento principal do repositório.

Deve explicar:
- o que é o harness;
- qual problema ele resolve;
- qual é sua organização;
- em que estágio está;
- como os diretórios principais se relacionam.

### `VERSION`

Arquivo simples com a versão atual do harness.

### `CHANGELOG_HARNESS.md`

Histórico de mudanças estruturais, documentais e comportamentais do harness.

### `ROADMAP.md`

Mapa de evolução do sistema, fases, prioridades e itens fora do escopo imediato.

---

## `core/`

`core/` é o firmware do harness.

Ele contém o núcleo doutrinário e operacional permanente da engenharia.

```text
core/
├─ constitution/
├─ protocols/
├─ policies/
├─ artifacts/
├─ taxonomy/
├─ observability/
└─ governance/
```

Tudo que vive em `core/` deve ser:
- global;
- durável;
- independente de projeto;
- independente de runtime concreto;
- útil para governar o comportamento do harness.

---

## `core/constitution/`

Contém missão, princípios, leis, classes de risco e fronteiras fundamentais.

```text
core/constitution/
├─ 00-mission.md
├─ 01-principles.md
├─ 02-operating-laws.md
├─ 03-risk-classes.md
├─ 04-escalation-policy.md
├─ 05-autonomy-policy.md
├─ 06-architecture-by-pain.md
├─ 07-task-isolation-and-worktree.md
└─ 08-human-vs-agent-boundary.md
```

A constitution define o que o sistema é, o que ele protege, o que ele rejeita e como ele separa responsabilidade entre humano, Core Architect e executor.

Ela não deve conter detalhes de runtime, comandos específicos ou verdade local de projeto.

---

## `core/protocols/`

Contém os fluxos de operação do sistema.

```text
core/protocols/
├─ 00-implementation-flow.md
├─ 01-repository-discovery.md
├─ 02-authority-sources.md
├─ 03-context-economy-and-compaction.md
├─ 04-secure-engineering-baseline.md
├─ 05-production-minded-execution.md
├─ 06-evidence-standard.md
├─ 07-review-protocol.md
├─ 08-handoff-protocol.md
├─ 09-stuck-detection-and-recovery.md
├─ 10-entropy-management.md
├─ 11-project-state-maintenance.md
└─ 12-external-state-reading.md
```

Protocolos dizem como o harness trabalha.

Eles cobrem:
- fluxo de implementação;
- discovery;
- authority sources;
- economia de contexto;
- segurança;
- produção;
- evidência;
- review;
- handoff;
- stuck recovery;
- entropia;
- state maintenance;
- leitura externa.

---

## `core/policies/`

Contém regras de permissão, restrição e governança de superfícies sensíveis.

```text
core/policies/
├─ 00-command-safety-policy.md
├─ 01-file-mutation-policy.md
├─ 02-git-policy.md
├─ 03-mcp-policy.md
├─ 04-tool-and-runtime-boundaries.md
├─ 05-secret-and-prod-policy.md
├─ 06-automation-promotion-policy.md
├─ 07-trusted-integrations-policy.md
├─ 08-dependency-introduction-policy.md
├─ 09-observability-minimum-policy.md
└─ 10-project-state-vs-board-policy.md
```

Policies dizem o que é permitido, proibido ou condicionado.

Elas não devem ser confundidas com protocolos.  
Se o documento descreve um fluxo, provavelmente é protocolo.  
Se impõe limite, permissão ou boundary, provavelmente é policy.

---

## `core/artifacts/`

Contém os schemas canônicos dos artefatos formais do fluxo.

```text
core/artifacts/
├─ 00-implementation-packet.schema.md
├─ 01-execution-plan.schema.md
├─ 02-completion-packet.schema.md
├─ 03-review-report.schema.md
├─ 04-escalation-note.schema.md
├─ 05-investigation-note.schema.md
└─ 06-project-state-entry.schema.md
```

Artifacts estruturam as entradas, planos, saídas, revisões, escalonamentos, investigações e atualizações de estado.

Eles existem para evitar que a comunicação do sistema dependa apenas de texto livre.

---

## `core/taxonomy/`

Contém a classificação estrutural do sistema.

```text
core/taxonomy/
├─ 00-filesystem-manifest.md
├─ 01-agents-taxonomy.md
├─ 02-skills-taxonomy.md
├─ 03-stack-capabilities-taxonomy.md
├─ 04-risk-to-artifacts-matrix.md
└─ 05-quality-guardrails-catalog.md
```

Taxonomy não cria novas leis.  
Ela organiza o que já existe.

Sua função é tornar explícitos:
- estrutura do filesystem;
- catálogo de agentes;
- catálogo de skills;
- capacidades globais por stack;
- relação entre risco e artifacts;
- guardrails de qualidade.

---

## `core/observability/`

Contém mecanismos de observação do próprio harness.

```text
core/observability/
├─ 00-tracing-model.md
├─ 01-evals-baseline.md
├─ 02-metrics-catalog.md
├─ 03-replay-guidelines.md
└─ 04-entropy-signals.md
```

Essa camada existe para medir comportamento, falhas, eficiência, perda de contexto e degradação.

---

## `core/governance/`

Contém regras de evolução controlada do harness.

```text
core/governance/
├─ 00-maturity-model.md
├─ 01-deprecation-policy.md
├─ 02-experimental-registry.md
├─ 03-trusted-integrations-registry.md
├─ 04-pilot-guidelines.md
├─ 05-release-process.md
└─ 06-backlog-for-post-pilot.md
```

Governance impede que o harness cresça por impulso.

Ela define maturidade, depreciação, experimentos, integrações confiáveis, piloto, release e backlog pós-piloto.

---

## `skills/`

Contém capacidades acionáveis sob demanda.

```text
skills/
├─ orchestration/
├─ engineering/
├─ stack/
├─ platform/
├─ integration/
├─ security/
└─ hygiene/
```

Skills não são documentação enciclopédica.  
Skills são métodos acionáveis.

Cada skill concreta deve viver em diretório próprio com pelo menos:

```text
<skill-name>/
└─ SKILL.md
```

Skills existem para trazer:
- checklist;
- método;
- anti-patterns;
- outputs esperados;
- limites;
- gatilhos de uso.

---

## `agents/`

Contém contratos canônicos dos agentes globais.

```text
agents/
├─ README.md
├─ planner.md
├─ researcher.md
├─ implementer.md
├─ reviewer.md
├─ architect-critic.md
├─ delivery-prep.md
└─ mcp-observer.md
```

Esses contratos são independentes do runtime.

Eles definem:
- papel;
- quando usar;
- quando não usar;
- inputs;
- outputs;
- limites;
- gatilhos de escalonamento.

---

## `adapters/`

Contém tradução do núcleo canônico para runtimes concretos.

```text
adapters/
└─ opencode/
```

O adapter não redefine doutrina.  
Ele traduz o sistema para a ferramenta.

Para OpenCode:

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

## `templates/`

Contém moldes reutilizáveis.

```text
templates/
├─ workspace/
├─ packets/
├─ adr/
└─ checklists/
```

Templates existem para reduzir improviso em novos projetos, artifacts, decisões e checklists.

Eles não são truth local de um projeto.  
Eles são ponto de partida.

---

## Regra de separação global vs local

Tudo que for global, durável e recorrente pertence ao harness.

Tudo que for específico de um projeto pertence ao workspace.

### Pertence ao harness

- princípios;
- policies;
- protocols;
- artifacts;
- agents canônicos;
- skills globais;
- templates;
- taxonomias;
- governança.

### Pertence ao workspace

- arquitetura local;
- comandos reais;
- `PROJECT_STATE.md`;
- operational reality;
- riscos específicos;
- decisões locais;
- board context;
- conventions do repositório.

---

## Regra de separação núcleo vs adapter

O núcleo define a doutrina.  
O adapter implementa a tradução para uma ferramenta.

Se algo continuaria verdadeiro trocando OpenCode por outro runtime, pertence ao núcleo.

Se algo depende de sintaxe, UX, config ou semântica do OpenCode, pertence ao adapter.

---

## Regra de evolução

Mudanças no filesystem devem ser raras, justificadas e versionadas.

Antes de adicionar diretório ou arquivo estrutural, perguntar:

1. isso é recorrente?
2. isso é global?
3. isso reduz entropia?
4. isso tem fronteira clara?
5. isso não duplica responsabilidade já existente?

Se a resposta for fraca, não adicionar.

---

## Declaração operacional curta

A árvore do harness é arquitetura.  
Cada diretório tem responsabilidade.  
Misturar camadas aumenta entropia e reduz governabilidade.