# Skill — .NET Performance Baseline

## Finalidade

Esta skill orienta revisão de performance específica para aplicações .NET/C#, cobrindo async/await, alocação, GC, LINQ, EF Core, pooling, hot paths, throughput, concorrência e uso de recursos.

Seu papel é impedir que o agente escreva código C# funcional, mas ineficiente, bloqueante, alocador demais, ruim sob carga ou problemático para runtime.

---

## Quando usar

Use esta skill quando a task tocar:

- endpoint de alto uso;
- hot path;
- processamento de coleção;
- query EF Core;
- async/await;
- chamadas externas;
- jobs;
- workers;
- loops;
- serialização;
- uso de memória;
- cache;
- pooling;
- streaming;
- upload/download;
- operação com volume;
- performance reportada;
- GC pressure;
- throughput/latência.

---

## Quando não usar

Não use esta skill quando:

- a mudança é trivial;
- não há impacto de runtime;
- a task é puramente documental;
- performance já foi analisada em skill transversal suficiente.

---

## Tese central

.NET performa bem quando o código respeita o runtime.

O problema geralmente não é “C# é lento”.  
O problema costuma ser:

- async mal usado;
- I/O bloqueante;
- LINQ gerando trabalho excessivo;
- EF Core fazendo query ruim;
- alocação desnecessária;
- cache sem limite;
- pooling ignorado;
- coleção grande carregada em memória;
- concorrência sem controle.

---

## Método

### 1. Identificar caminho de execução

Mapear:

- endpoint;
- service;
- handler;
- job;
- worker;
- query;
- loop;
- chamada externa;
- serialização;
- operação de I/O.

---

### 2. Revisar async/await

Verificar:

- I/O assíncrono usa async corretamente?
- há `.Result` ou `.Wait()`?
- há blocking call em caminho async?
- cancellation token é propagado quando aplicável?
- tasks são aguardadas?
- há fire-and-forget sem controle?
- paralelismo tem limite?

---

### 3. Revisar EF Core/LINQ

Perguntar:

- query executa no banco ou em memória?
- há `ToList()` cedo demais?
- há N+1?
- há `Include` excessivo?
- há projection para DTO?
- há paginação?
- leitura usa `AsNoTracking` quando aplicável?
- filtros são aplicados antes da materialização?

---

### 4. Revisar alocação e memória

Verificar:

- criação excessiva de objetos em loop;
- strings concatenadas em hot path;
- buffers grandes;
- coleções sem limite;
- cache sem expiração/tamanho;
- stream lido inteiro sem necessidade;
- serialização pesada.

---

### 5. Revisar pooling e recursos

Avaliar:

- `HttpClient`/factory;
- DbContext lifetime;
- connection pool;
- memory streams;
- disposal;
- timers;
- background services;
- scoped services usados fora de escopo.

---

### 6. Revisar concorrência

Perguntar:

- há lock?
- há estado compartilhado?
- há paralelismo sem throttle?
- há race condition?
- há saturação de thread pool?
- há retry storm?
- há uso indevido de singleton?

---

### 7. Validar proporcionalmente

Possíveis validações:

- testes;
- benchmark pequeno;
- profiling;
- logs de query;
- generated SQL;
- métricas;
- análise de alocação;
- teste de carga leve;
- revisão de plano de execução.

---

## Output esperado

```md
# .NET Performance Baseline Review

## Caminho analisado
<endpoint, job, service, query ou hot path>

## Pressão principal
<CPU | memória | GC | I/O | banco | rede | thread pool | outro>

## Async/await
<suficiente | risco | não aplicável>

## EF Core/LINQ
<suficiente | risco | não aplicável>

## Alocação/memória
<suficiente | risco | incerto>

## Pooling/recursos
<suficiente | risco | incerto>

## Concorrência
<suficiente | risco | não aplicável>

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

Antes de aceitar, verificar:

- há `.Result` ou `.Wait()`?
- há `ToList()` antes da hora?
- há N+1?
- há `Include` excessivo?
- há paginação onde precisa?
- há `AsNoTracking` em leitura?
- há projection adequada?
- há cache sem limite?
- há stream carregado inteiro sem necessidade?
- há paralelismo sem throttle?
- cancellation token é considerado?
- recursos descartáveis são tratados corretamente?

---

## Critérios de escalonamento

Escalar quando:

- hot path crítico tiver risco de degradação;
- query crítica tiver cardinalidade desconhecida;
- houver suspeita de memory leak;
- houver OOM, GC pressure ou thread starvation;
- solução exigir cache, fila, streaming ou arquitetura nova;
- houver trade-off entre latência, throughput e consistência;
- a validação necessária exigir ambiente específico.

---

## Anti-patterns

Evitar:

- otimizar sem dor, mas ignorar gargalo óbvio;
- bloquear async com `.Result`;
- criar task fire-and-forget em request;
- carregar tudo em memória;
- query EF dentro de loop;
- `Include` para resolver tudo;
- usar cache sem invalidação;
- usar singleton com estado mutável;
- aumentar recurso cloud para mascarar código ruim;
- aceitar banco vazio/local como prova de performance.

---

## Declaração operacional curta

Performance .NET boa nasce de respeito ao runtime: async correto, queries bem moldadas, memória controlada e concorrência consciente.