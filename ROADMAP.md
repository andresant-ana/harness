# Roadmap do Harness

Este roadmap descreve a direção de evolução da engenharia de harness e agentes.

Ele não substitui a documentação canônica do repositório. Sua função é registrar, em alto nível, a trilha evolutiva do sistema, o estado atual da implementação e os próximos passos de maturidade.

---

## Estado atual

```text
Versão atual: 0.2.0-alpha
Fase atual: Fase 1 concluída documentalmente
Próximo estágio: piloto controlado
Runtime inicial: OpenCode
Maturidade: alpha
```

A arquitetura canônica do harness foi materializada.

O repositório já contém:

- raiz fundadora;
- `core/`;
- `skills/`;
- `agents/`;
- `templates/`;
- `adapters/opencode/`.

O próximo objetivo é validar a engenharia em uso real, antes de promover qualquer congelamento de v1.

---

## Fases do programa

### Fase 0 — Definição do programa

Status:

```text
concluída
```

Objetivo:

- definir propósito do harness;
- separar camada estratégica e camada executora;
- estabelecer o conceito de Core Architect;
- definir o papel do coding agent como executor governado;
- escolher OpenCode como primeiro runtime-alvo.

Resultado:

- programa conceitualmente definido;
- princípios iniciais estabelecidos;
- estratégia global clara.

---

### Fase 1 — Arquitetura canônica do harness

Status:

```text
concluída documentalmente
```

Objetivo:

- materializar a estrutura do repositório;
- criar o núcleo canônico;
- definir protocols, policies, artifacts e taxonomy;
- criar skills iniciais;
- definir agents canônicos;
- criar templates;
- criar adapter inicial do OpenCode.

Resultado:

- harness existe como sistema versionável;
- documentação canônica está organizada;
- runtime inicial possui tradução própria;
- pronto para piloto controlado.

Observação:

- `opencode.json` ainda é placeholder conservador;
- o adapter precisa ser validado contra a versão real instalada do OpenCode;
- a maturidade ainda é alpha.

---

### Fase 2 — Doutrina global do agente

Status:

```text
materializada dentro do core e do AGENTS.md inicial
```

Objetivo:

- consolidar comportamento obrigatório do executor;
- impedir atuação autônoma sem envelope;
- definir planejamento antes de mutação;
- impor evidência;
- controlar risco, contexto e entropia.

Resultado atual:

- regras persistentes no `adapters/opencode/AGENTS.md`;
- leis operacionais no `core/constitution/`;
- protocols e policies formalizados.

Próximo refinamento:

- testar se a doutrina é curta o suficiente para runtime real;
- cortar redundância se o piloto revelar excesso.

---

### Fase 3 — Pacote inicial de skills globais

Status:

```text
concluída para escopo inicial
```

Famílias implementadas:

- orchestration;
- engineering;
- security;
- hygiene;
- platform;
- integration;
- stack.

Stacks iniciais:

- .NET;
- React;
- PostgreSQL;
- Azure.

Próximo refinamento:

- validar quais skills são usadas de verdade;
- remover ou compactar skills pouco acionáveis;
- adicionar novas stacks apenas por dor real.

---

### Fase 4 — Adapter global do Gemini CLI

Status:

```text
fora do escopo atual
```

Decisão atual:

- não implementar agora;
- manter foco no OpenCode;
- evitar múltiplos adapters prematuros.

Critério para reabrir:

- necessidade real de segundo runtime;
- maturidade do adapter OpenCode;
- evidência de valor operacional.

---

### Fase 5 — Adapter global do OpenCode

Status:

```text
implementação inicial concluída
```

Conteúdo implementado:

- `README.md`;
- `AGENTS.md`;
- `opencode.json`;
- agents runtime-specific;
- commands;
- MCP read-only;
- plugins policy;
- permissions matrix.

Pendências:

- validar schema real do `opencode.json`;
- testar carregamento real pelo OpenCode;
- verificar ergonomia dos commands;
- medir custo de contexto;
- ajustar redundâncias.

---

### Fase 6 — Camada MCP conservadora

Status:

```text
documentada inicialmente
```

Postura atual:

- MCP read-only first;
- sem escrita externa por padrão;
- sem produção;
- sem segredos;
- sem automação sensível.

Integrações documentadas:

- GitHub Projects read-only;
- GitHub Issues/PRs read-only;
- cloud read-only;
- observability read-only.

Próximo refinamento:

- registrar trusted integrations reais;
- testar MCP no piloto;
- evitar que board substitua `PROJECT_STATE.md`;
- manter escrita externa fora do fluxo padrão.

---

### Fase 7 — Templates de workspace

Status:

```text
concluída
```

Templates implementados:

- workspace docs;
- packets;
- ADRs;
- checklists.

Objetivo cumprido:

