# Execution Plan

## Finalidade

Este artifact define o plano de execução antes de qualquer mutação relevante.

Ele deve ser específico o suficiente para guiar o `implementer`, revisável pelo humano/Core Architect e proporcional à classe de risco.

---

## Identificação

```text
Projeto:
Task/Issue:
Origem:
Planner:
Data:
Classe de risco: <R0 | R1 | R2 | R3 | R4>
Status do plano: <rascunho | pronto para revisão | aprovado | bloqueado>
```

---

## Objetivo

```text
<leitura consolidada da task>
```

---

## Contexto relevante

```text
<contexto técnico, produto, operacional ou arquitetural necessário>
```

---

## Classe de risco

```text
Classe: <R0 | R1 | R2 | R3 | R4>
Justificativa: <por que essa classe foi atribuída>
```

### Sinais que podem elevar risco

- `<sinal 1>`;
- `<sinal 2>`.

---

## Discovery realizado

### Topologia relevante

- `<topologia relevante>`;
- `<módulo/diretório/arquivo>`.

### Authority sources consultadas

- `<authority source 1>`;
- `<authority source 2>`.

### Áreas afetadas

- `<área afetada 1>`;
- `<área afetada 2>`.

### Sensibilidades

- `<segurança | banco | arquitetura | cloud | operação | outro>`;
- `<sensibilidade 2>`.

---

## Escopo

### Dentro do escopo

- `<item 1>`;
- `<item 2>`.

### Fora do escopo

- `<item 1>`;
- `<item 2>`.

---

## Abordagem escolhida

```text
<abordagem escolhida e rationale>
```

### Por que esta abordagem

- `<motivo 1>`;
- `<motivo 2>`.

### Alternativas consideradas

| Alternativa | Benefício | Custo/Risco | Motivo de rejeição |
|------------|-----------|-------------|--------------------|
| `<alternativa>` | `<benefício>` | `<risco>` | `<motivo>` |

---

## Architecture by pain

### Dor real que justifica a solução

```text
<dor atual, evidência ou necessidade real>
```

### Abstrações novas

- [ ] Nenhuma;
- [ ] Sim, listadas abaixo.

| Abstração | Dor que justifica | Alternativa simples considerada |
|----------|-------------------|---------------------------------|
| `<abstração>` | `<dor>` | `<alternativa>` |

---

## Plano de execução

1. `<etapa 1>`;
2. `<etapa 2>`;
3. `<etapa 3>`;
4. `<etapa 4>`.

---

## Arquivos/áreas prováveis

- `<área ou arquivo 1>`;
- `<área ou arquivo 2>`.

---

## Skills acionadas

- `<skill 1>`;
- `<skill 2>`.

---

## Validação planejada

### Comandos

```bash
<comando 1>
<comando 2>
```

### Checagens

- `<validação 1>`;
- `<validação 2>`.

### Evidência esperada

- `<evidência 1>`;
- `<evidência 2>`.

---

## Segurança

```text
<como input, auth, secrets, dados sensíveis, dependências ou cloud serão tratados>
```

---

## Produção e operação

```text
<impacto operacional, observabilidade, config, deploy, runtime ou banco>
```

---

## Riscos e mitigação

| Risco | Impacto | Mitigação |
|------|---------|-----------|
| `<risco 1>` | `<impacto>` | `<mitigação>` |
| `<risco 2>` | `<impacto>` | `<mitigação>` |

---

## Lacunas conhecidas

- `<lacuna 1>`;
- `<lacuna 2>`.

---

## Sinais de escalonamento

Parar e escalar se ocorrer:

- `<sinal 1>`;
- `<sinal 2>`;
- `<sinal 3>`.

---

## Artifact de saída esperado

```text
<Completion Packet | Review Report | Escalation Note | outro>
```

---

## Aprovação

```text
Status: <pendente | aprovado | aprovado com ressalvas | rejeitado>
Aprovador:
Data:
Observações:
```