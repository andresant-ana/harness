# Skill — Authn/Authz Review

## Finalidade

Esta skill orienta a revisão de autenticação, autorização, identidade, sessão, escopo de permissão e controle de acesso.

Seu papel é impedir que o agente confunda usuário autenticado com usuário autorizado, exponha recursos indevidos ou implemente fluxos com privilégio excessivo.

---

## Quando usar

Use esta skill quando a task tocar:

- login;
- logout;
- sessão;
- token;
- JWT;
- refresh token;
- cookie;
- OAuth/OIDC;
- roles;
- claims;
- policies;
- permissões;
- tenant;
- owner;
- ACL;
- endpoint protegido;
- dados privados;
- recursos por usuário;
- admin features.

---

## Quando não usar

Não use esta skill quando:

- não houver identidade, usuário ou recurso protegido;
- a task for puramente documental;
- a alteração não tocar fluxo de acesso;
- outra revisão de auth já cobrir a task com evidência suficiente.

---

## Tese central

Autenticação responde “quem é?”.  
Autorização responde “pode fazer isso neste recurso?”.

Um sistema pode estar autenticado e ainda assim inseguro.

---

## Método

### 1. Identificar atores

Listar:

- usuário anônimo;
- usuário autenticado;
- owner;
- admin;
- operador;
- serviço interno;
- sistema externo;
- tenant;
- role específica.

---

### 2. Identificar recursos

Mapear:

- que recurso está sendo acessado;
- quem é dono;
- qual tenant;
- qual escopo;
- se é público ou privado;
- se há dado sensível.

---

### 3. Verificar autenticação

Perguntar:

- o endpoint exige autenticação?
- token/cookie é validado?
- expiração é respeitada?
- issuer/audience são validados?
- refresh flow é seguro?
- logout invalida o que precisa invalidar?

---

### 4. Verificar autorização

Perguntar:

- o usuário pode acessar este recurso específico?
- há checagem de owner?
- há checagem de tenant?
- há checagem de role/policy?
- há risco de IDOR?
- o backend impõe a regra?

Nunca depender apenas de esconder botão no frontend.

---

### 5. Verificar privilégio mínimo

Perguntar:

- a permissão concedida é mínima?
- admin é amplo demais?
- service account tem escopo excessivo?
- token carrega claims demais?
- endpoint interno ficou exposto?

---

### 6. Verificar falhas

Considerar:

- token expirado;
- token inválido;
- usuário sem permissão;
- recurso inexistente;
- recurso de outro usuário;
- tenant errado;
- tentativa de enumeração;
- downgrade de role.

---

## Output esperado

```md
# Authn/Authz Review

## Fluxo ou recurso analisado
<endpoint, página, ação, recurso ou integração>

## Atores
- <ator 1>
- <ator 2>

## Recurso protegido
<recurso, owner, tenant ou dado>

## Autenticação
<suficiente | insuficiente | não aplicável | incerta>

## Autorização
<suficiente | insuficiente | não aplicável | incerta>

## Risco de IDOR/tenant leak
<análise curta>

## Privilégio mínimo
<análise curta>

## Falhas consideradas
- <falha 1>
- <falha 2>

## Veredito
<suficiente | ajustar | escalar>

## Risco residual
<risco que permanece>
```

---

## Checklist de qualidade

Antes de aceitar, verificar:

- há autenticação onde precisa?
- há autorização no backend?
- owner/tenant são verificados?
- role/policy faz sentido?
- existe risco de IDOR?
- token é validado corretamente?
- refresh/session foram considerados?
- frontend não é a única barreira?
- erro não revela recurso privado?
- privilégio mínimo foi respeitado?

---

## Critérios de escalonamento

Escalar quando:

- houver dados sensíveis;
- houver multi-tenant;
- houver admin ou privilégio elevado;
- houver mudança em token/session;
- houver dúvida sobre policy;
- houver risco de IDOR;
- houver impacto em login, refresh ou logout;
- houver decisão de arquitetura de identidade.

---

## Anti-patterns

Evitar:

- autenticar sem autorizar;
- confiar em ID vindo do cliente;
- filtrar recurso só no frontend;
- expor endpoint admin sem policy;
- retornar diferença clara entre recurso inexistente e proibido quando isso permitir enumeração;
- token sem validação completa;
- role genérica demais;
- service account com permissão ampla;
- tenant vindo apenas do payload.

---

## Declaração operacional curta

Auth segura exige identidade validada e permissão específica sobre recurso específico.  
Autenticação sem autorização é falsa segurança.