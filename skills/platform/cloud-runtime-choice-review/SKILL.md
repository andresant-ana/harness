# Skill — Cloud Runtime Choice Review

## Finalidade

Esta skill orienta a escolha ou revisão de runtime/cloud execution model para uma aplicação, serviço, job ou workload.

Seu papel é impedir que o agente escolha App Service, Container Apps, Functions, AKS, VM, serverless, container ou outro modelo por hype, familiaridade ou tutorial, sem avaliar trade-offs de operação, escala, custo, complexidade e confiabilidade.

---

## Quando usar

Use esta skill quando a task envolver:

- escolha de runtime;
- deploy target;
- cloud architecture;
- container vs serverless;
- App Service;
- Azure Container Apps;
- Azure Functions;
- AKS;
- VM;
- job/worker;
- autoscaling;
- cold start;
- statefulness;
- observabilidade;
- custo cloud;
- requisitos operacionais;
- mudança de modelo de execução.

---

## Quando não usar

Não use esta skill quando:

- o runtime já está definido por authority source;
- a task não toca deploy/runtime;
- a escolha é irrelevante para o escopo;
- a análise seria puramente especulativa.

---

## Tese central

Runtime molda a aplicação.

Escolher onde rodar não é detalhe de deploy.  
A decisão afeta:

- arquitetura;
- observabilidade;
- escala;
- custos;
- falha;
- statefulness;
- CI/CD;
- segurança;
- operação diária.

---

## Método

### 1. Definir workload

Descrever:

- aplicação web;
- API;
- worker;
- job agendado;
- processamento em lote;
- evento;
- frontend estático;
- serviço interno;
- integração externa.

---

### 2. Mapear requisitos

Levantar:

- tráfego esperado;
- latência;
- duração de execução;
- consumo de memória/CPU;
- necessidade de scale to zero;
- estado local;
- persistência;
- rede;
- secrets;
- integração com banco/fila;
- SLA;
- custo aceitável;
- maturidade operacional.

---

### 3. Comparar opções

Comparar opções viáveis.

Exemplo:

| Runtime | Benefícios | Custos | Riscos | Quando usar |
|--------|------------|--------|--------|-------------|
| App Service | simples para web/API | menos controle fino | custo fixo | API persistente |
| Container Apps | container + escala flexível | mais conceitos | config/runtime | APIs/workers containerizados |
| Functions | event-driven/scale to zero | cold start/limites | execução curta | eventos/jobs curtos |
| AKS | controle alto | operação alta | complexidade | escala/infra madura |

---

### 4. Avaliar statefulness

Perguntar:

- a aplicação depende de filesystem local?
- sessão local?
- cache local?
- processo único?
- background thread dentro da web app?
- isso funciona em múltiplas réplicas?

---

### 5. Avaliar operação

Perguntar:

- como será observado?
- como escala?
- como faz deploy?
- como reverte?
- como lida com falha?
- quem opera?
- o time entende o runtime?

---

### 6. Recomendar runtime proporcional

A recomendação deve declarar:

- opção escolhida;
- por que é adequada agora;
- o que está sendo deixado na mesa;
- quando reavaliar.

---

## Output esperado

```md
# Cloud Runtime Choice Review

## Workload
<API | web | worker | job | event-driven | frontend | outro>

## Requisitos principais
- <requisito 1>
- <requisito 2>

## Opções consideradas
- <opção 1>
- <opção 2>
- <opção 3>

## Comparação
| Opção | Benefícios | Custos | Riscos | Adequação |
|------|------------|--------|--------|-----------|
| | | | | |

## Statefulness
<análise curta>

## Operação
<deploy, observabilidade, escala, custo, rollback>

## Recomendação
<runtime recomendado e motivo>

## Critério de revisão futura
<quando reavaliar>
```

---

## Checklist de qualidade

Antes de recomendar, verificar:

- workload está claro?
- tráfego e escala foram considerados?
- statefulness foi considerada?
- cold start importa?
- custo foi considerado?
- observabilidade foi considerada?
- operação pelo time é viável?
- segurança/secrets foram considerados?
- CI/CD é compatível?
- recomendação é proporcional ao estágio do projeto?

---

## Critérios de escalonamento

Escalar quando:

- runtime afetar arquitetura;
- houver produção;
- houver custo cloud relevante;
- houver SLA;
- houver necessidade de AKS/Kubernetes;
- houver disputa entre simplicidade e controle;
- houver integração crítica;
- houver requisito de segurança/rede complexo.

---

## Anti-patterns

Evitar:

- escolher Kubernetes por prestígio;
- usar serverless para workload longo sem avaliar limites;
- colocar state local em runtime escalável;
- assumir autoscaling como solução para código ruim;
- ignorar cold start;
- ignorar observabilidade;
- escolher runtime antes de entender workload;
- copiar arquitetura de tutorial;
- trocar simplicidade por controle desnecessário.

---

## Declaração operacional curta

Runtime é decisão arquitetural-operacional.  
Escolha boa respeita workload, escala, custo, operação e maturidade real do projeto.