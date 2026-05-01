# Skill — Azure Execution Model Review

## Finalidade

Esta skill orienta a escolha ou revisão do modelo de execução Azure para workloads da stack principal.

Seu papel é impedir que o agente escolha App Service, Container Apps, Functions, AKS, Static Web Apps, Storage, filas ou outro serviço Azure por hype, tutorial ou familiaridade, sem avaliar workload, escala, custo, operação, estado, segurança e maturidade.

Esta skill complementa `cloud-runtime-choice-review`.  
A skill transversal compara modelos de runtime em geral.  
Esta skill foca opções e trade-offs específicos da Azure.

---

## Quando usar

Use esta skill quando a task envolver:

- escolha de recurso Azure;
- revisão de runtime;
- App Service;
- Azure Container Apps;
- Azure Functions;
- AKS;
- Azure Static Web Apps;
- Azure Storage;
- Azure Service Bus;
- Azure Queue Storage;
- Azure Container Registry;
- Azure SQL/PostgreSQL;
- workers;
- jobs;
- event-driven workloads;
- autoscaling;
- scale to zero;
- cold start;
- custo cloud;
- modelo operacional;
- migração de runtime.

---

## Quando não usar

Não use esta skill quando:

- o recurso Azure já estiver definido por authority source;
- a task não envolve Azure;
- a mudança for apenas código local;
- a decisão for puramente de entrega, não de modelo de execução;
- a análise seria especulativa sem workload concreto.

---

## Tese central

Na Azure, o modelo de execução molda a arquitetura.

Escolher App Service, Container Apps, Functions ou AKS não é detalhe de hospedagem.  
A decisão afeta:

- deploy;
- escala;
- custo;
- cold start;
- statefulness;
- observabilidade;
- networking;
- secrets;
- CI/CD;
- falha;
- operação diária;
- complexidade para o time.

A opção mais poderosa raramente é a melhor para o estágio inicial.

---

## Método

### 1. Definir workload

Classificar o workload:

- API HTTP;
- frontend estático;
- worker;
- job agendado;
- consumer de fila;
- processamento event-driven;
- processamento em lote;
- serviço interno;
- webhook receiver;
- aplicação containerizada;
- workload com GPU ou recurso especial, se aplicável.

---

### 2. Levantar requisitos

Registrar:

- tráfego esperado;
- latência;
- duração de execução;
- uso de CPU/memória;
- necessidade de escala horizontal;
- necessidade de scale to zero;
- cold start aceitável;
- estado local;
- dependências;
- rede privada;
- secrets;
- observabilidade;
- SLA;
- custo;
- maturidade operacional do projeto/time.

---

### 3. Avaliar App Service

App Service tende a ser adequado quando:

- workload é web/API tradicional;
- simplicidade operacional importa;
- deploy direto é suficiente;
- escala horizontal moderada basta;
- runtime gerenciado é preferível;
- não há necessidade forte de orquestração.

Riscos:

- custo fixo;
- menor controle de runtime;
- cuidado com slots/config;
- background jobs longos podem ser inadequados dependendo do caso.

---

### 4. Avaliar Azure Container Apps

Container Apps tende a ser adequado quando:

- workload já é containerizado;
- há API ou worker containerizado;
- escala flexível importa;
- scale to zero pode ser útil;
- Dapr/event-driven pode fazer sentido, com cautela;
- AKS seria over-engineering.

Riscos:

- mais conceitos que App Service;
- config de ingress/scale/secrets precisa ser bem entendida;
- cold start ou escala precisam ser avaliados;
- observabilidade e troubleshooting podem exigir maturidade maior.

---

### 5. Avaliar Azure Functions

Functions tende a ser adequada quando:

- workload é event-driven;
- execução é curta;
- trigger é natural;
- scale to zero é relevante;
- custo por execução faz sentido;
- acoplamento ao modelo serverless é aceitável.

Riscos:

- cold start;
- limites de execução;
- debugging e observabilidade;
- estado local inadequado;
- dependência forte de triggers/bindings;
- não ideal para lógica longa ou complexa demais.

---

### 6. Avaliar AKS

AKS tende a ser adequado quando:

- há necessidade real de Kubernetes;
- múltiplos serviços exigem orquestração avançada;
- rede, autoscaling, workloads e policies justificam;
- o time tem maturidade operacional;
- há escala/complexidade que paga o custo.

Riscos:

- overhead operacional alto;
- custo e complexidade;
- segurança, upgrades, ingress, observabilidade e node management;
- over-engineering para projeto inicial.

