# ADR — <título da decisão>

## Status

```text
<proposta | aceita | rejeitada | substituída | obsoleta | em revisão>
```

## Data

```text
<YYYY-MM-DD>
```

## Decisores

- `<nome/papel>`;
- `<nome/papel>`.

## Contexto

Descrever o cenário que motivou a decisão.

Incluir:

- problema atual;
- restrições relevantes;
- estado técnico do sistema;
- riscos existentes;
- pressão de produto, operação ou arquitetura;
- relação com issues, PRs, incidents, artifacts ou `PROJECT_STATE.md`.

```text
<contexto da decisão>
```

---

## Dor real

Qual dor concreta justifica esta decisão?

A decisão deve responder a uma pressão observável, não a uma antecipação abstrata.

Exemplos de dor real:

- acoplamento já causando dificuldade;
- regra duplicada já divergindo;
- contrato externo instável poluindo domínio;
- volume/carga exigindo mudança;
- risco operacional observado;
- boundary contaminado;
- deploy/observabilidade/segurança insuficientes;
- manutenção recorrente ficando cara.

```text
<dor real observada>
```

---

## Decisão

Registrar a decisão de forma direta.

```text
<decisão tomada>
```

---

## Escopo da decisão

### Dentro do escopo

- `<item 1>`;
- `<item 2>`.

### Fora do escopo

- `<item 1>`;
- `<item 2>`.

---

## Opções consideradas

| Opção | Descrição | Benefícios | Custos/Riscos | Motivo de aceitar/rejeitar |
|------|-----------|------------|---------------|----------------------------|
| `<opção 1>` | `<descrição>` | `<benefícios>` | `<custos/riscos>` | `<motivo>` |
| `<opção 2>` | `<descrição>` | `<benefícios>` | `<custos/riscos>` | `<motivo>` |
| `<opção 3>` | `<descrição>` | `<benefícios>` | `<custos/riscos>` | `<motivo>` |

---

## Alternativa mais simples considerada

Toda decisão arquitetural relevante deve registrar a alternativa mais simples avaliada.

```text
<qual era a alternativa mais simples e por que ela foi aceita ou rejeitada>
```

---

## Trade-offs

### Benefícios esperados

- `<benefício 1>`;
- `<benefício 2>`;
- `<benefício 3>`.

### Custos introduzidos

- `<custo cognitivo>`;
- `<custo operacional>`;
- `<custo de manutenção>`;
- `<custo de contexto para agentes>`;
- `<custo de teste/validação>`.

### Riscos aceitos

- `<risco 1>`;
- `<risco 2>`.

### Riscos mitigados

- `<risco mitigado 1>`;
- `<risco mitigado 2>`.

---

## Impacto arquitetural

Descrever como a decisão afeta:

```text
Módulos:
Boundaries:
Dependências:
Banco:
Runtime:
Cloud/infra:
Segurança:
Observabilidade:
CI/CD:
Testes:
Documentação:
```

---

## Impacto operacional

Descrever impacto em:

- deploy;
- rollback;
- observabilidade;
- configuração;
- secrets;
- ambientes;
- custo;
- suporte;
- incidentes;
- runbooks.

```text
<impacto operacional>
```

---

## Impacto em segurança

```text
<impacto em autenticação, autorização, dados sensíveis, secrets, supply chain, rede, cloud, frontend ou API>
```

---

## Consequências

### Consequências positivas

- `<consequência 1>`;
- `<consequência 2>`.

### Consequências negativas

- `<consequência 1>`;
- `<consequência 2>`.

### Consequências neutras ou aceitas

- `<consequência 1>`;
- `<consequência 2>`.

---

## Plano de aplicação

```text
<como a decisão será aplicada>
```

Passos:

1. `<passo 1>`;
2. `<passo 2>`;
3. `<passo 3>`.

---

## Critério de validação

Como saberemos que a decisão funcionou?

- `<sinal 1>`;
- `<sinal 2>`;
- `<sinal 3>`.

Validações possíveis:

```bash
<comando ou validação>
```

---

## Critério de revisão futura

Quando esta decisão deve ser reavaliada?

Exemplos:

- segunda ocorrência real;
- aumento de carga;
- mudança de time;
- mudança de runtime;
- incidente;
- custo operacional acima do esperado;
- boundary voltando a doer;
- dependência externa mudando.

```text
<critério de revisão>
```

---

## Relação com PROJECT_STATE

Esta ADR altera memória técnica durável?

```text
<sim | não | incerto>
```

Entrada sugerida para `PROJECT_STATE.md`, se aplicável:

```text
Tipo: decisão
Status: ativa
Origem: ADR-<número>
Área:
Resumo:
Impacto:
Risco:
Próxima revisão:
Referências:
```

---

## Relação com artifacts

Referências:

- Implementation Packet: `<referência>`;
- Execution Plan: `<referência>`;
- Investigation Note: `<referência>`;
- Review Report: `<referência>`;
- Escalation Note: `<referência>`;
- Completion Packet: `<referência>`.

---

## Referências

- `<issue/PR/commit/link/doc>`;
- `<ADR relacionada>`;
- `<arquivo local>`;
- `<fonte externa confiável, se houver>`.

---

## Decisão final

```text
<decisão final objetiva>
```