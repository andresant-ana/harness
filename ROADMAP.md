# Roadmap do Harness

Este roadmap descreve a direção de evolução da engenharia de harness e agentes.

Ele não substitui a documentação oficial nem a ordem detalhada de implantação do programa. Sua função é registrar, em alto nível, a trilha evolutiva do sistema dentro deste repositório canônico.

---

## Estado atual

Fase atual: **Fase 1 — Arquitetura canônica do harness**

Objetivo imediato:
- consolidar a estrutura física do sistema;
- preencher a constituição inicial;
- congelar a base do núcleo canônico;
- preparar o terreno para protocolos, policies, artifacts, taxonomia e observabilidade.

---

## Onda atual

### Onda 1 — Fundação estrutural
Escopo:
- raiz do repositório
- `core/constitution/`
- definição do inventário canônico
- congelamento da linguagem-base do sistema

Resultado esperado:
- o harness deixa de ser apenas uma ideia e passa a existir como arquitetura documentada.

---

## Próximas ondas

### Onda 2 — Protocolos e policies
Escopo:
- `core/protocols/`
- `core/policies/`
- início do comportamento operacional formal

Resultado esperado:
- o sistema passa a ter fluxo, guardrails, boundaries e política de decisão.

### Onda 3 — Artifacts, taxonomy e observability
Escopo:
- schemas canônicos dos packets
- taxonomia formal de agents e skills
- baseline de tracing, evals e sinais de entropia

Resultado esperado:
- o sistema passa a ter artifacts formais e capacidade de medir sua própria qualidade.

### Onda 4 — Skills prioritárias
Escopo:
- orchestration
- engineering
- security
- integration
- higiene inicial
- stack capabilities prioritárias

Resultado esperado:
- o sistema passa a ter capacidades acionáveis reais.

### Onda 5 — Agents canônicos
Escopo:
- planner
- researcher
- implementer
- reviewer
- architect-critic
- delivery-prep
- mcp-observer

Resultado esperado:
- o sistema passa a ter papéis formais independentes do runtime.

### Onda 6 — Templates de workspace
Escopo:
- bootstrap de projeto
- packets
- state document
- authority sources
- operational reality
- checklists

Resultado esperado:
- qualquer projeto novo pode ser iniciado sem improviso estrutural.

### Onda 7 — Adapter do OpenCode
Escopo:
- `adapters/opencode/`
- AGENTS.md
- opencode.json
- commands
- permissions
- MCP read-only
- plugins básicos

Resultado esperado:
- a arquitetura canônica passa a operar no runtime real.

### Onda 8 — Piloto controlado
Escopo:
- execução de task real
- tracing
- review
- handoff
- captura de falhas e fricções

Resultado esperado:
- a engenharia deixa de ser apenas teórica e passa a ser validada em uso real.

### Onda 9 — Hardening
Escopo:
- cortar gordura
- corrigir fricções
- simplificar excesso
- estabilizar convenções
- consolidar versão inicial madura

Resultado esperado:
- primeira versão operacional consistente do harness.

---

## Fora do escopo imediato

Itens deliberadamente fora do escopo desta primeira etapa:

- automação write via MCP
- deploy automatizado pelo harness
- plugin complexo no runtime
- múltiplos adapters paralelos
- skill bloat
- integração prematura com todos os projetos reais
- especialização enciclopédica da stack

---

## Critério de sucesso desta fase

A fase atual será considerada bem-sucedida quando:

- a estrutura do sistema estiver congelada;
- a constituição inicial estiver escrita;
- a linguagem-base do harness estiver consistente;
- a fronteira entre camada estratégica e camada executora estiver explícita;
- houver material suficiente para avançar para protocolos e policies sem improviso.

---

## Regra de progresso

A engenharia só avança de fase se a fase anterior estiver:

- materializada,
- legível,
- coerente,
- versionável,
- e útil o suficiente para orientar a próxima.

Neste repositório, progresso sem coerência não conta como progresso.