AKS não deve ser escolhido por prestígio.

---

### 7. Avaliar Static Web Apps / Storage

Para frontend:

- Static Web Apps pode ser adequada para SPA com integração simples;
- Storage static website + CDN pode ser suficiente em cenários simples;
- App Service pode ser excessivo para frontend estático;
- autenticação, roteamento, preview environments e CI/CD devem ser considerados.

---

### 8. Avaliar filas e eventos

Quando houver trabalho assíncrono:

- Azure Service Bus para mensageria mais robusta, tópicos, DLQ, ordering/transactions conforme necessidade;
- Azure Queue Storage para fila simples;
- Event Grid para eventos de infraestrutura/pub-sub;
- Event Hubs para ingestão de stream/telemetria em alta escala.

Não usar mensageria sem dor real.  
Acionar `messaging-justification-review`.

---

### 9. Avaliar statefulness

Perguntar:

- o workload depende de filesystem local?
- mantém sessão em memória?
- usa cache local como fonte de verdade?
- precisa sobreviver restart?
- roda em múltiplas instâncias?
- precisa de storage externo?
- depende de sticky session?

Cloud runtime deve assumir processo descartável sempre que possível.

---

### 10. Avaliar custo e operação

Perguntar:

- custo mínimo mensal importa?
- escala para zero importa?
- quem opera?
- como diagnostica?
- como faz rollback?
- como configura secrets?
- como monitora?
- como faz deploy?
- como isola ambientes?

---

## Output esperado

```md
# Azure Execution Model Review

## Workload
<API | frontend | worker | job | event-driven | batch | outro>

## Requisitos principais
- <requisito 1>
- <requisito 2>

## Opções Azure consideradas
- <App Service>
- <Container Apps>
- <Functions>
- <AKS>
- <Static Web Apps>
- <Storage/Queue/Service Bus/etc>

## Comparação
| Opção | Benefícios | Custos | Riscos | Adequação |
|------|------------|--------|--------|-----------|
| | | | | |

## Statefulness
<análise curta>

## Escala e custo
<análise curta>

## Operação
<deploy, observabilidade, rollback, secrets, rede>

## Recomendação
<opção recomendada e motivo>

## O que fica na mesa
<trade-offs aceitos>

## Critério de revisão futura
<quando reavaliar>
```

---

## Checklist de qualidade

Antes de recomendar, verificar:

- workload está claro?
- tráfego e duração foram considerados?
- scale to zero importa?
- cold start é aceitável?
- estado local foi eliminado ou justificado?
- custo mínimo foi considerado?
- observabilidade foi considerada?
- secrets/config foram considerados?
- rede privada é necessária?
- CI/CD é compatível?
- operação pelo time é realista?
- AKS foi descartado se não houver dor real?
- mensageria foi justificada por dor real?

---

## Critérios de escalonamento

Escalar quando:

- runtime afetar arquitetura;
- houver produção;
- houver SLA;
- houver custo cloud relevante;
- houver necessidade de AKS;
- houver decisão entre App Service, Container Apps e Functions com trade-offs fortes;
- houver estado local difícil de remover;
- houver requisito de rede privada/security boundary;
- houver escolha de mensageria;
- workload envolver dados sensíveis ou operação crítica.

---

## Anti-patterns

Evitar:

- AKS para projeto simples;
- Functions para workload longo sem avaliar limites;
- Container Apps só porque “container é moderno”;
- App Service como resposta automática para tudo;
- usar fila para esconder lentidão sem entender causa;
- estado local em runtime escalável;
- assumir autoscaling como cura para código ruim;
- ignorar cold start;
- ignorar custo mínimo;
- escolher runtime antes de entender workload;
- copiar arquitetura de tutorial da Azure.

---

## Relação com outras skills

Use junto com:

- `cloud-runtime-choice-review`, para comparação runtime geral;
- `azure-delivery-reviewer`, para entrega no recurso escolhido;
- `messaging-justification-review`, se fila/evento estiverem em discussão;
- `failure-mode-and-reliability-review`, se houver falha parcial;
- `observability-first`, para sinais operacionais;
- `iac-security-review`, se a escolha envolver IaC;
- `secrets-and-config-hygiene`, se houver config sensível.

---

## Declaração operacional curta

Modelo de execução Azure deve seguir o workload, não o hype.  
A melhor escolha é a mais simples que atende escala, custo, operação e risco reais.