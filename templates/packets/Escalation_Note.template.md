# Escalation Note

## Finalidade

Este artifact registra uma pausa formal por risco, ambiguidade, decisão estratégica, ausência de autorização ou limite de autonomia.

Ele deve deixar claro por que o agente não deve seguir sozinho.

---

## Identificação

```text
Projeto:
Task/Issue:
Origem:
Agente:
Data:
Classe de risco atual: <R0 | R1 | R2 | R3 | R4>
Escalar para: <humano | Core Architect | reviewer | dono do projeto | outro>
```

---

## Situação

```text
<situação em que a escalada surgiu>
```

---

## Motivo da escalada

```text
<por que o executor não deve seguir sozinho>
```

---

## Tipo de escalada

Marcar todos que se aplicam:

- [ ] risco subiu;
- [ ] decisão arquitetural;
- [ ] ambiguidade de escopo;
- [ ] conflito entre authority sources;
- [ ] produção;
- [ ] segredo;
- [ ] dado real;
- [ ] operação destrutiva;
- [ ] dependência nova sensível;
- [ ] mudança de schema;
- [ ] mudança de cloud/runtime;
- [ ] validação essencial indisponível;
- [ ] issue/board insuficiente;
- [ ] outro.

---

## Evidências

- `<fonte 1>`;
- `<fonte 2>`.

---

## Impacto potencial

- `<impacto 1>`;
- `<impacto 2>`.

---

## Opções identificadas

| Opção | Benefício | Custo/Risco | Observação |
|------|-----------|-------------|------------|
| `<opção 1>` | `<benefício>` | `<risco>` | `<observação>` |
| `<opção 2>` | `<benefício>` | `<risco>` | `<observação>` |

---

## Trade-offs

- `<trade-off 1>`;
- `<trade-off 2>`.

---

## Riscos se seguir sem decisão

- `<risco 1>`;
- `<risco 2>`.

---

## Riscos se adiar

```text
<efeito provável do adiamento>
```

---

## Recomendação

```text
<recomendação, se houver base suficiente>
```

---

## Pergunta exata para arbitragem

```text
<pergunta exata que precisa de decisão>
```

---

## O que está bloqueado

- `<item bloqueado 1>`;
- `<item bloqueado 2>`.

---

## O que ainda pode avançar com segurança

- `<item seguro 1>`;
- `<item seguro 2>`.

---

## Decisão recebida

Preencher depois da arbitragem.

```text
Decisão:
Decisor:
Data:
Condições:
```

---

## Próximo passo após decisão

```text
<retomar plano | revisar plan | criar ADR | atualizar PROJECT_STATE | cancelar | outro>
```