# Skill — API Abuse and Input Validation

## Finalidade

Esta skill orienta a revisão de validação de entrada, contratos HTTP, payloads, abuso de API, enumeração, rate abuse e proteção contra chamadas maliciosas ou desproporcionais.

Seu papel é impedir que endpoints aceitem qualquer dado, executem operações caras sem limite ou exponham comportamento abusável.

---

## Quando usar

Use esta skill quando a task tocar:

- endpoint HTTP;
- controller;
- minimal API;
- mutation;
- formulário;
- upload;
- busca;
- filtro;
- paginação;
- payload JSON;
- query string;
- route parameter;
- webhook;
- integração externa;
- operação cara;
- endpoint público;
- endpoint autenticado com recurso por usuário.

---

## Quando não usar

Não use esta skill quando:

- não houver API ou input externo;
- a mudança for puramente interna;
- o contrato já estiver validado e a task não alterar input;
- a análise só geraria ruído em task trivial.

---

## Tese central

Toda API exposta será chamada de formas inesperadas.

Validação deve proteger:

- corretude;
- segurança;
- custo;
- disponibilidade;
- consistência;
- experiência de erro.

---

## Método

### 1. Mapear entradas

Listar:

- route params;
- query params;
- body;
- headers;
- files;
- cookies;
- claims;
- webhook payload;
- external event.

---

### 2. Validar shape

Verificar:

- campos obrigatórios;
- tipos;
- tamanho máximo;
- formato;
- enum;
- range;
- normalização;
- campos desconhecidos;
- payload vazio;
- payload grande.

---

### 3. Validar semântica

Perguntar:

- IDs pertencem ao usuário/tenant?
- datas fazem sentido?
- valores combinam entre si?
- estado atual permite a ação?
- operação é idempotente?
- recurso existe e é acessível?

---

### 4. Avaliar abuso

Perguntar:

- endpoint pode ser chamado em loop?
- busca permite wildcard caro?
- paginação tem limite?
- upload tem limite?
- payload grande causa custo alto?
- erro permite enumeração?
- operação pode ser usada para brute force?
- há rate limit ou mitigação?

---

### 5. Avaliar resposta de erro

Erro deve ser:

- claro o suficiente para cliente legítimo;
- seguro contra enumeração;
- consistente;
- sem stack trace;
- sem detalhes internos sensíveis.

---

### 6. Avaliar custo de execução

Perguntar:

- input barato dispara query cara?
- filtro sem índice pode degradar?
- request pode prender conexão?
- operação faz fan-out?
- chama API externa por item?
- gera trabalho assíncrono ilimitado?

---

## Output esperado

```md
# API Abuse and Input Validation Review

## Endpoint ou contrato
<método, rota, operação ou webhook>

## Entradas analisadas
- <entrada 1>
- <entrada 2>

## Validação de shape
<suficiente | insuficiente | incerta>

## Validação semântica
<suficiente | insuficiente | incerta>

## Riscos de abuso
- <risco 1>
- <risco 2>

## Paginação/limites/rate
<análise curta>

## Respostas de erro
<análise curta>

## Veredito
<suficiente | ajustar | escalar>

## Risco residual
<risco que permanece>
```

---

## Checklist de qualidade

Antes de aceitar, verificar:

- route/query/body foram validados?
- tamanho de payload foi considerado?
- paginação tem limite?
- upload tem limite?
- IDs são autorizados?
- busca não permite custo ilimitado?
- erro não revela informação sensível?
- operação cara tem proteção?
- webhook valida origem/assinatura quando aplicável?
- há risco de enumeração?

---

## Critérios de escalonamento

Escalar quando:

- endpoint for público e crítico;
- houver upload;
- houver pagamento, auth ou dado sensível;
- abuso puder causar custo alto;
- input puder disparar operação assíncrona ou externa;
- houver risco de enumeração de usuários ou recursos;
- a mitigação exigir rate limit global ou decisão de produto.

---

## Anti-patterns

Evitar:

- validação só no frontend;
- aceitar payload sem limite;
- paginação sem máximo;
- buscar tudo e filtrar depois;
- erro que confirma existência de recurso privado;
- webhook sem validação de origem;
- operação cara sem throttling;
- confiar em ID vindo do cliente;
- converter erro interno em 200 com mensagem genérica.

---

## Declaração operacional curta

API segura valida forma, sentido, permissão e custo.  
Input externo nunca é neutro.