# Done Criteria

## Finalidade

Este documento define critérios locais de pronto para tasks neste projeto.

Ele evita que uma entrega seja considerada concluída apenas porque “o código foi escrito”.

---

## Regra central

Task pronta precisa de evidência proporcional ao risco.

A conclusão deve demonstrar:

- objetivo atendido;
- escopo respeitado;
- validação executada;
- riscos declarados;
- lacunas registradas;
- documentação/state considerados;
- handoff claro.

---

## Critério mínimo para qualquer task

Uma task só pode ser encerrada quando:

- objetivo está claro;
- escopo realizado corresponde ao pedido;
- fora de escopo não foi alterado;
- diff é revisável;
- não há segredo no diff;
- validação proporcional foi feita ou lacuna foi declarada;
- Completion Packet ou handoff foi produzido quando necessário.

---

## Critérios por classe de risco

### R0 — leitura/investigação

Pronto quando:

- pergunta investigada foi respondida;
- fontes foram registradas;
- fatos foram separados de hipóteses;
- lacunas foram declaradas;
- próxima ação está clara.

Artifact esperado:

- Investigation Note, quando relevante.

---

### R1 — mudança local pequena

Pronto quando:

- mudança é localizada;
- build/test/lint relevante foi considerado;
- diff não contém ruído;
- não há impacto estrutural;
- Completion Packet simples foi produzido quando necessário.

---

### R2 — mudança funcional relevante

Pronto quando:

- Execution Plan existiu ou foi implicitamente aprovado;
- critérios de aceite foram cobertos;
- testes/build/lint relevantes foram executados;
- segurança básica foi considerada;
- impacto em documentação/state foi avaliado;
- Completion Packet foi produzido;
- review é recomendado.

---

### R3 — mudança estrutural/sensível

Pronto quando:

- plano foi aprovado;
- decisão arquitetural foi validada;
- riscos foram explicitados;
- validações fortes foram executadas;
- review obrigatório foi realizado;
- ADR ou Project State Entry foi considerado;
- lacunas não bloqueantes foram aceitas conscientemente.

---

### R4 — produção, segredo, irreversibilidade ou alto risco

Pronto somente com:

- autorização explícita;
- plano de execução;
- plano de rollback/mitigação;
- validação em ambiente seguro;
- review humano/Core Architect;
- evidência robusta;
- registro de risco;
- handoff completo.

---

## Critérios técnicos

### Build

```text
Comando:
Obrigatório quando:
Pode ser dispensado quando:
```

### Testes

```text
Comando:
Obrigatório quando:
Pode ser dispensado quando:
```

### Lint/format/typecheck

```text
Comando:
Obrigatório quando:
Pode ser dispensado quando:
```

### Segurança

Obrigatório considerar quando houver:

- input externo;
- auth;
- dados sensíveis;
- secrets;
- dependência nova;
- API;
- frontend com dados;
- cloud/IaC.

### Observabilidade

Obrigatório considerar quando houver:

- endpoint relevante;
- integração;
- job/worker;
- deploy;
- falha parcial;
- runtime cloud;
- fluxo crítico.

---

## Critérios documentais

Atualizar ou considerar:

- `PROJECT_STATE.md`, se houve mudança durável;
- ADR, se houve decisão arquitetural;
- `LOCAL_COMMANDS.md`, se comando mudou;
- `OPERATIONAL_REALITY.md`, se realidade operacional mudou;
- `AUTHORITY_SOURCES.md`, se nova fonte de autoridade surgiu;
- README/docs, se comportamento documentado mudou.

Não atualizar docs por ritual.

---

## Critérios de handoff

Handoff deve conter:

- o que foi feito;
- onde foi feito;
- como foi validado;
- o que não foi validado;
- riscos remanescentes;
- próximos passos;
- sugestão de commit/PR, se aplicável.

---

## Checklist pré-commit

Antes de commit:

```bash
git status
git diff --stat
git diff --check
```

Confirmar:

- arquivos esperados;
- sem segredo;
- sem ruído;
- sem escopo misturado;
- validações registradas;
- mensagem de commit causal.

---

## Motivos aceitáveis para lacuna

Uma lacuna pode ser aceita quando:

- ambiente não existe;
- comando local está quebrado antes da task;
- validação exigiria produção;
- teste depende de serviço externo indisponível;
- custo é desproporcional ao risco;
- humano/Core Architect aceitou.

A lacuna deve ser registrada.

---

## Motivos de bloqueio

Bloquear quando:

- objetivo não foi atendido;
- validação essencial faltou;
- segredo apareceu;
- produção foi tocada sem autorização;
- risco R3/R4 não foi escalado;
- schema/data foram alterados sem plano;
- arquitetura mudou sem decisão;
- diff mistura escopos incompatíveis.

---

## Última atualização

```text
Data:
Autor:
Motivo:
```