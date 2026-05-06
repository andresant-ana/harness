# OpenCode Command — investigate

## Finalidade

Este comando orienta o OpenCode a investigar uma pergunta factual sem mutação.

O comando `investigate` reduz incerteza antes de plano, implementação, review ou escalonamento.

Ele não implementa.

---

## Agentes responsáveis

Primário:

```text
adapters/opencode/agents/researcher.md
```

Quando houver fonte externa/MCP:

```text
adapters/opencode/agents/mcp-observer.md
```

Contratos canônicos:

```text
agents/researcher.md
agents/mcp-observer.md
```

---

## Quando usar

Use este comando quando:

- a task for R0;
- houver dúvida factual;
- uma issue estiver vaga;
- houver bug sem causa conhecida;
- for necessário entender parte do repositório;
- docs externas precisarem ser verificadas;
- o comportamento de uma ferramenta/stack estiver incerto;
- for necessário consultar GitHub, board, cloud ou observabilidade em modo read-only.

---

## Quando não usar

Não use este comando quando:

- já houver evidência suficiente;
- a investigação seria curiosidade;
- a pergunta não estiver clara;
- a task já tiver Execution Plan aprovado;
- a próxima ação for mutação local controlada;
- a consulta externa exigiria escrita.

---

## Inputs esperados

```text
Pergunta investigada:
Contexto:
Arquivos/módulos suspeitos:
Issue/PR/board item:
Erro/log filtrado:
Ambiente:
Janela de tempo:
```

---

## Fontes que devem ser consultadas

Priorizar fontes locais:

```text
WORKSPACE_GUIDE.md
AUTHORITY_SOURCES.md
PROJECT_STATE.md
LOCAL_COMMANDS.md
OPERATIONAL_REALITY.md
README.md
ADRs
código e testes
```

Fontes externas, se necessário:

```text
GitHub read-only
GitHub Projects read-only
documentação oficial
cloud read-only
observabilidade read-only
```

---

## Skills prováveis

```text
skills/engineering/repository-discovery-operator/SKILL.md
skills/integration/docs-research-operator/SKILL.md
skills/integration/github-readonly-ops/SKILL.md
skills/integration/github-projects-readonly/SKILL.md
skills/integration/mcp-readonly-operator/SKILL.md
skills/integration/cloud-readonly-inspection/SKILL.md
skills/integration/observability-readonly-inspection/SKILL.md
skills/orchestration/stuck-recovery-playbook/SKILL.md
```

---

## Processo

### 1. Formular pergunta

Antes de investigar, declarar:

```text
O que precisamos descobrir?
Por que isso importa?
Que decisão depende disso?
Qual fonte pode responder?
```

### 2. Priorizar workspace

Consultar primeiro o que está no repositório e nos authority files.

### 3. Usar fonte externa apenas com pergunta clara

MCP, GitHub, cloud e observabilidade devem ser usados em modo read-only.

### 4. Separar fatos de hipóteses

Toda conclusão deve ser classificada como:

```text
fato confirmado
hipótese
lacuna
risco
```

### 5. Registrar impacto

A investigação deve dizer se o próximo passo é:

```text
Execution Plan
Escalation Note
Project State Entry
nova investigação
nenhuma ação
```

---

## Output obrigatório

Produzir `Investigation Note` usando:

```text
templates/packets/Investigation_Note.template.md
```

A saída deve conter:

```text
Pergunta investigada
Contexto
Escopo da investigação
Fontes consultadas
Fatos confirmados
Hipóteses
Lacunas
Riscos encontrados
Conclusão
Próximos passos recomendados
Necessita Execution Plan?
Necessita Escalation Note?
Necessita Project State Entry?
```

---

## Prompt operacional sugerido

```text
Use o comando investigate.

Investigue a pergunta abaixo sem fazer mutações.

Pergunta:
<colar pergunta>

Contexto:
<colar contexto, erro, issue, PR ou observação>

Regras:
- Não implemente.
- Não edite arquivos.
- Consulte primeiro fontes locais.
- Use MCP apenas em modo read-only.
- Separe fatos, hipóteses e lacunas.
- Não copie logs/documentos extensos sem síntese.
- Use templates/packets/Investigation_Note.template.md como formato.
```

---

## Critério de sucesso

O comando foi bem-sucedido quando:

- a pergunta foi respondida ou a lacuna ficou clara;
- fontes foram registradas;
- fatos e hipóteses foram separados;
- riscos foram declarados;
- o próximo passo ficou acionável.

---

## Anti-patterns

Evitar:

- investigar sem pergunta;
- ler o repositório inteiro sem hipótese;
- aceitar tutorial externo como autoridade;
- ignorar versão;
- tratar hipótese como fato;
- despejar contexto bruto;
- usar MCP para agir em vez de observar.