# Skill — Runtime Resource Diagnostics

## Finalidade

Esta skill orienta diagnóstico e revisão de uso de recursos em runtime: memória, CPU, heap, GC, conexões, threads, file handles, containers e comportamento de processo.

Seu papel é impedir que o agente trate runtime como caixa preta e ignore problemas que só aparecem em execução real.

---

## Quando usar

Use esta skill quando a task envolver:

- consumo alto de memória;
- vazamento de memória;
- CPU alta;
- lentidão;
- thread starvation;
- pool saturado;
- conexão vazando;
- processo reiniciando;
- container sendo morto;
- OOM;
- health check falhando;
- cold start;
- worker travado;
- GC pressure;
- arquivo, socket ou handle não liberado;
- comportamento diferente entre local e produção.

---

## Quando não usar

Não use esta skill quando:

- a task não toca runtime;
- não há sintoma de recurso;
- a mudança é puramente documental;
- o diagnóstico exigiria ambiente indisponível e não há evidência mínima.

---

## Tese central

Runtime revela verdades que o código isolado esconde.

Build verde e teste passando não provam que o sistema usa recursos bem.

A pergunta correta é:

“que recurso está sendo pressionado, por qual caminho e com que evidência?”

---

## Método

### 1. Identificar sintoma

Descrever:

- memória crescendo;
- CPU alta;
- latency spikes;
- restart loop;
- timeout;
- conexão saturada;
- erro de pool;
- OOM;
- degradação progressiva;
- deadlock aparente.

---

### 2. Identificar ambiente

Registrar:

- local;
- container;
- staging;
- produção;
- CI;
- serverless;
- worker;
- App Service;
- Kubernetes;
- outro runtime.

---

### 3. Identificar recurso suspeito

Classificar:

- heap;
- GC;
- CPU;
- thread pool;
- connection pool;
- database pool;
- socket;
- file handle;
- disk I/O;
- network I/O;
- container memory limit;
- startup time.

---

### 4. Formular hipótese

Exemplos:

- coleção crescendo sem limite;
- stream não descartado;
- HttpClient criado incorretamente;
- DbContext mal escopado;
- query carregando dados demais;
- retry gerando tempestade;
- lock causando espera;
- health check matando processo cedo demais;
- limite de container abaixo do necessário.

---

### 5. Definir evidência necessária

Possíveis evidências:

- logs;
- métricas;
- heap snapshot;
- profiler;
- dump;
- tracing;
- contadores runtime;
- plano de execução;
- métricas de container;
- métricas cloud;
- teste de carga leve.

---

### 6. Recomendar ação proporcional

Ação pode ser:

- investigar mais;
- corrigir uso de recurso;
- adicionar limite;
- ajustar pool;
- reduzir cardinalidade;
- adicionar streaming;
- corrigir disposal;
- ajustar health check;
- escalar para decisão operacional.

---

## Output esperado

```md
# Runtime Resource Diagnostics

## Sintoma
<descrição do comportamento observado>

## Ambiente
<local | container | cloud | CI | staging | produção | outro>

## Recurso suspeito
<memória | CPU | GC | pool | threads | I/O | container | outro>

## Hipóteses
- <hipótese 1>
- <hipótese 2>

## Evidência necessária
- <evidência 1>
- <evidência 2>

## Achados disponíveis
- <achado 1>
- <achado 2>

## Ação recomendada
<investigar | corrigir | medir | escalar>

## Risco residual
<risco que permanece>
```

---

## Checklist de qualidade

Antes de concluir diagnóstico, verificar:

- há sintoma claro?
- ambiente está identificado?
- recurso suspeito foi classificado?
- hipótese está separada de fato?
- há evidência?
- há risco de produção?
- há relação com container limits?
- há relação com health checks?
- há relação com pool ou conexão?
- a ação recomendada é proporcional?

---

## Critérios de escalonamento

Escalar quando:

- envolver produção;
- envolver OOM recorrente;
- envolver indisponibilidade;
- exigir alteração de runtime/cloud;
- exigir mudança de limite de container;
- exigir decisão de autoscaling;
- a evidência for insuficiente e o risco alto;
- houver suspeita de vazamento ou deadlock em fluxo crítico.

---

## Anti-patterns

Evitar:

- culpar infraestrutura antes de entender código;
- aumentar memória sem diagnóstico;
- usar autoscaling para esconder bug;
- ignorar GC;
- ignorar pool;
- ignorar disposal;
- tratar restart loop como problema aleatório;
- confundir readiness com liveness;
- concluir causa sem evidência.

---

## Declaração operacional curta

Diagnóstico de runtime começa por sintoma, recurso e evidência.  
Sem isso, ajuste de infraestrutura vira chute caro.