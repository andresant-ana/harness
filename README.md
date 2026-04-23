# Harness Engineering

Repositório canônico da engenharia de harness e agentes.

Este repositório é a **fonte única de verdade** da engenharia global aplicada ao runtime OpenCode. Sua função é materializar, versionar e governar a arquitetura canônica do sistema antes da sua tradução para qualquer runtime específico.

O objetivo desta engenharia é transformar o coding agent em um executor disciplinado, verificável, econômico em contexto, seguro por desenho e subordinado a uma camada estratégica humana. Em vez de depender de prompts soltos e comportamento oportunista do modelo, o sistema organiza missão, princípios, leis operacionais, classes de risco, protocolos, políticas, artifacts, skills, agents, templates e governança.

## O que este repositório é

Este repositório é:

- a arquitetura canônica do harness;
- o núcleo documental e operacional da engenharia;
- o lugar onde a doutrina do sistema é escrita e evoluída;
- a base a partir da qual o adapter do OpenCode será implementado.

## O que este repositório não é

Este repositório não é:

- um projeto de produto;
- um workspace específico de aplicação;
- um repositório de código de negócio;
- um conjunto de prompts avulsos para uso imediato no runtime;
- uma configuração viva do OpenCode pronta desde o primeiro dia.

A engenharia nasce aqui primeiro como **sistema governável**. Só depois ela é traduzida para o runtime.

## Estado atual

Status atual do programa:

- Fase 1 iniciada: arquitetura canônica materializada
- Primeira onda documental em andamento
- Núcleo da `constitution/` sendo escrito
- Adapter do OpenCode ainda não iniciado
- Skills ainda não implementadas
- Templates ainda não materializados

## Princípio central

O agente não substitui a camada estratégica.

A camada estratégica continua sendo responsabilidade do humano e do Core Architect. O harness existe para fazer a camada executora operar com disciplina, previsibilidade, evidência, controle de risco e controle de entropia.

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

## Lógica de organização

### `core/`

Contém o firmware do sistema: missão, princípios, leis, classes de risco, protocolos, políticas, artifacts, taxonomia, observabilidade e governança.

### `skills/`

Contém capacidades acionáveis sob demanda, organizadas por família.

### `agents/`

Contém os contratos canônicos dos agentes globais, independentes do runtime.

### `adapters/`

Contém a tradução do sistema canônico para o runtime concreto. O primeiro adapter será o OpenCode.

### `templates/`

Contém moldes reutilizáveis para bootstrap de projetos, packets, ADRs e checklists.

## Ordem correta de construção

A ordem deliberada da engenharia é:

1. materializar a arquitetura canônica;
2. escrever a constituição do sistema;
3. escrever protocolos e políticas;
4. definir artifacts e taxonomias;
5. implementar skills prioritárias;
6. definir contratos canônicos de agents;
7. criar templates de workspace;
8. traduzir tudo para o adapter OpenCode;
9. instrumentar, pilotar e endurecer.

## Regra de integridade

Tudo que for:

* recorrente,
* global,
* durável,
* independente de projeto

deve viver no harness.

Tudo que for:

* específico de um projeto,
* verdadeiro apenas para um repositório,
* dependente do domínio de negócio,
* ligado a comandos, riscos e arquitetura locais

deve viver no workspace do projeto, não aqui.

## Critério de progresso

Esta primeira etapa só será considerada sólida quando existirem:

* arquivos fundadores da raiz preenchidos;
* constituição inicial documentada;
* fronteira clara entre humano, Core Architect e executor;
* classes de risco formalizadas;
* política de autonomia e escalonamento escrita.

## Nota de implementação

A criação desta engenharia não deve ser confundida com “começar a usar o agent”. Primeiro o sistema precisa existir como arquitetura. Só depois ele passa a operar como runtime.

Este repositório é o começo desse processo.
