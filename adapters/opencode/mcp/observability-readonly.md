# OpenCode MCP — Observability Read-Only Inspection

## Finalidade

Este arquivo orienta o uso de MCP para leitura read-only de logs, métricas, traces, dashboards, health signals e alertas no OpenCode.

Observabilidade deve responder hipóteses operacionais específicas.

Ela não deve ser usada para despejar logs brutos no contexto.

---

## Modo permitido

```text
read-only
```

Operações permitidas:

```text
ler logs filtrados
ler métricas
ler traces
ler dashboards
ler alertas
consultar health signals
consultar janela de tempo limitada
resumir evidência
```

Operações proibidas sem autorização explícita:

```text
alterar dashboard
alterar alerta
silenciar alerta
criar alerta
deletar alerta
alterar retenção
alterar configuração de observabilidade
reiniciar serviço
fazer deploy
alterar recurso cloud
```

---

## Agente responsável

```text
adapters/opencode/agents/mcp-observer.md
```

Skills relacionadas:

```text
skills/integration/observability-readonly-inspection/SKILL.md
skills/security/secrets-and-config-hygiene/SKILL.md
skills/engineering/failure-mode-and-reliability-review/SKILL.md
skills/engineering/performance-and-capacity-review/SKILL.md
skills/engineering/runtime-resource-diagnostics/SKILL.md
```

---

## Quando usar

Use quando a task precisar investigar:

- erro em runtime;
- falha intermitente;
- degradação;
- timeout;
- 5xx;
- latência;
- job falhando;
- fila travada;
- memory/CPU pressure;
- falha de startup;
- incidente passado;
- health check;
- comportamento em staging/produção.

---

## Quando não usar

Não use quando:

- não houver pergunta diagnóstica;
- logs não forem necessários;
- a fonte contém dados sensíveis não filtráveis;
- a investigação pode ser feita localmente com menor risco;
- a leitura geraria contexto bruto demais;
- a próxima ação exigiria alteração operacional.

---

## Pergunta obrigatória antes da consulta

Antes de consultar observabilidade, declarar:

```text
Qual sintoma estamos investigando?
Qual serviço/recurso?
Qual ambiente?
Qual janela de tempo?
Qual hipótese queremos confirmar ou refutar?
```

Sem hipótese ou pergunta, não abrir logs.

---

## Escopo mínimo

Filtrar por:

```text
ambiente
serviço
janela de tempo
endpoint
status code
correlation id
request id
severity
operação
recurso
```

Evitar:

```text
logs amplos
janelas longas sem motivo
copiar payload inteiro
copiar stack trace extenso
consultas sem filtro
```

---

## Proteção de dados

Não reproduzir:

```text
payload sensível
token
header Authorization
cookie
dados pessoais desnecessários
secret
connection string
stack trace com segredo
```

Mascarar quando necessário:

```text
<redacted>
<masked>
<sensitive-payload-omitted>
```

---

## Separação entre sinal e conclusão

Classificar achados como:

```text
fato observado
padrão recorrente
anomalia
hipótese confirmada
hipótese refutada
lacuna
falso positivo possível
```

Não concluir causa raiz por um único log isolado sem evidência suficiente.

---

## Processo

### 1. Definir hipótese

Exemplo:

```text
O endpoint X está retornando 500 por falha de conexão com o banco entre 10:00 e 10:30.
```

### 2. Consultar sinais mínimos

Buscar apenas os sinais necessários:

```text
logs filtrados
métrica de erro
métrica de latência
trace de request
alerta relacionado
```

### 3. Conectar achado a ação

Cada achado deve indicar se:

```text
confirma hipótese
refuta hipótese
exige investigação adicional
sugere bug
sugere falha operacional
exige escalonamento
```

### 4. Registrar limitações

Se a observabilidade for insuficiente, declarar.

---

## Output recomendado

```md
# Observability Read-Only Inspection Note

## Sintoma ou pergunta
<o que está sendo investigado>

## Ambiente e janela
<ambiente, período, serviço>

## Fontes consultadas
- <logs>
- <métricas>
- <traces>
- <alertas>

## Achados
- <achado 1>
- <achado 2>

## Hipóteses confirmadas/refutadas
- <hipótese 1>
- <hipótese 2>

## Dados sensíveis
<não acessados | mascarados | risco identificado>

## Implicação para a task
<próximo passo técnico>

## Veredito
<suficiente | investigar mais | escalar>
```

---

## Escalonamento

Escalar quando:

- ambiente for produção;
- houver incidente ativo;
- logs contiverem dados sensíveis;
- sinal indicar falha crítica;
- ação corretiva exigir deploy, restart, config ou rollback;
- houver suspeita de segurança;
- evidência for inconclusiva e risco alto;
- observabilidade revelar indisponibilidade real.

---

## Anti-patterns

Evitar:

- abrir logs sem hipótese;
- copiar logs extensos;
- reproduzir payload sensível;
- alterar alerta durante investigação;
- concluir causa por um único log;
- ignorar janela de tempo;
- confundir correlação com causalidade;
- usar observabilidade para justificar chute.

---

## Declaração operacional curta

Observabilidade read-only transforma sinais em evidência.  
O OpenCode deve ler pouco, filtrar bem, proteger dados e conectar achados a decisão.