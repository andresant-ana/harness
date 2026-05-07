# Harness Engineering

Repositório canônico da engenharia de harness e agentes.

Este repositório é a **fonte única de verdade** da engenharia global do harness e da sua tradução inicial para o runtime OpenCode. Sua função é materializar, versionar e governar a arquitetura canônica do sistema antes de sua aplicação em workspaces reais.

O objetivo desta engenharia é transformar o coding agent em um executor disciplinado, verificável, econômico em contexto, seguro por desenho e subordinado a uma camada estratégica humana. Em vez de depender de prompts soltos e comportamento oportunista do modelo, o sistema organiza missão, princípios, leis operacionais, classes de risco, protocolos, policies, artifacts, skills, agents, templates, adapters e governança.

---

## O que este repositório é

Este repositório é:

- a arquitetura canônica do harness;
- o núcleo documental e operacional da engenharia;
- o lugar onde a doutrina do sistema é escrita, versionada e evoluída;
- a base global para uso em múltiplos workspaces;
- a fonte de adaptação para runtimes concretos, começando pelo OpenCode.

---

## O que este repositório não é

Este repositório não é:

- um projeto de produto;
- um workspace específico de aplicação;
- um repositório de código de negócio;
- um backlog de produto;
- um diário de sessão;
- uma coleção de prompts avulsos;
- uma garantia de maturidade operacional antes do piloto;
- uma configuração final validada do OpenCode em produção.

A engenharia nasce aqui como **sistema governável**.  
Depois ela é validada em projetos reais.

---

## Estado atual

Status atual do programa:

```text
Versão: 0.2.0-alpha
Fase: Fase 1 — arquitetura canônica e adapter inicial concluídos
Estado: pronto para piloto controlado
Runtime inicial: OpenCode
Maturidade: alpha documental/operacional inicial
```

A Fase 1 materializou:

- raiz fundadora do repositório;
- `core/` completo;
- `skills/` completo para o escopo inicial;
- `agents/` canônicos;
- `templates/` reutilizáveis;
- `adapters/opencode/` inicial;
- rules persistentes do OpenCode;
- agents runtime-specific;
- commands operacionais;
- MCP read-only;
- plugins policy;
- permissions matrix.

Ainda não foi validado em piloto real.  
O próximo passo é aplicar o harness em um workspace controlado e observar fricções, falhas, excesso de burocracia, lacunas de contexto e qualidade da execução.

---

## Princípio central

O agente não substitui a camada estratégica.

A camada estratégica continua sendo responsabilidade do humano e do Core Architect. O harness existe para fazer a camada executora operar com disciplina, previsibilidade, evidência, controle de risco, controle de entropia e respeito à realidade local do projeto.

A regra operacional curta é:

```text
Humano decide.
Core Architect estrutura.
Harness governa.
Executor executa.
Evidência valida.
```

---

## Estrutura do repositório

```text
harness/
├─ README.md
├─ VERSION
├─ CHANGELOG_HARNESS.md
├─ ROADMAP.md
├─ core/
│  ├─ constitution/
│  ├─ protocols/
│  ├─ policies/
│  ├─ artifacts/
│  ├─ taxonomy/
│  ├─ observability/
│  └─ governance/
├─ skills/
│  ├─ orchestration/
│  ├─ engineering/
│  ├─ stack/
│  │  ├─ dotnet/
│  │  ├─ react/
│  │  ├─ postgres/
│  │  └─ azure/
│  ├─ platform/
│  ├─ integration/
│  ├─ security/
│  └─ hygiene/
├─ agents/
├─ adapters/
│  └─ opencode/
└─ templates/
   ├─ workspace/
   ├─ packets/
   ├─ adr/
   └─ checklists/
```

---

## Lógica de organização

### `core/`

Contém o firmware do sistema:

- missão;
- princípios;
- leis operacionais;
- classes de risco;
- protocolos;
- policies;
- schemas de artifacts;
- taxonomia;
- observabilidade;
- governança.

O `core/` define o que é verdadeiro independentemente de runtime.

---

### `skills/`

Contém capacidades acionáveis sob demanda.

Skills são métodos operacionais especializados. Elas não são agentes e não são comandos. Uma skill ensina como executar uma capacidade específica com critérios, limites, inputs e outputs.

Famílias principais:

- orchestration;
- engineering;
- stack;
- platform;
- integration;
- security;
- hygiene.

---

### `agents/`

Contém os contratos canônicos dos agentes globais, independentes de runtime.

Agente não é personalidade.  
Agente é papel operacional.

Agentes canônicos:

- planner;
- researcher;
- implementer;
- reviewer;
- architect-critic;
- delivery-prep;
- mcp-observer.

---

### `templates/`

Contém moldes reutilizáveis para uso em projetos reais:

- workspace docs;
- packets;
- ADRs;
- checklists.

Templates não são verdade local.  
Eles viram verdade local apenas quando copiados, preenchidos e mantidos dentro de um workspace concreto.

---

### `adapters/`

Contém traduções do sistema canônico para runtimes concretos.

O primeiro adapter é:

```text
adapters/opencode/
```

O adapter OpenCode inclui:

