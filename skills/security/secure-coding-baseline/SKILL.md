# Skill — Secure Coding Baseline

## Finalidade

Esta skill orienta a aplicação de uma baseline mínima de segurança em mudanças de código.

Seu papel é impedir que o agente implemente funcionalidades funcionais, mas inseguras, ignorando input não confiável, autorização, validação, exposição de dados, tratamento de erro, dependências, logs e superfície de abuso.

---

## Quando usar

Use esta skill quando a task tocar:

- input externo;
- API;
- autenticação;
- autorização;
- dados sensíveis;
- configuração;
- integração externa;
- upload/download;
- query;
- serialização;
- logs;
- dependência nova;
- frontend com dados de usuário;
- infraestrutura;
- qualquer fluxo exposto a usuário, sistema externo ou internet.

---

## Quando não usar

Não use esta skill quando:

- a task for puramente documental;
- a mudança for local e sem superfície de entrada;
- a segurança já estiver coberta por skill mais específica;
- a aplicação da skill geraria análise pesada sem risco real.

---

## Tese central

Código seguro começa assumindo que entrada externa não é confiável.

O harness não precisa transformar toda task em auditoria AppSec profunda, mas precisa garantir que nenhuma mudança relevante ignore a superfície de risco básica.

---

## Método

### 1. Identificar fronteira de confiança

Perguntar:

- de onde vem o dado?
- quem controla esse dado?
- o dado vem de usuário?
- vem de sistema externo?
- vem de arquivo?
- vem de variável de ambiente?
- vem de banco?
- vem de payload HTTP?

Tudo que cruza fronteira precisa ser tratado com cautela.

---

### 2. Validar input

Verificar:

- tipo;
- formato;
- tamanho;
- obrigatoriedade;
- intervalo;
- enumeração;
- encoding;
- normalização;
- rejeição de valores inesperados.

Validação não deve existir só no frontend.

---

### 3. Verificar autorização

Perguntar:

- quem pode executar esta ação?
- o usuário está autenticado?
- ele tem permissão para este recurso?
- há checagem por owner, tenant, role ou policy?
- há risco de IDOR?

Autenticação não substitui autorização.

---

### 4. Proteger dados sensíveis

Verificar:

- dados sensíveis não são logados;
- payloads não expõem mais do que precisam;
- erros não revelam detalhes internos;
- secrets não aparecem em código;
- configurações sensíveis não são commitadas;
- respostas não vazam campos internos.

---

### 5. Tratar erros com segurança

Erros devem ser úteis, mas não reveladores demais.

Evitar:

- stack trace para usuário;
- mensagem interna em API pública;
- catch vazio;
- erro genérico sem log interno;
- log com segredo.

---

### 6. Avaliar dependências

Se houver dependência nova ou atualizada:

- justificar necessidade;
- avaliar manutenção;
- avaliar superfície de supply chain;
- verificar se duplica capacidade existente;
- registrar risco.

---

### 7. Considerar abuso

Perguntar:

- a rota pode ser chamada em loop?
- há limite de tamanho?
- há rate limit ou mitigação?
- há risco de enumeração?
- há risco de brute force?
- há risco de payload grande?
- há risco de operação cara sob input barato?

---

### 8. Registrar validação e lacunas

No Completion Packet, registrar:

- segurança considerada;
- checagens realizadas;
- lacunas;
- riscos remanescentes;
- follow-ups.

---

## Output esperado

```md
# Secure Coding Baseline Review

## Superfície analisada
<endpoint, fluxo, componente, integração ou operação>

## Fronteiras de confiança
- <entrada 1>
- <entrada 2>

## Validação de input
<suficiente | insuficiente | não aplicável | incerto>

## Autenticação/autorização
<suficiente | insuficiente | não aplicável | incerto>

## Dados sensíveis
<risco e mitigação>

## Tratamento de erro
<análise curta>

## Riscos de abuso
- <risco 1>
- <risco 2>

## Dependências/configuração
<análise curta>

## Veredito
<suficiente | ajustar | escalar>

## Risco residual
<risco que permanece>
```

---

## Checklist de qualidade

Antes de aceitar a mudança, verificar:

- entrada externa foi identificada?
- input é validado no backend?
- autorização foi checada?
- há risco de IDOR?
- dados sensíveis estão protegidos?
- logs não vazam segredo?
- erros não expõem detalhes internos?
- dependências foram justificadas?
- abuso básico foi considerado?
- lacunas foram registradas?

---

## Critérios de escalonamento

Escalar quando:

- houver risco de exposição de dado sensível;
- autorização estiver ambígua;
- segredo aparecer em diff, log ou config;
- a mudança tocar produção;
- a task envolver auth, pagamento, dados pessoais ou tenant isolation;
- a mitigação exigir decisão arquitetural;
- a validação de segurança não puder ser feita.

---

## Anti-patterns

Evitar:

- confiar só no frontend;
- autenticar sem autorizar;
- aceitar qualquer payload;
- retornar entidade inteira sem filtro;
- logar token, header ou payload sensível;
- catch vazio;
- expor stack trace;
- adicionar dependência por conveniência;
- tratar input interno como sempre confiável.

---

## Declaração operacional curta

Segurança básica não é opcional.  
Toda fronteira de confiança exige validação, autorização, proteção de dados e evidência proporcional.