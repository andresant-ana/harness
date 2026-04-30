# Skill — Performance and Capacity Review

## Finalidade

Esta skill orienta a revisão de performance, capacidade e custo operacional de uma mudança.

Seu papel é impedir que o agente entregue código funcional no caminho feliz, mas ruim sob carga, caro em recursos, ineficiente em banco, pesado em memória ou incapaz de escalar de forma previsível.

---

## Quando usar

Use esta skill quando a task tocar:

- endpoint de alto uso;
- query relevante;
- listagem, busca, relatório ou paginação;
- processamento em lote;
- fluxo crítico;
- integração externa;
- cache;
- fila;
- job;
- concorrência;
- uso de memória;
- CPU;
- I/O;
- pool de conexões;
- hot path;
- comportamento sob carga;
- N+1;
- throughput ou latência.

---

## Quando não usar

Não use esta skill quando:

- a mudança for trivial e sem impacto de runtime;
- a task for puramente documental;
- a performance não for relevante para a área tocada;
- a aplicação da skill só adicionaria análise especulativa.

---

## Tese central

Performance não é otimização prematura.  
Performance é entender se a solução respeita a capacidade esperada do sistema.

A pergunta correta não é:

“isso está super otimizado?”

A pergunta correta é:

“isso tem custo compatível com o uso esperado e não cria gargalo óbvio?”

---

## Método

### 1. Identificar o caminho de execução

Mapear:

- quem chama;
- com que frequência;
- qual volume esperado;
- que dependências toca;
- que banco, API, fila ou recurso usa;
- se é caminho crítico ou marginal.

---

### 2. Identificar recurso pressionado

Classificar o possível gargalo:

- CPU;
- memória;
- heap/GC;
- banco;
- rede;
- disco;
- fila;
- lock;
- pool de conexão;
- API externa;
- cold start;
- serialização;
- renderização.

---

### 3. Avaliar cardinalidade

Perguntar:

- quantos registros podem ser processados?
- a query tem paginação?
- existe loop chamando banco?
- existe loop chamando API externa?
- há risco de carregar coleção grande em memória?
- há risco de operação O(n²) em volume real?

---

### 4. Avaliar banco e I/O

Verificar:

- N+1;
- joins desnecessários;
- falta de filtro;
- paginação ausente;
- índice necessário;
- transação longa;
- escrita em massa;
- leitura repetida;
- round-trips excessivos.

---

### 5. Avaliar memória e alocação

Perguntar:

- há objetos grandes em memória?
- há buffering desnecessário?
- há leitura total onde streaming bastaria?
- há cache sem limite?
- há risco de vazamento?
- há pressão de GC?

---

### 6. Avaliar concorrência e throughput

Verificar:

- uso correto de async;
- bloqueio síncrono em caminho assíncrono;
- locks;
- paralelismo sem limite;
- saturação de pool;
- retry storm;
- fan-out descontrolado.

---

### 7. Definir validação proporcional

Quando aplicável, recomendar:

- teste de unidade para comportamento;
- teste de integração para query;
- análise de plano de execução;
- profiling;
- medição simples local;
- benchmark controlado;
- teste de carga leve;
- métrica ou log operacional.

---

## Output esperado

```md
# Performance and Capacity Review

## Caminho analisado
<endpoint, job, fluxo, query ou operação>

## Pressão principal
<CPU | memória | banco | rede | I/O | pool | API externa | outro>

## Riscos identificados
- <risco 1>
- <risco 2>

## Cardinalidade esperada
<volume, frequência, tamanho de coleção ou incerteza>

## Pontos de atenção
- <N+1, paginação, cache, lock, pool, GC, etc>

## Validação recomendada
- <validação 1>
- <validação 2>

## Veredito
<suficiente | ajustar | medir | escalar>

## Risco residual
<risco que permanece>
```

---

## Checklist de qualidade

Antes de aceitar a mudança, verificar:

- há risco de N+1?
- há paginação onde precisa?
- há carregamento excessivo em memória?
- há loop com I/O externo?
- há retry sem limite?
- há paralelismo descontrolado?
- há saturação provável de pool?
- há operação síncrona bloqueando caminho assíncrono?
- há métrica ou sinal para observar degradação?
- a validação é proporcional ao risco?

---

## Critérios de escalonamento

Escalar quando:

- o fluxo for crítico e sem evidência de capacidade;
- houver risco de queda sob carga;
- a mudança tocar arquitetura de cache;
- a solução exigir fila, particionamento, streaming ou mudança estrutural;
- houver risco de custo cloud relevante;
- houver trade-off entre consistência, latência e throughput;
- a validação necessária não puder ser feita no contexto atual.

---

## Anti-patterns

Evitar:

- otimizar sem dor real;
- ignorar N+1;
- carregar tudo em memória;
- paginação só no frontend;
- cache sem invalidação;
- paralelismo sem limite;
- retry agressivo;
- benchmark artificial como prova absoluta;
- aceitar “funciona local” como evidência de capacidade.

---

## Declaração operacional curta

Performance review não busca perfeição.  
Busca evitar gargalos óbvios, custo desproporcional e fragilidade sob uso real.