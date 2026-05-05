# Checklist — Plan Review

## Finalidade

Este checklist revisa um Execution Plan antes de qualquer mutação relevante.

Ele deve garantir que o plano é claro, proporcional, validável e seguro o suficiente para o `implementer`.

---

## Identificação

```text
Projeto:
Task/Issue:
Execution Plan:
Reviewer:
Data:
Classe de risco:
```

---

## 1. Objetivo e escopo

Verificar:

- [ ] objetivo está claro;
- [ ] escopo dentro/fora está explícito;
- [ ] critérios de aceite foram considerados;
- [ ] plano não mistura tasks;
- [ ] plano não inclui refactor lateral;
- [ ] plano não expande demanda sem justificativa.

Problemas:

```text
<problemas>
```

---

## 2. Discovery

Verificar:

- [ ] topologia relevante foi identificada;
- [ ] arquivos/áreas prováveis foram listados;
- [ ] authority sources foram consultadas;
- [ ] comandos locais foram procurados;
- [ ] riscos locais foram considerados;
- [ ] board/issue não foi usado como verdade técnica única.

Lacunas:

```text
<lacunas>
```

---

## 3. Classe de risco

Verificar:

- [ ] classe de risco foi atribuída;
- [ ] justificativa é coerente;
- [ ] sinais de elevação foram declarados;
- [ ] risco não foi rebaixado sem evidência;
- [ ] R3/R4 foi tratado com escalonamento adequado.

Veredito de risco:

```text
<correto | ajustar para R... | incerto>
```

---

## 4. Architecture by pain

Verificar:

- [ ] plano evita abstração sem dor real;
- [ ] dependências novas são justificadas;
- [ ] camadas novas são justificadas;
- [ ] não há CQRS/mensageria/microserviço/runtime complexo sem dor;
- [ ] alternativa mais simples foi considerada;
- [ ] custo cognitivo e operacional foi considerado.

Sinais de over-engineering:

```text
<sinais ou nenhum>
```

---

## 5. Segurança

Verificar se o plano considera, quando aplicável:

- [ ] input externo;
- [ ] autenticação;
- [ ] autorização;
- [ ] dados sensíveis;
- [ ] secrets/config;
- [ ] dependências;
- [ ] frontend security;
- [ ] API abuse;
- [ ] IaC/cloud;
- [ ] logs.

Lacunas de segurança:

```text
<lacunas>
```

---

## 6. Produção e operação

Verificar se o plano considera:

- [ ] runtime;
- [ ] deploy;
- [ ] banco/migrations;
- [ ] observabilidade;
- [ ] falha parcial;
- [ ] rollback/mitigação;
- [ ] config por ambiente;
- [ ] CI/CD;
- [ ] custo/capacidade, se aplicável.

Lacunas operacionais:

```text
<lacunas>
```

---

## 7. Validação

Verificar:

- [ ] comandos de validação estão definidos;
- [ ] comandos vêm de `LOCAL_COMMANDS.md` ou fonte local;
- [ ] build/test/lint/format foram considerados;
- [ ] validação funcional foi definida;
- [ ] validação de segurança/produção foi definida quando aplicável;
- [ ] lacunas esperadas foram declaradas.

Validação suficiente?

```text
<sim | não | parcial>
```

---

## 8. Skills

Verificar:

- [ ] skills relevantes foram selecionadas;
- [ ] skill de stack foi usada quando o problema é específico;
- [ ] skill de engineering foi usada quando o problema é transversal;
- [ ] skill de security foi usada quando há risco;
- [ ] skill de hygiene foi considerada para drift/state/docs.

Skills faltantes:

```text
<skills>
```

---

## 9. Sinais de escalonamento

Verificar:

- [ ] sinais de escalonamento estão explícitos;
- [ ] plano manda pausar se risco subir;
- [ ] decisão arquitetural não foi empurrada para o implementer;
- [ ] produção/segredo/dado real exigem autorização.

---

## 10. Veredito

Escolher:

- [ ] aprovado;
- [ ] aprovado com ressalvas;
- [ ] reavaliar;
- [ ] bloquear.

Justificativa:

```text
<justificativa>
```

Ações obrigatórias antes da execução:

- `<ação 1>`;
- `<ação 2>`.

Ações recomendadas:

- `<ação 1>`;
- `<ação 2>`.