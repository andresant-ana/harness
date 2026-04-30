# Skill — Observability First

## Finalidade

Esta skill orienta a consideração de observabilidade em mudanças relevantes.

Seu papel é impedir que o agente entregue funcionalidades, integrações, jobs, endpoints ou fluxos que funcionam apenas no caminho feliz local, mas ficam invisíveis ou difíceis de diagnosticar em produção.

---

## Quando usar

Use esta skill quando a task tocar:

- endpoint;
- fluxo de usuário relevante;
- integração externa;
- autenticação/autorização;
- persistência crítica;
- processamento assíncrono;
- fila;
- job;
- runtime;
- cloud;
- deploy;
- erro recorrente;
- performance;
- falha parcial;
- comportamento que precisará ser monitorado.

---

## Quando não usar

Não use esta skill quando:

- a task for puramente documental;
- a mudança for local e sem impacto operacional;
- já houver observabilidade suficiente e nenhuma mudança relevante;
- a aplicação da skill viraria cerimônia sem ganho.

---

## Tese central

Se não é observável, não é operável com confiança.

Observabilidade não significa logar tudo.  
Significa deixar sinais suficientes para entender sucesso, falha, degradação e comportamento relevante.

---

## Dimensões

### 1. Logs

Logs devem responder:

- o que aconteceu?
- em qual operação?
- com qual contexto seguro?
- qual erro ocorreu?
- há correlação suficiente?

Não devem expor segredos ou dados sensíveis.

---

### 2. Métricas

Métricas devem responder:

- quantas vezes aconteceu?
- quanto demorou?
- falhou quanto?
- saturou onde?
- há retry, timeout ou degradação?

---

### 3. Tracing

Tracing deve ser considerado quando:

- há múltiplos serviços;
- há integração externa;
- há fluxo distribuído;
- há operação com várias etapas;
- há necessidade de causalidade ponta a ponta.

---

### 4. Health checks

Health checks devem distinguir:

- processo vivo;
- serviço pronto;
- dependência crítica disponível;
- capacidade real de receber tráfego.

Liveness e readiness não são a mesma coisa.

---

### 5. Erros acionáveis

Erros devem ajudar diagnóstico.

Erro ruim:

- genérico;
- silencioso;
- engolido;
- sem contexto;
- com dado sensível.

Erro bom:

- claro;
- seguro;
- correlacionável;
- diferenciado por causa plausível.

---

## Método

### 1. Identificar o comportamento observável

Perguntar:

- que evento ou fluxo importa?
- como saberemos que funcionou?
- como saberemos que falhou?
- quem precisará diagnosticar isso?

---

### 2. Identificar sinais existentes

Verificar se já existem:

- logs;
- métricas;
- traces;
- health checks;
- error handling;
- alertas;
- dashboards;
- padrões locais.

---

### 3. Detectar lacunas

Perguntar:

- se isso quebrar em produção, perceberemos?
- saberemos onde quebrou?
- saberemos se é usuário, sistema ou dependência externa?
- há risco de erro silencioso?

---

### 4. Propor observabilidade mínima

Adicionar ou recomendar apenas o necessário.

Evitar instrumentação ornamental.

---

### 5. Garantir segurança

Verificar que sinais não vazam:

- token;
- segredo;
- senha;
- connection string;
- payload sensível;
- dado pessoal desnecessário;
- header de autorização.

---

### 6. Registrar no plan ou completion

Se observabilidade for relevante, registrar:

- o que foi considerado;
- o que foi adicionado;
- o que já existia;
- o que ficou como lacuna.

---

## Output esperado

```md
# Observability Check

## Comportamento relevante
<fluxo, endpoint, job, integração ou operação>

## Sinais existentes
- <log/métrica/trace/health/error handling existente>

## Lacunas
- <lacuna 1>
- <lacuna 2>

## Observabilidade mínima recomendada
- <ação 1>
- <ação 2>

## Segurança dos sinais
<risco de dado sensível e mitigação>

## Veredito
<suficiente | adicionar mínimo | reavaliar | escalar>
```

---

## Checklist de qualidade

Antes de concluir, verificar:

- há forma de saber que funcionou?
- há forma de saber que falhou?
- erro crítico não será engolido?
- logs são úteis sem vazar dado?
- health check, se existir, faz sentido?
- integração externa tem sinal suficiente?
- operação assíncrona tem rastreabilidade?
- Completion Packet registra lacunas?

---

## Critérios de escalonamento

Escalar quando:

- fluxo crítico ficar invisível;
- observabilidade exigir decisão de plataforma;
- logs existentes vazarem dados sensíveis;
- health check puder derrubar serviço indevidamente;
- tracing/métricas exigirem padrão global;
- produção estiver envolvida.

---

## Anti-patterns

Evitar:

- logar tudo;
- não logar nada;
- logar segredo;
- criar métrica sem uso;
- trace ornamental;
- engolir exceção;
- tratar health check como ping;
- assumir que teste local substitui sinal operacional;
- adicionar observabilidade pesada em task simples sem necessidade.

---

## Declaração operacional curta

Observabilidade é capacidade de enxergar o sistema real.  
Sem sinal suficiente, a entrega fica operacionalmente frágil.