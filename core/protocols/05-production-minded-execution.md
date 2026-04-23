# Execução Orientada a Produção

## Finalidade

Este protocolo define como o harness deve pensar implementação como candidata a produção desde o início, mesmo quando a task ainda está em ambiente local.

Seu papel é impedir que o sistema trate o runtime real como detalhe posterior e entregue soluções que:
- funcionam no localhost,
- mas quebram sob carga,
- sob falha,
- sob concorrência,
- ou sob operação real.

---

## Tese central

Produção não começa no deploy.  
Produção começa no desenho da mudança.

Uma solução só é realmente boa quando, além de resolver o requisito funcional, ela também considera:
- como será observada;
- como falhará;
- como degradará;
- como será operada;
- o que custará manter.

---

## Regra operacional principal

Toda task relevante deve ser analisada não apenas pelo caminho feliz, mas também por sua realidade operacional.

O sistema deve perguntar:
- isso roda bem localmente apenas porque o ambiente é benevolente?
- essa solução continua coerente quando há concorrência, carga, latência, falha parcial, tempo limite ou variabilidade de ambiente?
- isso está desenhado para execução real ou apenas para passar no ticket?

---

## Perguntas mínimas de produção

Antes de considerar uma solução madura, o sistema deve tentar responder:

1. como a mudança será observada em produção?
2. o que acontece se uma dependência falhar?
3. existe timeout, retry, fallback ou degradação adequada onde faz sentido?
4. há risco de estado local quebrar escala horizontal?
5. há impacto em memória, CPU, heap, GC, conexão, pool ou throughput?
6. a solução pressupõe ambiente local benevolente demais?
7. a mudança afeta health checks, inicialização, readiness ou liveness?
8. existe custo operacional novo sendo introduzido?

---

## Dimensões mínimas da execução orientada a produção

### 1. Observabilidade
Se a mudança não puder ser observada, ela ainda está incompleta.

O sistema deve considerar:
- logs úteis;
- métricas mínimas;
- sinais de erro;
- pontos de tracing, quando aplicável;
- health indicators;
- capacidade de distinguir sucesso, degradação e falha.

Não é necessário instrumentar tudo de forma maximalista, mas é necessário evitar invisibilidade.

### 2. Modos de falha
Toda integração ou fluxo relevante deve ser lido também pelo lado da falha.

Perguntas mínimas:
- o que acontece se o banco atrasar ou cair?
- o que acontece se a API externa não responder?
- o que acontece se houver timeout?
- a aplicação falha rápido, falha mal ou degrada bem?
- existe retry cego onde não deveria?
- existe ausência de timeout onde deveria haver?

### 3. Estado e escalabilidade
A mudança deve ser lida sob a ótica de:
- statefulness;
- afinidade local;
- cache local;
- sessão local;
- dependência de memória de processo;
- suposições que quebram réplicas paralelas.

Escala horizontal não é só infraestrutura; ela começa no desenho do comportamento.

### 4. Recursos e runtime
Sempre que a task tocar comportamento de runtime, o sistema deve considerar:
- consumo de memória;
- comportamento de heap e GC;
- consumo de CPU;
- saturação de pool;
- pressão de banco;
- explosão de I/O;
- custo de concorrência.

Autoscaling não corrige código mal desenhado.  
Cloud não absolve erro de modelo operacional.

### 5. Execution model
Mudanças devem respeitar o modelo de execução real do sistema:
- long-running service;
- container;
- serverless;
- job assíncrono;
- pipeline;
- background worker.

Cada modelo impõe consequências diferentes e o sistema não deve fingir que são equivalentes.

### 6. Health and readiness
Quando aplicável, a solução deve respeitar:
- distinção entre readiness e liveness;
- inicialização real do serviço;
- dependências mínimas para aceitar tráfego;
- risco de loop de restart por checagem mal configurada.

---

## Relação com architecture-by-pain

Execução orientada a produção não significa sofisticar tudo desde o início.

A pergunta correta não é:
“vamos desenhar solução enterprise completa?”

A pergunta correta é:
“qual o menor nível de maturidade operacional que impede irresponsabilidade?”

Este protocolo é contra:
- ingenuidade operacional;
- mas também contra over-engineering de produção.

---

## O que o Execution Plan deve registrar

Quando a task tiver impacto operacional, o plan deve dizer:

- que pressuposto de runtime a solução faz;
- que risco operacional a mudança toca;
- se há impacto em observabilidade;
- se há impacto em falha parcial;
- se há impacto em estado, concorrência ou escala;
- que validações de produção-minded execution estão previstas.

---

## O que o Completion Packet deve registrar

Quando a task tiver impacto operacional, o completion packet deve dizer:

- o que foi considerado;
- o que foi validado;
- o que não foi validado;
- que risco operacional permanece;
- que observabilidade foi mantida ou alterada;
- que follow-up pode ser necessário.

---

## O que o reviewer deve observar

O reviewer deve desconfiar de soluções que:

- passam no caminho feliz, mas ignoram falha;
- assumem ambiente local idealizado;
- introduzem estado sem perceber;
- pioram observabilidade;
- ampliam custo operacional sem explicitar;
- tratam runtime real como detalhe irrelevante;
- usam cloud ou autoscaling como muleta para problema de código ou modelo.

---

## Relação com skills

Quando a task exigir mais profundidade, o sistema deve acionar skills como:

- `observability-first`
- `performance-and-capacity-review`
- `concurrency-and-statefulness-review`
- `failure-mode-and-reliability-review`
- `runtime-resource-diagnostics`
- `docker-container-baseline`
- `cloud-runtime-choice-review`

---

## O que este protocolo não exige

Este protocolo não exige:
- antecipar toda necessidade futura;
- construir plataforma de observabilidade para cada task;
- desenhar alta disponibilidade complexa sem justificativa;
- tratar toda mudança como incidente de produção.

Ele exige apenas que o sistema pense como sistema real, não como demo local.

---

## Declaração operacional curta

Localhost não é critério de verdade.  
Produção começa no desenho da solução.  
A engenharia boa pergunta cedo como o sistema roda, falha, escala e será observado.