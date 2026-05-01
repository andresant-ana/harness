# Skill — Observability Read-Only Inspection

## Finalidade

Esta skill orienta a leitura read-only de logs, métricas, traces, dashboards, health signals e alertas.

Seu papel é permitir diagnóstico baseado em evidência sem vazar dados sensíveis, sem alterar observabilidade e sem transformar logs brutos em contexto descontrolado.

---

## Quando usar

Use esta skill quando a task precisar investigar:

- erro em runtime;
- falha intermitente;
- degradação;
- timeout;
- latência;
- 5xx;
- comportamento em produção/staging;
- fila travada;
- job falhando;
- memory/CPU pressure;
- traces distribuídos;
- health check;
- alerta;
- incidente passado.

---

## Quando não usar

Não use esta skill quando:

- não há pergunta diagnóstica;
- logs não são necessários;
- a fonte contém dados sensíveis não filtráveis;
- a operação exigiria alterar alerta/dashboard;
- a investigação pode ser feita localmente com menor risco;
- a leitura geraria contexto bruto demais.

---

## Tese central

Observabilidade serve para responder hipótese, não para despejar logs.

Boa inspeção observa sinais mínimos suficientes para confirmar, refutar ou refinar uma hipótese operacional.

---

## Método

### 1. Definir hipótese ou pergunta

Antes de consultar observabilidade, declarar:

- qual sintoma estamos investigando;
- qual janela de tempo;
- qual serviço/recurso;
- qual métrica/log/trace pode ajudar;
- que evidência mudaria a decisão.

---

### 2. Restringir escopo

Filtrar por:

- serviço;
- ambiente;
- período;
- correlation id;
- request id;
- status code;
- endpoint;
- operação;
- severity;
- usuário mascarado, se aplicável.

Evitar logs amplos.

---

### 3. Proteger dados sensíveis

Não reproduzir:

- payload sensível;
- token;
- header Authorization;
- cookie;
- dado pessoal desnecessário;
- segredo;
- connection string;
- stack trace com segredo.

Mascarar quando necessário.

---

### 4. Separar sinal de ruído

Classificar achados:

- fato observado;
- padrão recorrente;
- anomalia;
- hipótese;
- lacuna;
- falso positivo possível.

---

### 5. Conectar com ação

Cada achado deve indicar:

- confirmar hipótese;
- refutar hipótese;
- exigir investigação adicional;
- sugerir bug;
- sugerir falha de dependência;
- sugerir problema operacional;
- exigir escalonamento.

---

## Output esperado

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

## Checklist de qualidade

Antes de concluir, verificar:

- havia pergunta diagnóstica?
- janela de tempo foi limitada?
- serviço/recurso foi limitado?
- dados sensíveis foram evitados?
- achados são fatos observados?
- hipótese foi separada de conclusão?
- logs brutos não foram despejados?
- a inspeção sugere próximo passo claro?
- nenhuma alteração em dashboard/alerta foi feita?

---

## Critérios de escalonamento

Escalar quando:

- ambiente for produção;
- houver incidente ativo;
- logs contiverem dados sensíveis;
- sinal indicar falha crítica;
- ação corretiva exigiria deploy, restart, config ou rollback;
- houver suspeita de segurança;
- evidência for inconclusiva e risco alto.

---

## Anti-patterns

Evitar:

- abrir logs sem hipótese;
- copiar logs extensos;
- reproduzir payload sensível;
- alterar alerta durante investigação read-only;
- concluir causa por um único log isolado;
- ignorar janela de tempo;
- confundir correlação com causalidade;
- usar observabilidade para justificar chute.

---

## Declaração operacional curta

Observabilidade read-only transforma sinais em evidência.  
O harness lê pouco, filtra bem, protege dados e conecta achados a decisão.