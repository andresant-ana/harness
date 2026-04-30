# Taxonomia de Capacidades por Stack

## Finalidade

Este documento classifica as capacidades globais reconhecidas pelo harness para a stack principal.

Ele não ensina a stack inteira.  
Ele define quais áreas recorrentes merecem skills, critérios de review e guardrails próprios.

---

## Tese central

Stack não é identidade do harness.  
Stack é superfície recorrente de trabalho.

O harness deve ser capaz de operar bem na stack principal sem virar documentação enciclopédica de ferramenta.

As capacidades por stack existem para:
- reduzir erros comuns;
- orientar validação;
- melhorar review;
- preservar segurança;
- evitar over-engineering;
- conectar implementação com produção.

---

## Stack principal reconhecida

```text
Backend: C# / .NET
Frontend: React
Banco relacional: PostgreSQL
Cloud: Azure
```

---

## `.NET / C#`

### Diretório

```text
skills/stack/dotnet/
├─ dotnet-solution-ops/
├─ aspnet-endpoint-review/
├─ efcore-migrations-safety/
└─ dotnet-performance-baseline/
```

### Capacidades reconhecidas

#### `dotnet-solution-ops`

Cobre:
- leitura de solution;
- organização de projects;
- build/test;
- referências entre projetos;
- comandos locais;
- estrutura de backend.

Usar quando:
- a task toca solution;
- há erro de build;
- há mudança entre projects;
- é preciso entender a estrutura .NET local.

#### `aspnet-endpoint-review`

Cobre:
- endpoints;
- controllers/minimal APIs;
- validação;
- contratos HTTP;
- status codes;
- auth;
- error handling;
- boundaries de API.

Usar quando:
- a task cria ou altera endpoint;
- há contrato HTTP;
- há risco de input, auth ou response inconsistente.

#### `efcore-migrations-safety`

Cobre:
- migrations;
- schema changes;
- tracking;
- queries;
- impacto de banco;
- validação de migração;
- risco de dados.

Usar quando:
- a task altera entidade persistida;
- cria migration;
- muda relacionamento;
- toca query relevante.

#### `dotnet-performance-baseline`

Cobre:
- async/await;
- alocação;
- GC;
- pooling;
- concorrência;
- throughput;
- hot paths;
- N+1;
- uso indevido de LINQ/EF.

Usar quando:
- há impacto em performance;
- há risco de query ruim;
- há processamento relevante;
- há operação sob carga.

---

## React

### Diretório

```text
skills/stack/react/
├─ react-component-architecture/
└─ react-state-and-boundary-review/
```

### Capacidades reconhecidas

#### `react-component-architecture`

Cobre:
- composição de componentes;
- separação de responsabilidade;
- props;
- reuso;
- legibilidade;
- boundaries de UI;
- prevenção de componente gigante.

Usar quando:
- a task cria ou altera componente relevante;
- há risco de duplicação;
- há estado visual complexo;
- há mudança em layout ou fluxo de UI.

#### `react-state-and-boundary-review`

Cobre:
- estado local vs global;
- efeitos;
- hooks;
- boundaries;
- data fetching;
- sincronização;
- renderização;
- propagação de estado.

Usar quando:
- há estado compartilhado;
- há efeitos colaterais;
- há bugs de renderização;
- há risco de acoplamento entre componentes.

---

## PostgreSQL

### Diretório

```text
skills/stack/postgres/
├─ postgres-schema-change-safety/
└─ postgres-query-review/
```

### Capacidades reconhecidas

#### `postgres-schema-change-safety`

Cobre:
- alteração de schema;
- índices;
- constraints;
- migrations;
- compatibilidade;
- risco de dados;
- rollback;
- impacto em produção.

Usar quando:
- a task altera tabela, coluna, índice ou constraint;
- há migration;
- há risco de lock, dado existente ou incompatibilidade.

#### `postgres-query-review`

Cobre:
- shape de query;
- filtros;
- joins;
- índices;
- N+1;
- paginação;
- transações;
- isolamento;
- custo de leitura e escrita.

Usar quando:
- a task cria ou altera query;
- há performance de banco;
- há risco de cardinalidade;
- há listagem, busca ou relatório.

---

## Azure

### Diretório

```text
skills/stack/azure/
├─ azure-delivery-reviewer/
└─ azure-execution-model-review/
```

### Capacidades reconhecidas

#### `azure-delivery-reviewer`

Cobre:
- deploy;
- configuração;
- pipeline;
- app settings;
- managed identity;
- observabilidade;
- ambiente;
- risco de publicação.

Usar quando:
- a task toca entrega;
- há config de cloud;
- há pipeline;
- há risco de ambiente.

#### `azure-execution-model-review`

Cobre:
- App Service;
- Container Apps;
- Functions;
- AKS;
- storage;
- filas;
- runtime;
- escala;
- custo;
- modelo operacional.

Usar quando:
- há escolha ou revisão de execution model;
- há discussão sobre container/serverless;
- há impacto em escala, custo ou operação.

---

## Capacidades transversais relacionadas

Além das skills de stack, algumas capacidades vivem em `engineering/`, `platform/` ou `security/` porque atravessam várias stacks:

- observabilidade;
- performance;
- concorrência;
- runtime diagnostics;
- failure modes;
- CI/CD;
- Docker;
- IaC;
- segurança;
- dependency review;
- state maintenance.

Essas capacidades não devem ser duplicadas em cada stack sem necessidade.

---

## Regra de uso

Use skill de stack quando o problema for específico de tecnologia.  
Use skill de engineering quando o problema for conceitual ou transversal.  
Use skill de platform quando o problema for ferramenta/runtime.  
Use skill de security quando houver superfície de risco.

---

## O que evitar

Evitar:

- transformar stack taxonomy em tutorial;
- criar skill para cada detalhe de framework;
- duplicar capacidade transversal em stack;
- assumir que tecnologia resolve arquitetura;
- usar stack como desculpa para over-engineering.

---

## Declaração operacional curta

Stack capabilities existem para melhorar execução recorrente na stack principal.  
Elas orientam prática, não substituem julgamento arquitetural.