- permitir bootstrap de um projeto real sem improviso estrutural;
- separar verdade global do harness e verdade local do workspace;
- formalizar `PROJECT_STATE.md` como memória técnica viva.

Próximo refinamento:

- usar em workspace real;
- cortar campos que gerarem burocracia;
- reforçar campos que evitarem erro do agente.

---

### Fase 8 — Piloto controlado

Status:

```text
próximo passo
```

Objetivo:

- aplicar o harness em um workspace real;
- executar uma task concreta com OpenCode;
- observar fricção, lacunas e qualidade;
- verificar se os artifacts são úteis;
- medir risco de burocracia;
- validar se o agente respeita boundaries;
- testar `PROJECT_STATE.md`;
- testar commands;
- testar MCP read-only, se necessário.

Critérios de sucesso:

- task executada com escopo claro;
- Execution Plan útil;
- implementação sem expansão indevida;
- Completion Packet honesto;
- review detectando problemas reais;
- state update usado com parcimônia;
- sem slop relevante;
- sem over-engineering;
- sem dependência indevida de contexto excessivo.

Critérios de falha:

- agente ignora regras;
- contexto fica grande demais;
- artifacts viram burocracia;
- comandos são vagos;
- skills não são acionáveis;
- OpenCode não consegue usar a estrutura;
- `PROJECT_STATE.md` vira changelog;
- MCP aumenta ruído em vez de reduzir incerteza.

---

### Fase 9 — Hardening e congelamento da v1

Status:

```text
pendente após piloto
```

Objetivo:

- cortar gordura;
- reduzir redundância;
- corrigir fricções;
- fortalecer lacunas;
- estabilizar convenções;
- validar adapter real;
- congelar primeira versão madura.

Saídas esperadas:

- `1.0.0` ou `1.0.0-rc`;
- README final;
- changelog consolidado;
- release process aplicado;
- guidelines de instalação/uso;
- primeiro conjunto de lessons learned;
- backlog pós-piloto priorizado.

---

## Ondas já concluídas

### Onda 1 — Fundação estrutural

Status:

```text
concluída
```

Incluiu:

- raiz do repositório;
- estrutura física;
- constitution inicial;
- arquivos fundadores.

---

### Onda 2 — Protocolos e policies

Status:

```text
concluída
```

Incluiu:

- implementation flow;
- repository discovery;
- authority sources;
- context economy;
- secure engineering;
- production-minded execution;
- evidence standard;
- review;
- handoff;
- stuck recovery;
- entropy management;
- project state maintenance;
- external state reading;
- command/file/git/MCP/tool policies;
- secret/prod/dependency/observability policies.

---

### Onda 3 — Artifacts, taxonomy e observability

Status:

```text
concluída
```

Incluiu:

- schemas de packets;
- matriz risco → artifacts;
- taxonomia de agents;
- taxonomia de skills;
- catálogo de guardrails;
- tracing;
- evals;
- metrics;
- replay;
- entropy signals.

---

### Onda 4 — Skills prioritárias

Status:

```text
concluída
```

Incluiu:

- orchestration;
- engineering;
- security;
- hygiene;
- platform;
- integration;
- stack.

---

### Onda 5 — Agents canônicos

Status:

```text
concluída
```

Incluiu:

- planner;
- researcher;
- implementer;
- reviewer;
- architect-critic;
- delivery-prep;
- mcp-observer.

---

### Onda 6 — Templates

Status:

```text
concluída
```

Incluiu:

- workspace;
- packets;
- ADR;
- checklists.

---

### Onda 7 — Adapter do OpenCode

Status:

```text
concluída como implementação inicial
```

Incluiu:

- base do adapter;
- runtime rules;
- agents específicos;
- commands;
- MCP;
- plugins;
- permissions.

---

## Fora do escopo imediato

Itens deliberadamente fora do escopo antes do piloto:

- automação write via MCP;
- deploy automatizado pelo harness;
- produção controlada por agente;
- manipulação de segredos por agente;
- múltiplos adapters paralelos;
- plugin complexo;
- skill bloat;
- integração com todos os projetos reais;
- especialização enciclopédica de stack;
- tentativa de congelar v1 sem uso real.

---

## Critério de sucesso da versão 0.2.0-alpha

A versão `0.2.0-alpha` é bem-sucedida se:

- a estrutura estiver completa;
- a documentação canônica for navegável;
- o adapter OpenCode possuir ponto de partida;
- os templates permitirem bootstrap de workspace;
- as permissões impedirem autonomia excessiva;
- MCP estiver conservador;
- houver base suficiente para piloto controlado.

---

## Próximo marco

```text
Marco: Piloto controlado
Objetivo: validar o harness em uso real
Resultado esperado: lista de ajustes para hardening
```

O próximo passo não é expandir a engenharia.  
É testá-la.