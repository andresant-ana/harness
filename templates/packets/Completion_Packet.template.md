# Completion Packet

## Finalidade

Este artifact formaliza o fechamento de uma execução.

Ele deve registrar o que foi feito, como foi validado, quais lacunas restaram, quais riscos permanecem e qual é o próximo passo.

Não é propaganda da entrega.  
É handoff técnico factual.

---

## Identificação

```text
Projeto:
Task/Issue:
Execution Plan:
Implementer:
Data:
Classe de risco final: <R0 | R1 | R2 | R3 | R4>
Status: <concluído | concluído com ressalvas | bloqueado | parcial>
```

---

## Objetivo original

```text
<objetivo da task>
```

---

## Resultado

```text
<resumo objetivo da mudança>
```

---

## Mudanças realizadas

- `<item 1>`;
- `<item 2>`;
- `<item 3>`.

---

## Arquivos/áreas tocadas

- `<área ou arquivo 1>`;
- `<área ou arquivo 2>`.

---

## Escopo

### Dentro do escopo realizado

- `<item 1>`;
- `<item 2>`.

### Fora do escopo preservado

- `<item 1>`;
- `<item 2>`.

---

## Divergências do Execution Plan

- [ ] Nenhuma;
- [ ] Sim, descritas abaixo.

| Divergência | Motivo | Impacto |
|------------|--------|---------|
| `<divergência>` | `<motivo>` | `<impacto>` |

---

## Validações executadas

### Comandos

```bash
<comando executado>
```

### Resultado

```text
<resultado resumido>
```

### Checagens manuais/técnicas

- `<validação 1>`;
- `<validação 2>`.

---

## Validações não executadas

| Validação | Motivo | Risco |
|----------|--------|-------|
| `<validação>` | `<motivo>` | `<risco>` |

---

## Evidência

- `<evidência 1>`;
- `<evidência 2>`.

---

## Segurança

```text
<o que foi considerado sobre input, auth, secrets, dados, dependências, frontend, IaC ou cloud>
```

---

## Produção e operação

```text
<impacto operacional, observabilidade, runtime, config, deploy, banco ou lacunas>
```

---

## Riscos remanescentes

- `<risco 1>`;
- `<risco 2>`.

---

## Lacunas

- `<lacuna 1>`;
- `<lacuna 2>`.

---

## Impacto em documentação/state

### PROJECT_STATE.md

```text
<não precisa | precisa | incerto>
Motivo: <motivo>
```

### ADR

```text
<não precisa | precisa | incerto>
Motivo: <motivo>
```

### Outros documentos

- `<documento 1>`;
- `<documento 2>`.

---

## Sugestão de Project State Entry

Preencher apenas se houver mudança técnica durável.

```text
Tipo:
Status:
Origem:
Área:
Resumo:
Impacto:
Risco:
Próxima revisão:
Referências:
```

---

## Sugestão de commit

```text
<mensagem causal de commit>
```

---

## Próxima ação recomendada

```text
<review | commit | PR | nova task | escalonamento | atualizar state | outro>
```

---

## Observações finais

```text
<observações factuais, sem narrativa triunfalista>
```