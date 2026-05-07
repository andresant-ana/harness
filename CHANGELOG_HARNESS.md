# Changelog do Harness

Todas as mudanças relevantes da engenharia de harness e agentes devem ser registradas aqui.

A proposta deste changelog não é registrar qualquer edição textual mínima, mas sim preservar as mudanças que alteram comportamento, escopo, estrutura, doutrina, governança, protocolos, policies, artifacts, skills, agents, templates ou adapters.

---

## 0.2.0-alpha

### Added

- Conclusão documental da Fase 1 da engenharia de harness.
- Materialização completa do núcleo `core/`.
- Adição da camada `core/constitution/`, contendo:
  - missão;
  - princípios;
  - leis operacionais;
  - classes de risco;
  - política de escalonamento;
  - política de autonomia;
  - arquitetura por dor real;
  - isolamento de task/worktree;
  - fronteira humano/Core Architect/agente.
- Adição da camada `core/protocols/`, contendo:
  - implementation flow;
  - repository discovery;
  - authority sources;
  - context economy and compaction;
  - secure engineering baseline;
  - production-minded execution;
  - evidence standard;
  - review protocol;
  - handoff protocol;
  - stuck detection and recovery;
  - entropy management;
  - project state maintenance;
  - external state reading.
- Adição da camada `core/policies/`, contendo:
  - command safety;
  - file mutation;
  - git;
  - MCP;
  - tool and runtime boundaries;
  - secret and production;
  - automation promotion;
  - trusted integrations;
  - dependency introduction;
  - observability minimum;
  - project state vs board.
- Adição da camada `core/artifacts/`, contendo schemas para:
  - Implementation Packet;
  - Execution Plan;
  - Completion Packet;
  - Review Report;
  - Escalation Note;
  - Investigation Note;
  - Project State Entry.
- Adição da camada `core/taxonomy/`, contendo:
  - filesystem manifest;
  - agents taxonomy;
  - skills taxonomy;
  - stack capabilities taxonomy;
  - risk-to-artifacts matrix;
  - quality guardrails catalog.
- Adição da camada `core/observability/`, contendo:
  - tracing model;
  - evals baseline;
  - metrics catalog;
  - replay guidelines;
  - entropy signals.
- Adição da camada `core/governance/`, contendo:
  - maturity model;
  - deprecation policy;
  - experimental registry;
  - trusted integrations registry;
  - pilot guidelines;
  - release process;
  - backlog for post-pilot.
- Adição do pacote inicial de `skills/`, organizado em:
  - orchestration;
  - engineering;
  - security;
  - hygiene;
  - platform;
  - integration;
  - stack.
- Adição das skills iniciais de stack para:
  - .NET;
  - React;
  - PostgreSQL;
  - Azure.
- Adição dos contratos canônicos de `agents/`:
  - planner;
  - researcher;
  - implementer;
  - reviewer;
  - architect-critic;
  - delivery-prep;
  - mcp-observer.
- Adição de `templates/workspace/`, contendo:
  - WORKSPACE_GUIDE;
  - PROJECT_CONTEXT;
  - AUTHORITY_SOURCES;
  - LOCAL_COMMANDS;
  - PROJECT_STATE;
  - WORKTREE_POLICY;
  - RISK_SURFACES;
  - DONE_CRITERIA;
  - OPERATIONAL_REALITY;
  - GITHUB_PROJECTS_CONTEXT.
- Adição de `templates/packets/`, contendo:
  - Implementation Packet;
  - Execution Plan;
  - Completion Packet;
  - Review Report;
  - Escalation Note;
  - Investigation Note.
- Adição de `templates/adr/`, contendo:
  - ADR;
  - ADR Lite.
- Adição de `templates/checklists/`, contendo:
  - Project Bootstrap;
  - Task Intake;
  - Plan Review;
  - Pre-Merge Review;
  - Operational Reality;
  - Anti-Slop;
  - Release Readiness.
- Adição do adapter inicial do OpenCode em `adapters/opencode/`.
- Adição de `adapters/opencode/AGENTS.md` como rules persistentes do runtime.
- Adição de `adapters/opencode/opencode.json` como placeholder conservador de configuração.
- Adição dos agents runtime-specific do OpenCode.
- Adição dos commands operacionais do OpenCode:
  - plan;
  - investigate;
  - implement;
  - review;
  - handoff;
  - project-state.
- Adição da documentação MCP read-only do OpenCode:
  - GitHub Projects;
  - GitHub Issues/PRs;
  - cloud read-only;
  - observability read-only.
- Adição da policy de plugins do OpenCode.
- Adição da matriz de permissões do OpenCode.
- Adição da política específica de permissões para board/GitHub Projects.

### Changed

- Atualização do estado do repositório de fundação inicial para harness estruturalmente completo em alpha.
- Atualização da direção do projeto para refletir que a próxima etapa é piloto controlado, não criação adicional de arquivos canônicos.
- Consolidação da separação entre:
  - núcleo canônico;
  - skills;
  - agents;
  - templates;
  - adapter;
  - workspace real.
- Formalização do `PROJECT_STATE.md` como memória técnica durável, distinta de changelog, backlog e board.
- Formalização do princípio de MCP read-only first.
- Formalização da regra de arquitetura por dor real como proteção contra over-engineering.
- Formalização da matriz de permissões por papel operacional.

### Notes

- Esta versão ainda é alpha.
- O harness está pronto para piloto controlado, mas não deve ser tratado como v1 madura.
- O adapter OpenCode foi documentado, mas ainda precisa ser validado contra o runtime real.
- `adapters/opencode/opencode.json` ainda é placeholder conservador e não deve ser tratado como schema executável final sem validação.
- MCP write, produção, segredos e automações externas continuam fora da autonomia padrão.
- A próxima etapa é testar o harness em um workspace real e capturar fricções.

### Intent

- Fechar a primeira versão estrutural do harness.
- Permitir bootstrap de projetos reais com templates locais.
- Permitir uso inicial do OpenCode sob regras persistentes, comandos, agentes e permissões.
- Criar base suficiente para piloto, observabilidade comportamental e hardening posterior.

---

## 0.1.0-alpha

### Added

- Inicialização do repositório canônico do harness.
- Materialização da árvore principal da engenharia.
- Definição da estrutura global do sistema.
- Início da primeira onda documental.
- Introdução dos arquivos fundadores da raiz do repositório.
- Início da `constitution/` como firmware do sistema.

### Notes

- O adapter do OpenCode ainda não havia sido iniciado.
- Skills ainda não haviam sido materializadas.
- Templates ainda não haviam sido materializados.
- A engenharia ainda estava em fase de formação estrutural.

### Intent

- Congelar a arquitetura canônica antes de qualquer acoplamento prematuro ao runtime.
- Garantir que a engenharia nascesse como sistema governável e versionável.