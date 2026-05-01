# Skill — Secrets and Config Hygiene

## Finalidade

Esta skill orienta o tratamento seguro de segredos, variáveis de ambiente, connection strings, tokens, chaves, certificados e configurações sensíveis.

Seu papel é impedir que o agente leia, exponha, registre, versione ou manipule segredo como se fosse dado comum.

---

## Quando usar

Use esta skill quando a task tocar:

- `.env`;
- appsettings;
- connection string;
- API key;
- token;
- password;
- certificado;
- private key;
- OAuth secret;
- webhook secret;
- cloud credential;
- service principal;
- configuração de produção;
- secret store;
- logs com dados sensíveis;
- CI/CD secrets.

---

## Quando não usar

Não use esta skill quando:

- não houver segredo nem configuração sensível;
- a task for puramente documental sem valores reais;
- a análise já estiver coberta por policy de produção/segredo.

---

## Tese central

Segredo não deve ser visto, copiado, logado ou commitado.

Quando a existência de um segredo importa, o ideal é confirmar presença, nome, referência ou configuração sem revelar valor.

---

## Método

### 1. Identificar material sensível

Classificar:

- secret real;
- placeholder;
- config pública;
- config sensível;
- credential file;
- token temporário;
- dado pessoal;
- connection string.

---

### 2. Evitar exposição

Não reproduzir:

- valor do segredo;
- token completo;
- connection string real;
- private key;
- certificado;
- senha;
- header Authorization;
- payload sensível.

Se precisar mencionar, mascarar.

Exemplo:

```text
API_KEY=<redacted>
```

---

### 3. Verificar versionamento

Perguntar:

- o segredo aparece em arquivo versionado?
- aparece em diff?
- aparece em documentação?
- aparece em exemplo realista demais?
- `.gitignore` cobre arquivos locais sensíveis?

---

### 4. Verificar configuração por ambiente

Perguntar:

- dev, staging e prod estão separados?
- config sensível vem de env/secret store?
- defaults são seguros?
- fallback não aponta para produção?
- config de produção não está local?

---

### 5. Verificar logs

Perguntar:

- erro pode imprimir secret?
- config é logada?
- headers são logados?
- payloads sensíveis são logados?
- exceptions expõem connection string?

---

### 6. Verificar rotação e incidente

Se segredo real foi exposto:

- não apenas remover do arquivo;
- registrar risco;
- orientar rotação;
- tratar como potencial incidente;
- evitar repetir o valor.

---

## Output esperado

```md
# Secrets and Config Hygiene Review

## Superfície analisada
<arquivo, config, pipeline, log ou integração>

## Material sensível identificado
<tipo sem revelar valor>

## Exposição em código/diff/log
<sim | não | incerto>

## Estratégia de configuração
<env | secret store | local config | hardcoded | incerto>

## Riscos
- <risco 1>
- <risco 2>

## Ações recomendadas
- <ação 1>
- <ação 2>

## Veredito
<suficiente | ajustar | escalar>

## Risco residual
<risco que permanece>
```

---

## Checklist de qualidade

Antes de aceitar, verificar:

- há segredo real no diff?
- há connection string real?
- há token em log?
- há arquivo sensível versionado?
- placeholders são claramente fictícios?
- `.gitignore` cobre arquivos locais?
- config de produção está protegida?
- ambiente está claro?
- erro não vaza config?
- se houve exposição, rotação foi considerada?

---

## Critérios de escalonamento

Escalar quando:

- segredo real aparecer em diff;
- segredo pode ter sido commitado;
- segredo apareceu em log;
- config de produção foi tocada;
- secret store ou CI secret precisar ser alterado;
- houver dúvida sobre rotação;
- houver risco de acesso externo.

---

## Anti-patterns

Evitar:

- colar segredo em prompt;
- imprimir `.env`;
- commitar appsettings com segredo real;
- usar placeholder realista demais;
- logar config inteira;
- guardar token no frontend;
- usar fallback para produção;
- tratar remoção do segredo do arquivo como solução completa após exposição;
- misturar configuração local e produção.

---

## Declaração operacional curta

Segredo não é conteúdo comum.  
O harness deve preservar referência e intenção sem reproduzir valor sensível.