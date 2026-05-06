# OpenCode Command — plan

## Finalidade

Este comando orienta o OpenCode a transformar uma demanda, issue, board item ou Implementation Packet em um Execution Plan.

O comando `plan` não implementa.  
Ele prepara a execução.

---

## Agente responsável

```text
adapters/opencode/agents/planner.md
```

Contrato canônico:

```text
agents/planner.md
```

---

## Quando usar

Use este comando quando:

- a task for R1+;
- houver mutação local;
- houver múltiplos caminhos possíveis;
- a demanda ainda precisar ser estruturada;
- uma issue precisar virar plano executável;
- houver risco de over-engineering;
- houver impacto em arquitetura, banco, cloud, segurança, CI/CD ou integração.

---

## Quando não usar

Não use este comando quando:

- a task for apenas investigação R0;
- já existir Execution Plan aprovado e ainda válido;
- a demanda estiver vaga demais e exigir intake antes;
- a decisão depender do Core Architect antes de qualquer plano.

---

## Inputs esperados

O comando pode receber:

```text
- pedido humano;
- issue;
- board item;
- Implementation Packet;
- Investigation Note;
- contexto de workspace;
- decisão do Core Architect;
- referência a arquivos ou módulos.
```

---

## Fontes que devem ser consultadas

Antes de planejar, consultar quando existirem:

```text
WORKSPACE_GUIDE.md
PROJECT_CONTEXT.md
AUTHORITY_SOURCES.md
LOCAL_COMMANDS.md
PROJECT_STATE.md
RISK_SURFACES.md
DONE_CRITERIA.md
OPERATIONAL_REALITY.md
GITHUB_PROJECTS_CONTEXT.md
README.md
ADRs
```

Fontes globais relevantes:

```text
core/protocols/00-implementation-flow.md
core/protocols/01-repository-discovery.md
core/protocols/02-authority-sources.md
core/taxonomy/04-risk-to-artifacts-matrix.md
templates/packets/Execution_Plan.template.md
templates/checklists/Plan_Review.checklist.md
```

---

## Skills prováveis

Acionar conforme necessidade:

```text
skills/orchestration/implementation-planner/SKILL.md
skills/orchestration/risk-classifier/SKILL.md
skills/orchestration/task-decomposer/SKILL.md
skills/engineering/repository-discovery-operator/SKILL.md
skills/engineering/architecture-by-pain-check/SKILL.md
skills/engineering/product-impact-lens/SKILL.md
```

Skills específicas de stack, platform ou security devem ser acionadas quando o plano tocar essas áreas.

---

## Processo

### 1. Consolidar demanda

Identificar:

- objetivo;
- contexto;
- critério de aceite;
- dentro do escopo;
- fora do escopo;
- dúvidas abertas.

### 2. Fazer discovery proporcional

Descobrir apenas o necessário para planejar:

- topologia relevante;
- arquivos prováveis;
- comandos locais;
- testes;
- boundaries;
- riscos;
- authority sources.

### 3. Classificar risco

Usar:

```text
R0 — leitura/investigação sem mutação
R1 — mudança local pequena e reversível
R2 — mudança funcional relevante
R3 — mudança estrutural, sensível ou sistêmica
R4 — produção, segredo, irreversibilidade ou alto risco
```

Quando houver dúvida, escolher a classe mais conservadora.

### 4. Definir abordagem

A abordagem deve ser:

- simples;
- proporcional;
- verificável;
- alinhada ao workspace;
- livre de abstração sem dor real.

### 5. Definir validação

Usar comandos de `LOCAL_COMMANDS.md` quando existirem.

Não inventar comando local como se fosse autoridade.

### 6. Definir escalonamento

Registrar sinais que exigem pausa:

- risco R3/R4;
- produção;
- segredo;
- dado real;
- decisão arquitetural;
- dependência nova;
- conflito entre authority sources;
- validação essencial indisponível.

---

## Output obrigatório

Produzir um `Execution Plan` usando:

```text
templates/packets/Execution_Plan.template.md
```

O output deve conter, no mínimo:

```text
Objetivo
Contexto
Classe de risco
Discovery realizado
Authority sources consultadas
Escopo
Fora do escopo
Abordagem
Etapas
Validação planejada
Skills acionadas
Riscos e mitigação
Sinais de escalonamento
Artifact de saída esperado
```

---

## Prompt operacional sugerido

```text
Use o comando plan.

Transforme a demanda abaixo em um Execution Plan usando o harness.

Demanda:
<colar demanda>

Contexto adicional:
<colar contexto, issue, board item ou Implementation Packet>

Regras:
- Não implemente.
- Consulte authority sources locais quando existirem.
- Faça discovery proporcional.
- Classifique risco.
- Evite over-engineering.
- Defina validações.
- Registre sinais de escalonamento.
- Use templates/packets/Execution_Plan.template.md como formato.
```

---

## Critério de sucesso

O comando foi bem-sucedido quando existe um Execution Plan:

- claro;
- executável;
- proporcional ao risco;
- com escopo definido;
- com validação planejada;
- com riscos declarados;
- com sinais de escalonamento explícitos.

---

## Anti-patterns

Evitar:

- plano genérico;
- plano sem arquivos/áreas prováveis;
- plano sem validação;
- plano que já implementa;
- plano que ignora `LOCAL_COMMANDS.md`;
- plano que usa board como verdade técnica;
- plano que introduz arquitetura sem dor real.