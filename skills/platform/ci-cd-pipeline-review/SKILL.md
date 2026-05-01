# Skill — CI/CD Pipeline Review

## Finalidade

Esta skill orienta a revisão de pipelines de CI/CD, workflows, gates, checks, secrets, build, test, deploy e permissões.

Seu papel é impedir que automações de entrega sejam frágeis, inseguras, opacas ou capazes de causar efeitos externos sem controle.

---

## Quando usar

Use esta skill quando a task tocar:

- GitHub Actions;
- Azure Pipelines;
- CI;
- CD;
- workflow YAML;
- build pipeline;
- test pipeline;
- release;
- deploy;
- secrets de pipeline;
- permissões;
- artifacts;
- cache;
- environments;
- branch protection;
- checks obrigatórios.

---

## Quando não usar

Não use esta skill quando:

- não houver pipeline;
- a mudança for local e sem CI/CD;
- a alteração não afetar automação;
- a análise duplicar revisão já feita no mesmo escopo.

---

## Tese central

Pipeline é código operacional.

Erro em pipeline pode:

- quebrar entrega;
- vazar segredo;
- publicar artefato errado;
- disparar deploy indevido;
- pular teste;
- ampliar permissão;
- mascarar falhas.

---

## Método

### 1. Identificar objetivo do pipeline

Classificar:

- CI de validação;
- build;
- test;
- lint;
- package;
- publish;
- deploy;
- release;
- infra plan/apply.

---

### 2. Revisar gatilhos

Verificar:

- `push`;
- `pull_request`;
- `workflow_dispatch`;
- tags;
- branches;
- paths;
- cron;
- ambientes.

Perguntar se o gatilho é amplo demais.

---

### 3. Revisar permissões

Verificar:

- permissões do token;
- secrets acessíveis;
- environments protegidos;
- approvals;
- OIDC;
- service principal;
- escopo mínimo.

---

### 4. Revisar passos

Checar:

- checkout;
- setup de runtime;
- cache;
- restore/install;
- build;
- test;
- lint;
- artifact;
- deploy;
- ordem causal.

---

### 5. Revisar segurança

Perguntar:

- secret pode ser impresso?
- action externa é confiável?
- versão de action está pinada?
- PR externo pode acessar segredo?
- shell script é auditável?
- deploy exige aprovação?

---

### 6. Revisar evidência

Pipeline deve produzir sinais úteis:

- logs claros;
- test reports;
- build artifacts;
- status checks;
- failure modes compreensíveis.

---

## Output esperado

```md
# CI/CD Pipeline Review

## Pipeline analisado
<workflow, job ou stage>

## Objetivo
<CI | build | test | publish | deploy | IaC | outro>

## Gatilhos
<push, PR, tag, manual, schedule, paths>

## Permissões e secrets
<análise curta>

## Gates e validações
- <gate 1>
- <gate 2>

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

- gatilhos são restritos?
- permissões são mínimas?
- secrets não aparecem em PR inseguro?
- deploy tem proteção?
- actions são confiáveis?
- versões estão controladas?
- build/test/lint estão na ordem correta?
- cache não mascara falha?
- falhas são visíveis?
- artifacts não expõem dado sensível?

---

## Critérios de escalonamento

Escalar quando:

- pipeline faz deploy;
- pipeline toca produção;
- pipeline acessa secret;
- pipeline altera infraestrutura;
- permissões são amplas;
- PR externo pode executar contexto sensível;
- alteração pode quebrar entrega do projeto.

---

## Anti-patterns

Evitar:

- `permissions: write-all`;
- deploy em todo push sem gate;
- secret em log;
- action externa sem versão;
- script grande inline sem clareza;
- pular testes para acelerar;
- cache como substituto de build correto;
- pipeline verde sem validação útil;
- CI/CD tratado como detalhe secundário.

---

## Declaração operacional curta

Pipeline é parte da produção.  
CI/CD deve validar, proteger e entregar com rastreabilidade, não apenas automatizar comandos.