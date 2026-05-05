# Checklist — Task Intake

## Finalidade

Este checklist transforma uma demanda inicial em entrada clara para investigação, planejamento ou implementação.

Ele deve ser usado antes de criar um Implementation Packet ou Execution Plan, principalmente quando a task ainda está vaga.

---

## Identificação

```text
Projeto:
Task/Issue:
Origem:
Solicitante:
Data:
```

---

## 1. Objetivo

A demanda deixa claro:

- [ ] o que precisa ser resolvido;
- [ ] por que isso importa;
- [ ] qual resultado esperado;
- [ ] quem será impactado;
- [ ] qual problema atual existe.

Resumo:

```text
<objetivo consolidado>
```

---

## 2. Tipo de task

Marcar:

- [ ] investigação;
- [ ] bugfix;
- [ ] feature;
- [ ] refactor;
- [ ] documentação;
- [ ] teste;
- [ ] infraestrutura;
- [ ] CI/CD;
- [ ] segurança;
- [ ] performance;
- [ ] arquitetura;
- [ ] release;
- [ ] outro.

---

## 3. Classe de risco inicial

```text
<R0 | R1 | R2 | R3 | R4 | incerta>
```

Justificativa:

```text
<por que esta classe foi atribuída>
```

Sinais de risco:

- [ ] produção;
- [ ] segredo;
- [ ] dado real;
- [ ] auth/authz;
- [ ] banco/schema;
- [ ] CI/CD;
- [ ] cloud/IaC;
- [ ] dependência nova;
- [ ] mudança estrutural;
- [ ] integração externa;
- [ ] performance crítica;
- [ ] operação destrutiva.

---

## 4. Escopo

### Dentro do escopo

- `<item 1>`;
- `<item 2>`.

### Fora do escopo

- `<item 1>`;
- `<item 2>`.

Se o fora do escopo não estiver claro, registrar lacuna.

---

## 5. Critérios de aceite

A task tem critérios de aceite?

- [ ] sim;
- [ ] não;
- [ ] parcial.

Critérios:

- `<critério 1>`;
- `<critério 2>`.

---

## 6. Fontes de autoridade

Consultar ou apontar:

- [ ] `WORKSPACE_GUIDE.md`;
- [ ] `PROJECT_CONTEXT.md`;
- [ ] `AUTHORITY_SOURCES.md`;
- [ ] `LOCAL_COMMANDS.md`;
- [ ] `PROJECT_STATE.md`;
- [ ] `DONE_CRITERIA.md`;
- [ ] `RISK_SURFACES.md`;
- [ ] `OPERATIONAL_REALITY.md`;
- [ ] issue/board item;
- [ ] ADR;
- [ ] documentação local;
- [ ] código/testes.

Fontes relevantes:

```text
<fontes>
```

---

## 7. Contexto externo

É necessário consultar algo fora do workspace?

- [ ] não;
- [ ] GitHub Projects;
- [ ] issue/PR;
- [ ] documentação oficial;
- [ ] cloud read-only;
- [ ] observabilidade read-only;
- [ ] outro.

Pergunta externa exata:

```text
<pergunta>
```

---

## 8. Dúvidas abertas

- `<dúvida 1>`;
- `<dúvida 2>`.

Classificação:

```text
Essas dúvidas bloqueiam? <sim | não | parcial>
```

---

## 9. Necessidade de artifacts

Marcar:

- [ ] Investigation Note;
- [ ] Implementation Packet;
- [ ] Execution Plan;
- [ ] Completion Packet;
- [ ] Review Report;
- [ ] Escalation Note;
- [ ] ADR;
- [ ] Project State Entry.

Justificativa:

```text
<justificativa>
```

---

## 10. Skills prováveis

- `<skill 1>`;
- `<skill 2>`;
- `<skill 3>`.

---

## 11. Sinais de escalonamento

Escalar se:

- [ ] classe subir para R3/R4;
- [ ] escopo estiver ambíguo;
- [ ] issue for insuficiente;
- [ ] houver conflito entre fontes;
- [ ] houver decisão arquitetural;
- [ ] houver segredo/produção;
- [ ] validação essencial não existir;
- [ ] risco de dados ou segurança aparecer.

---

## 12. Decisão de encaminhamento

Escolher:

- [ ] seguir para Investigation Note;
- [ ] seguir para Implementation Packet;
- [ ] seguir para Execution Plan;
- [ ] escalar antes de planejar;
- [ ] rejeitar/adiar por falta de informação;
- [ ] dividir em tasks menores.

Motivo:

```text
<decisão e motivo>
```