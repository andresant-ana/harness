# Workspace Guide

## Finalidade

Este documento é o guia local do workspace.

Ele explica como este projeto deve ser entendido, operado e evoluído por humano, Core Architect e agentes usando o harness.

Este arquivo não substitui o `README.md` público do projeto.  
Ele é uma authority source operacional interna para execução assistida por agentes.

---

## Identidade do projeto

### Nome

`<nome-do-projeto>`

### Descrição curta

`<descrição objetiva do que o projeto faz>`

### Tipo de projeto

`<API | frontend | fullstack | worker | biblioteca | monólito modular | serviço | outro>`

### Stack principal

```text
Backend:
Frontend:
Banco:
Cloud:
Runtime:
IaC:
CI/CD:
```

---

## Objetivo do workspace

Este workspace existe para:

- `<objetivo 1>`;
- `<objetivo 2>`;
- `<objetivo 3>`.

---

## Fontes locais de autoridade

Antes de planejar ou implementar, consultar:

- `PROJECT_CONTEXT.md`;
- `AUTHORITY_SOURCES.md`;
- `LOCAL_COMMANDS.md`;
- `PROJECT_STATE.md`;
- `DONE_CRITERIA.md`;
- `OPERATIONAL_REALITY.md`;
- `RISK_SURFACES.md`;
- ADRs, se existirem;
- documentação de módulo, se existir.

Se houver conflito entre conversa antiga e arquivo local, o arquivo local vence até revisão explícita.

---

## Como agentes devem trabalhar neste workspace

### Ordem padrão

```text
1. Ler este WORKSPACE_GUIDE.md
2. Ler PROJECT_CONTEXT.md
3. Ler AUTHORITY_SOURCES.md
4. Ler LOCAL_COMMANDS.md
5. Ler PROJECT_STATE.md
6. Fazer repository discovery proporcional
7. Produzir Execution Plan antes de mutação R1+
8. Executar dentro do escopo aprovado
9. Validar com comandos locais
10. Produzir Completion Packet
11. Propor Project State Entry quando houver mudança durável
```

---

## Regras locais de execução

- Não inventar comandos.
- Não ignorar authority sources.
- Não expandir escopo sem escalonamento.
- Não adicionar dependência sem justificar dor real.
- Não alterar arquitetura sem plano e aprovação.
- Não tocar produção.
- Não manipular segredo real.
- Não usar board como fonte técnica principal.
- Não registrar ruído em `PROJECT_STATE.md`.

---

## Estrutura esperada do repositório

```text
<descrever estrutura local relevante>
```

Exemplo:

```text
src/
tests/
docs/
infra/
.github/
```

---

## Convenções locais

### Nomeação

`<convenções de nomes relevantes>`

### Organização de arquivos

`<como módulos/features/camadas são organizados>`

### Testes

`<onde ficam, como nomear, como rodar>`

### Commits

`<padrão de mensagem, branch, PR, etc>`

### Documentação

`<onde documentar decisões, comandos, estado e ADRs>`

---

## Arquitetura local

Resumo curto da arquitetura atual:

```text
<arquitetura local, sem transformar este guia em ADR detalhado>
```

Boundaries importantes:

- `<boundary 1>`;
- `<boundary 2>`;
- `<boundary 3>`.

---

## Relação com GitHub Projects

GitHub Projects ou board pode ser usado para entender:

- prioridade;
- status;
- issue relacionada;
- sequencing;
- dependências de trabalho.

Mas não deve ser usado como substituto de:

- código;
- `PROJECT_STATE.md`;
- ADRs;
- `AUTHORITY_SOURCES.md`;
- `OPERATIONAL_REALITY.md`.

---

## Política de PROJECT_STATE

`PROJECT_STATE.md` deve registrar apenas memória técnica durável:

- decisões;
- riscos;
- limitações;
- estado arquitetural;
- operational reality;
- comandos relevantes;
- integrações;
- dívidas conscientes;
- follow-ups estruturais.

Não registrar:

- histórico granular de tasks;
- backlog;
- diário de sessão;
- comentários efêmeros;
- conteúdo inteiro de Completion Packet.

---

## Critério de pronto local

Consultar `DONE_CRITERIA.md`.

Nenhuma task relevante deve ser considerada finalizada sem:

- validação proporcional;
- diff revisável;
- riscos declarados;
- lacunas registradas;
- handoff claro;
- state update considerado.

---

## Comandos principais

Consultar `LOCAL_COMMANDS.md`.

Comandos neste projeto devem vir de authority source local, não de suposição genérica da stack.

---

## Riscos conhecidos

Consultar `RISK_SURFACES.md`.

Resumo rápido:

- `<risco 1>`;
- `<risco 2>`;
- `<risco 3>`.

---

## Operational reality

Consultar `OPERATIONAL_REALITY.md`.

Resumo rápido:

```text
Ambiente local:
Ambiente remoto:
Deploy:
Observabilidade:
Banco:
Segredos:
Limitações:
```

---

## Última atualização

```text
Data:
Autor:
Motivo:
```