- `AGENTS.md`;
- `opencode.json`;
- agents runtime-specific;
- commands;
- MCP read-only;
- plugins policy;
- permissions matrix.

O adapter não redefine a doutrina.  
Ele traduz a doutrina para o runtime.

---

## Regra de integridade

Tudo que for:

- recorrente;
- global;
- durável;
- independente de projeto;
- independente de domínio específico;

deve viver no harness.

Tudo que for:

- específico de um projeto;
- verdadeiro apenas para um repositório;
- dependente do domínio de negócio;
- ligado a comandos locais;
- ligado a riscos locais;
- ligado a arquitetura local;
- ligado a estado técnico vivo de um projeto;

deve viver no workspace do projeto, não aqui.

---

## Relação entre harness e workspace

O harness fornece:

- doutrina;
- policies;
- protocolos;
- skills;
- agentes;
- templates;
- comandos de runtime;
- regras de permissão.

O workspace fornece:

- `WORKSPACE_GUIDE.md`;
- `PROJECT_CONTEXT.md`;
- `AUTHORITY_SOURCES.md`;
- `LOCAL_COMMANDS.md`;
- `PROJECT_STATE.md`;
- `WORKTREE_POLICY.md`;
- `RISK_SURFACES.md`;
- `DONE_CRITERIA.md`;
- `OPERATIONAL_REALITY.md`;
- `GITHUB_PROJECTS_CONTEXT.md`, se houver board.

A verdade local do projeto vence conhecimento genérico do modelo.

---

## Relação com OpenCode

O OpenCode é o primeiro runtime-alvo.

A camada atual de OpenCode é inicial e conservadora. Ela documenta regras, agentes, comandos, MCP read-only e permissões, mas ainda precisa ser validada contra uso real.

Ponto importante:

```text
adapters/opencode/opencode.json
```

é um placeholder conservador nesta versão.  
Não deve ser tratado como configuração executável final antes de validar o schema real da versão instalada do OpenCode.

---

## Classes de risco

O harness usa cinco classes de risco:

```text
R0 — leitura/investigação sem mutação
R1 — mudança local pequena e reversível
R2 — mudança funcional relevante
R3 — mudança estrutural, sensível ou sistêmica
R4 — produção, segredo, irreversibilidade ou alto risco
```

A classe de risco define:

- autonomia;
- artifacts exigidos;
- validação;
- review;
- escalonamento;
- permissões;
- necessidade de aprovação humana.

---

## Artifacts principais

O fluxo operacional usa artifacts formais:

- Implementation Packet;
- Execution Plan;
- Completion Packet;
- Review Report;
- Escalation Note;
- Investigation Note;
- Project State Entry;
- ADR;
- ADR Lite.

Artifacts evitam que decisões, lacunas, riscos e evidências fiquem perdidos em conversa solta.

---

## Postura arquitetural

Este harness adota arquitetura por dor real.

A regra é:

```text
complexidade precisa pagar aluguel
```

Antes de introduzir abstração, camada, interface, dependência, mensageria, CQRS, Event Sourcing, microserviço, runtime sofisticado ou automação externa, o sistema deve responder:

- qual dor real isso resolve;
- qual alternativa simples foi considerada;
- qual custo cognitivo adiciona;
- qual custo operacional adiciona;
- qual risco reduz;
- qual risco cria;
- quando deve ser revisitado.

---

## Postura sobre MCP

MCP começa como read-only.

Uso legítimo:

- ler GitHub Projects;
- ler issues e PRs;
- consultar documentação externa;
- inspecionar cloud metadata;
- consultar observabilidade;
- reduzir incerteza factual.

Uso proibido por padrão:

- mover cards;
- fechar issues;
- comentar em PRs;
- alterar cloud;
- disparar workflows;
- fazer deploy;
- reiniciar recursos;
- manipular segredos;
- tocar produção.

MCP amplia visão.  
Não amplia autonomia sem governança.

---

## Critério de conclusão da Fase 1

A Fase 1 é considerada documentalmente concluída quando existem:

- estrutura canônica materializada;
- núcleo `core/` preenchido;
- skills iniciais implementadas;
- agents canônicos definidos;
- templates reutilizáveis criados;
- adapter OpenCode inicial documentado;
- policies de MCP, permissões e plugins definidas;
- raiz atualizada com estado real do projeto.

Esta versão cumpre esse critério e deve avançar para piloto controlado.

---

## Próximo passo

O próximo passo não é criar mais documentação.

O próximo passo é executar um piloto controlado em um workspace real, usando o harness para conduzir uma task concreta.

Objetivo do piloto:

- testar se o OpenCode consegue consumir as regras sem se perder;
- verificar se os commands são práticos;
- medir se os artifacts ajudam ou burocratizam;
- observar se o `PROJECT_STATE.md` fica útil;
- validar se MCP read-only ajuda;
- detectar slop, drift e excesso de contexto;
- ajustar a engenharia antes do hardening.

---

## Nota de maturidade

Esta versão é `0.2.0-alpha`.

Ela é suficientemente completa para piloto, mas ainda não deve ser tratada como v1 madura. A v1 só deve ser congelada depois de uso real, revisão crítica, corte de excessos e hardening.