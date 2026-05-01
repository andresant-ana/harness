# Skill — ASP.NET Endpoint Review

## Finalidade

Esta skill orienta criação, alteração e revisão de endpoints ASP.NET, incluindo Controllers, Minimal APIs, contratos HTTP, validação, status codes, autenticação, autorização, error handling e boundaries de API.

Seu papel é impedir que o agente implemente endpoints que funcionam no caminho feliz, mas têm contrato fraco, validação insuficiente, status code incoerente, autorização ausente ou comportamento difícil de operar.

---

## Quando usar

Use esta skill quando a task tocar:

- Controller;
- Minimal API;
- endpoint HTTP;
- rota;
- request DTO;
- response DTO;
- status code;
- model binding;
- validação;
- autenticação;
- autorização;
- OpenAPI/Swagger;
- error handling;
- filtros/middlewares;
- contratos entre frontend e backend;
- integração externa via HTTP.

---

## Quando não usar

Não use esta skill quando:

- a task não envolve endpoint/API;
- a alteração é interna e não muda contrato HTTP;
- outra skill de API já cobriu o mesmo escopo com evidência suficiente;
- a mudança é apenas documentação sem alteração de contrato.

---

## Tese central

Endpoint é contrato público ou interno versionável.

Um endpoint bom precisa ser:

- claro;
- validado;
- autorizado;
- previsível;
- observável;
- proporcional;
- coerente com semântica HTTP;
- alinhado ao caso de uso real.

---

## Método

### 1. Identificar o contrato

Registrar:

- método HTTP;
- rota;
- consumidor;
- request;
- response;
- status codes;
- autenticação;
- autorização;
- versão, se houver;
- comportamento esperado.

---

### 2. Verificar rota e método

Perguntar:

- o método HTTP representa a intenção?
- a rota é consistente com o padrão local?
- o recurso está bem nomeado?
- há ambiguidade de rota?
- existe versionamento?
- a rota expõe detalhe interno desnecessário?

---

### 3. Verificar request e validação

Avaliar:

- campos obrigatórios;
- tipos;
- ranges;
- tamanho máximo;
- enums;
- normalização;
- IDs;
- datas;
- validação de negócio;
- validação no backend.

Validação frontend não substitui validação backend.

---

### 4. Verificar autorização

Perguntar:

- endpoint exige autenticação?
- usuário pode executar essa ação?
- recurso pertence ao usuário/tenant?
- roles/policies estão corretas?
- há risco de IDOR?
- backend impõe regra?

---

### 5. Verificar response

Avaliar:

- status code correto;
- response body mínimo e suficiente;
- não expõe entidade interna demais;
- não vaza dados sensíveis;
- erro tem formato consistente;
- mensagens não revelam detalhe interno;
- contratos são claros para o consumidor.

---

### 6. Verificar error handling

Perguntar:

- erro de validação vira 400/422 conforme padrão local?
- não autorizado vira 401?
- sem permissão vira 403?
- recurso inexistente vira 404?
- conflito vira 409?
- erro inesperado vira 500 tratado?
- há log/correlation quando relevante?

---

### 7. Verificar observabilidade

Endpoints relevantes devem permitir entender:

- volume;
- latência;
- erro;
- status code;
- falha de dependência;
- correlation id, quando aplicável.

---

### 8. Verificar impacto em testes

Considerar:

- teste de unidade do handler/use case;
- teste de integração do endpoint;
- teste de contrato;
- teste de validação;
- teste de autorização.

---

## Output esperado

```md
# ASP.NET Endpoint Review

## Endpoint
<METHOD /route>

## Consumidor
<frontend | serviço | externo | interno>

## Request
<shape, validações e pontos sensíveis>

## Response
<status codes, body e erros>

## Auth/Authz
<análise de autenticação/autorização>

## Validação
<suficiente | insuficiente | incerta>

## Error handling
<análise curta>

## Observabilidade
<logs/métricas/correlation/lacunas>

## Testes recomendados
- <teste 1>
- <teste 2>

## Veredito
<suficiente | ajustar | escalar>

## Risco residual
<risco que permanece>
```

---

## Checklist de qualidade

Antes de aceitar, verificar:

- método HTTP está correto?
- rota segue convenção local?
- request DTO é mínimo e validado?
- response DTO não expõe entidade interna demais?
- status codes são coerentes?
- autorização foi checada no backend?
- há risco de IDOR?
- erros são consistentes e seguros?
- contrato está refletido em OpenAPI/Swagger, se aplicável?
- há teste proporcional?
- observabilidade foi considerada?

---

## Critérios de escalonamento

Escalar quando:

- endpoint altera contrato público;
- há dados sensíveis;
- há multi-tenant;
- há decisão de versionamento;
- há quebra de compatibilidade;
- há risco de autorização;
- há impacto em produto;
- o endpoint exige mudança arquitetural;
- o contrato depende de decisão do Core Architect.

---

## Anti-patterns

Evitar:

- retornar entidade EF diretamente;
- validar apenas no frontend;
- usar 200 para erro sem padrão;
- usar 500 para erro de validação;
- autenticar sem autorizar;
- aceitar ID do cliente sem verificar ownership;
- expor stack trace;
- criar endpoint genérico demais;
- misturar regra de domínio pesada no controller;
- ignorar contrato do consumidor.

---

## Declaração operacional curta

Endpoint ASP.NET é contrato operacional.  
Ele precisa validar input, autorizar ação, responder com semântica HTTP correta e deixar erro observável.