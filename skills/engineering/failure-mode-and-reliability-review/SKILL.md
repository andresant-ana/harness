# Skill — Failure Mode and Reliability Review

## Finalidade

Esta skill orienta a análise de modos de falha, resiliência e confiabilidade de uma mudança.

Seu papel é impedir que o agente desenhe apenas o caminho feliz, ignorando timeout, falha parcial, retry, fallback, indisponibilidade de dependência, degradação e recuperação.

---

## Quando usar

Use esta skill quando a task tocar:

- API externa;
- banco;
- fila;
- storage;
- pagamento;
- autenticação;
- autorização;
- envio de e-mail;
- webhook;
- job;
- worker;
- integração entre módulos;
- processamento assíncrono;
- runtime cloud;
- fluxo crítico de usuário;
- operação que precisa ser confiável.

---

## Quando não usar

Não use esta skill quando:

- a mudança for puramente local e sem dependência;
- a task for documental;
- não houver caminho de falha relevante;
- a análise só adicionaria ritual.

---

## Tese central

Sistema real falha parcialmente.

Boa engenharia não pergunta apenas:

“como isso funciona?”

Pergunta também:

“como isso falha, como detectamos, como limitamos dano e como recuperamos?”

---

## Método

### 1. Mapear dependências

Listar dependências tocadas:

- banco;
- API externa;
- fila;
- cache;
- storage;
- identity provider;
- serviço interno;
- filesystem;
- rede;
- runtime;
- segredo/config.

---

### 2. Mapear falhas plausíveis

Para cada dependência, considerar:

- timeout;
- erro 4xx/5xx;
- indisponibilidade;
- latência alta;
- resposta inválida;
- dado inconsistente;
- falha parcial;
- duplicidade;
- retry;
- limite de rate;
- queda durante transação.

---

### 3. Avaliar comportamento atual

Perguntar:

- falha rápido ou trava?
- há timeout?
- há retry?
- retry é seguro?
- há fallback?
- há circuit breaker?
- há compensação?
- erro é visível?
- usuário recebe resposta adequada?
- estado fica consistente?

---

### 4. Avaliar retry e idempotência

Retry só é seguro quando a operação tolera repetição.

Perguntar:

- repetir cria duplicidade?
- há idempotency key?
- há constraint?
- há deduplicação?
- há risco de retry storm?

---

### 5. Avaliar degradação

Quando falhar, o sistema deve:

- bloquear com mensagem clara;
- degradar parcialmente;
- cair para fallback;
- enfileirar;
- falhar rápido;
- acionar alerta;
- registrar lacuna.

A escolha depende do fluxo.

---

### 6. Avaliar observabilidade de falha

Falhas precisam gerar sinal suficiente:

- log seguro;
- métrica;
- erro classificado;
- trace;
- evento;
- health signal.

---

## Output esperado

```md
# Failure Mode and Reliability Review

## Fluxo analisado
<fluxo, endpoint, job, integração ou operação>

## Dependências tocadas
- <dependência 1>
- <dependência 2>

## Modos de falha plausíveis
- <falha 1>
- <falha 2>

## Comportamento esperado em falha
<falhar rápido | retry | fallback | degradar | compensar | escalar>

## Retry e idempotência
<análise curta>

## Observabilidade de falha
<sinais existentes ou lacunas>

## Riscos remanescentes
- <risco 1>
- <risco 2>

## Veredito
<suficiente | ajustar | escalar>
```

---

## Checklist de qualidade

Antes de aceitar, verificar:

- há timeout onde precisa?
- retry é seguro?
- fallback faz sentido?
- erro não é engolido?
- falha parcial não corrompe estado?
- dependência externa tem tratamento?
- usuário recebe resposta coerente?
- há log/métrica/sinal?
- idempotência foi considerada?
- há risco de retry storm?

---

## Critérios de escalonamento

Escalar quando:

- falha pode causar perda ou corrupção de dado;
- fluxo crítico não tem fallback plausível;
- retry exige decisão arquitetural;
- compensação transacional é necessária;
- dependência externa é central e instável;
- observabilidade de falha exige padrão global;
- a escolha impacta produto ou operação.

---

## Anti-patterns

Evitar:

- caminho feliz como único desenho;
- retry cego;
- ausência de timeout;
- catch vazio;
- fallback que esconde erro crítico;
- logar erro sem contexto;
- tratar API externa como confiável;
- ignorar rate limit;
- compensar manualmente sem registro;
- considerar fila como garantia mágica.

---

## Declaração operacional curta

Confiabilidade é desenhar também para falha.  
O harness deve perguntar cedo como o sistema quebra, sinaliza e se recupera.