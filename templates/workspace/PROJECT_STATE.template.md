# Project State

## Finalidade

Este documento é a memória técnica viva do projeto.

Ele registra apenas informações duráveis que precisam sobreviver a sessões, agentes, conversas e handoffs.

`PROJECT_STATE.md` não é changelog, backlog, board, diário de sessão nem cópia de Completion Packet.

---

## Regra central

Registrar apenas o que muda o entendimento futuro do projeto.

Board responde:

```text
O que estamos fazendo?
```

`PROJECT_STATE.md` responde:

```text
Em que estado técnico o sistema está?
```

---

## Como usar

Atualizar quando houver:

- decisão técnica durável;
- mudança arquitetural;
- alteração de boundary;
- nova integração;
- mudança operacional;
- risco conhecido;
- limitação técnica;
- dívida consciente;
- comando relevante;
- divergência entre documentação e realidade;
- follow-up estrutural.

Não atualizar quando:

- a mudança for trivial;
- o detalhe pertencer apenas ao diff;
- o Completion Packet já bastar;
- a informação for efêmera;
- a entrada duplicar board/issue.

---

## Snapshot atual

```text
Status técnico geral:
Arquitetura atual:
Runtime:
Banco:
Deploy:
Observabilidade:
Riscos principais:
Limitações principais:
```

---

## Decisões ativas

| ID | Decisão | Status | Origem | Revisitar quando |
|----|---------|--------|--------|------------------|
| `DEC-001` | `<decisão>` | `<ativa | em observação | substituída>` | `<ADR/issue/commit/decisão humana>` | `<critério>` |

---

## Estado arquitetural

### Boundaries

- `<boundary 1>`;
- `<boundary 2>`;
- `<boundary 3>`.

### Regras estruturais

- `<regra 1>`;
- `<regra 2>`.

### Restrições arquiteturais

- `<restrição 1>`;
- `<restrição 2>`.

---

## Estado operacional

### Ambiente local

```text
<estado atual>
```

### Deploy

```text
<estado atual>
```

### Banco

```text
<estado atual>
```

### Observabilidade

```text
<estado atual>
```

### Integrações

```text
<estado atual>
```

---

## Riscos conhecidos

| ID | Risco | Severidade | Status | Mitigação/observação |
|----|-------|------------|--------|----------------------|
| `RISK-001` | `<risco>` | `<baixo | médio | alto>` | `<ativo | resolvido | em observação>` | `<mitigação>` |

---

## Limitações conhecidas

| ID | Limitação | Impacto | Status | Observação |
|----|-----------|---------|--------|------------|
| `LIM-001` | `<limitação>` | `<impacto>` | `<ativa | resolvida | em observação>` | `<observação>` |

---

## Dívidas conscientes

| ID | Dívida | Por que foi aceita | Critério de revisão |
|----|--------|--------------------|---------------------|
| `DEBT-001` | `<dívida>` | `<motivo>` | `<quando revisitar>` |

---

## Integrações e dependências relevantes

| Item | Função | Status | Risco |
|------|-------|--------|-------|
| `<integração/dependência>` | `<função>` | `<ativo | em revisão | planejado>` | `<risco>` |

---

## Comandos ou rotinas importantes

Não duplicar `LOCAL_COMMANDS.md` inteiro.  
Registrar apenas comandos que sejam parte de estado técnico relevante.

| Comando/rotina | Finalidade | Observação |
|----------------|------------|------------|
| `<comando>` | `<finalidade>` | `<observação>` |

---

## Follow-ups estruturais

Follow-ups aqui devem ser técnicos e duráveis, não backlog completo.

| ID | Follow-up | Motivo | Origem |
|----|-----------|--------|--------|
| `FU-001` | `<ação futura>` | `<por que importa>` | `<artifact/issue/decisão>` |

---

## Entradas recentes

Usar entradas densas, curtas e referenciadas.

### `<data | commit | issue | PR | identificador>`

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

Exemplo:

```text
Tipo: decisão
Status: ativa
Origem: ADR-0002
Área: arquitetura/backend
Resumo: O projeto permanece como monólito modular; microsserviços estão fora do escopo atual.
Impacto: Novos módulos devem respeitar boundaries internos sem criar deploy independente.
Risco: Acoplamento cruzado entre módulos deve ser auditado.
Próxima revisão: quando houver escala de time, deploy independente ou boundary operacional real.
Referências: ADR-0002, issue #12
```

---

## Entradas resolvidas/substituídas

Manter apenas o que ainda ajuda a entender histórico técnico.

| ID/Data | Entrada | Status | Substituída por |
|---------|---------|--------|-----------------|
| `<id>` | `<resumo>` | `<resolvida | substituída | obsoleta>` | `<referência>` |

---

## Última atualização

```text
Data:
Autor:
Motivo:
```