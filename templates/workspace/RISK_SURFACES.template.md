# Risk Surfaces

## Finalidade

Este documento lista as superfícies de risco conhecidas do projeto.

Ele ajuda humano, Core Architect e agentes a identificar áreas que exigem cuidado, validação, review ou escalonamento.

---

## Regra central

Risco conhecido deve ser visível antes da execução.

Se uma task tocar uma superfície listada aqui, o agente deve considerar skills, policies e validações proporcionais.

---

## Classes de risco usadas

```text
R0 — leitura/investigação sem mutação
R1 — mudança local pequena
R2 — mudança funcional relevante
R3 — mudança estrutural/sensível
R4 — produção, segredo, irreversibilidade ou alto risco
```

---

## Superfícies técnicas

| Área | Risco | Classe provável | Observações |
|------|-------|-----------------|-------------|
| `<área>` | `<risco>` | `<R1-R4>` | `<observação>` |

Exemplos:

| Área | Risco | Classe provável | Observações |
|------|-------|-----------------|-------------|
| Auth | IDOR, sessão, token, autorização | R3 | Exige authn/authz review |
| Database schema | perda de dado, lock, rollback | R3/R4 | Exige migration/schema review |
| CI/CD | deploy indevido, segredo, permissão | R3/R4 | Exige pipeline review |
| Cloud config | exposição pública, RBAC, custo | R3/R4 | Exige IaC/cloud review |

---

## Superfícies de segurança

- autenticação;
- autorização;
- dados pessoais/sensíveis;
- multi-tenant;
- upload/download;
- API pública;
- webhook;
- CORS;
- secrets;
- logs;
- dependências externas;
- IaC;
- pipeline.

Detalhes locais:

```text
<descrever riscos específicos>
```

---

## Superfícies de dados

- migrations;
- schema changes;
- seeds;
- backfills;
- deletes;
- updates em massa;
- constraints;
- índices;
- transações;
- isolamento;
- integridade referencial.

Detalhes locais:

```text
<descrever riscos específicos>
```

---

## Superfícies operacionais

- deploy;
- runtime;
- health checks;
- observabilidade;
- filas;
- jobs;
- workers;
- autoscaling;
- cloud cost;
- rollback;
- ambientes;
- configuração.

Detalhes locais:

```text
<descrever riscos específicos>
```

---

## Superfícies arquiteturais

- boundaries de módulo;
- dependências entre camadas;
- abstrações novas;
- mensageria;
- CQRS;
- event sourcing;
- microserviços;
- runtime cloud;
- refactor estrutural.

Detalhes locais:

```text
<descrever riscos específicos>
```

---

## Superfícies de frontend

- renderização de conteúdo externo;
- XSS;
- tokens no cliente;
- autorização só na UI;
- estado global;
- data fetching;
- exposição de dados;
- formulários;
- upload.

Detalhes locais:

```text
<descrever riscos específicos>
```

---

## Superfícies de dependência/supply chain

| Dependência/ferramenta | Risco | Observação |
|------------------------|-------|------------|
| `<item>` | `<risco>` | `<observação>` |

---

## Sinais de escalonamento

Escalar quando:

- risco subir para R3/R4;
- houver produção;
- houver segredo;
- houver dado real;
- houver alteração estrutural;
- houver decisão arquitetural;
- houver validação insuficiente;
- houver conflito entre sources;
- houver alteração irreversível.

---

## Skills recomendadas por superfície

| Superfície | Skills recomendadas |
|-----------|---------------------|
| Auth | `authn-authz-review`, `secure-coding-baseline` |
| API | `api-abuse-and-input-validation`, `aspnet-endpoint-review`, `http-api-contract-debugging` |
| Banco | `postgres-schema-change-safety`, `postgres-query-review`, `efcore-migrations-safety` |
| Deploy | `azure-delivery-reviewer`, `ci-cd-pipeline-review`, `iac-security-review` |
| Arquitetura | `architecture-by-pain-check`, `architecture-tradeoff-analyst`, `architect-critic` |
| Frontend | `frontend-security-baseline`, `react-component-architecture`, `react-state-and-boundary-review` |

Adicionar mappings locais:

| Superfície | Skills recomendadas |
|-----------|---------------------|
| `<superfície>` | `<skills>` |

---

## Riscos atualmente aceitos

| ID | Risco | Por que aceito | Critério de revisão |
|----|-------|----------------|---------------------|
| `<id>` | `<risco>` | `<motivo>` | `<critério>` |

---

## Última atualização

```text
Data:
Autor:
Motivo:
```