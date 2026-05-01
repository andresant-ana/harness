# Skill — HTTP API Contract Debugging

## Finalidade

Esta skill orienta investigação e revisão de contratos HTTP, endpoints, requests, responses, status codes, headers, payloads e falhas de integração entre cliente e servidor.

Seu papel é impedir que o agente trate bugs de API como simples erro de código, ignorando contrato, semântica HTTP, validação, autorização, serialização e observabilidade.

---

## Quando usar

Use esta skill quando a task envolver:

- endpoint HTTP;
- contrato de API;
- status code incorreto;
- payload divergente;
- erro 400/401/403/404/409/422/500;
- headers;
- autenticação;
- CORS;
- frontend chamando backend;
- webhook;
- integração externa;
- serialização JSON;
- versionamento de API;
- OpenAPI/Swagger;
- debugging de request/response.

---

## Quando não usar

Não use esta skill quando:

- não houver HTTP/API;
- a falha for puramente interna e já isolada;
- o contrato estiver fora de escopo;
- a análise só duplicaria skill de input/security já aplicada.

---

## Tese central

API é contrato, não só função remota.

Debug de API deve separar:

- erro de cliente;
- erro de contrato;
- erro de autenticação;
- erro de autorização;
- erro de validação;
- erro de servidor;
- erro de integração;
- erro de documentação.

---

## Método

### 1. Identificar operação

Registrar:

- método;
- rota;
- consumidor;
- produtor;
- payload;
- headers;
- auth;
- ambiente;
- resposta esperada;
- resposta observada.

---

### 2. Validar semântica HTTP

Verificar:

- método adequado;
- status code coerente;
- headers corretos;
- content type;
- cache;
- idempotência;
- localização de recurso;
- erro representado corretamente.

---

### 3. Validar contrato

Comparar:

- request real vs schema;
- response real vs schema;
- docs vs implementação;
- frontend client vs backend;
- tipos;
- campos obrigatórios;
- enum;
- nomes;
- formatos.

---

### 4. Validar auth e permissionamento

Distinguir:

- 401 não autenticado;
- 403 autenticado sem permissão;
- 404 para recurso inexistente ou ocultação intencional;
- risco de enumeração.

---

### 5. Validar erros

Erro deve ser:

- consistente;
- seguro;
- útil;
- sem stack trace;
- sem segredo;
- com correlation id quando aplicável.

---

### 6. Validar observabilidade

Verificar se há:

- log da operação;
- status code visível;
- erro classificado;
- trace/correlation;
- métrica quando relevante.

---

## Output esperado

```md
# HTTP API Contract Debugging

## Operação
<METHOD /route>

## Consumidor
<frontend | serviço | webhook | externo>

## Request esperado/observado
<resumo>

## Response esperado/observado
<status, body, headers>

## Divergência de contrato
- <divergência 1>
- <divergência 2>

## Auth/Authz
<análise curta>

## Erro e observabilidade
<análise curta>

## Causa provável
<contrato | validação | auth | servidor | integração | incerto>

## Ação recomendada
<ação>

## Veredito
<suficiente | ajustar | escalar>
```

---

## Checklist de qualidade

Antes de concluir, verificar:

- método HTTP faz sentido?
- status code está correto?
- payload bate com contrato?
- campos obrigatórios estão claros?
- erro é seguro?
- 401/403/404 foram diferenciados?
- CORS é relevante?
- content type está correto?
- auth foi considerada?
- logs ajudam diagnóstico?

---

## Critérios de escalonamento

Escalar quando:

- contrato público precisa mudar;
- mudança quebra cliente existente;
- há risco de segurança;
- há decisão entre versionar ou alterar contrato;
- status code envolve decisão de produto;
- integração externa depende de comportamento incerto;
- falha afeta produção.

---

## Anti-patterns

Evitar:

- tratar 500 como resposta normal;
- retornar 200 com erro sem padrão;
- esconder problema de contrato no frontend;
- usar 401 para tudo;
- vazar stack trace;
- mudar response sem versionar;
- aceitar docs desatualizadas como verdade;
- ignorar headers/content-type;
- debug sem request/response real.

---

## Declaração operacional curta

HTTP é contrato observável.  
Debug bom compara request, response, schema, auth e semântica antes de mexer no código.