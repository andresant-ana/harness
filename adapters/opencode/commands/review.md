# OpenCode Command — review

## Finalidade

Este comando orienta o OpenCode a revisar plano, diff, Completion Packet, artifacts ou handoff.

O comando `review` não implementa.  
Ele emite parecer baseado em evidência.

---

## Agente responsável

```text
adapters/opencode/agents/reviewer.md
```

Contrato canônico:

```text
agents/reviewer.md
```

---

## Quando usar

Use este comando quando:

- houver diff relevante;
- houver Completion Packet;
- a task for R2+;
- houver risco de segurança, dados, produção ou arquitetura;
- houver suspeita de AI slop;
- houver mudança em schema, CI/CD, cloud, auth ou dependências;
- o plano precisar ser revisado antes da execução;
- o humano pedir revisão.

---

## Quando não usar

Não use este comando para:

- implementar correções;
- redesenhar solução;
- substituir Core Architect em decisão estratégica;
- aprovar sem evidência;
- bloquear por preferência estética.

---

## Inputs esperados

```text
Objeto revisado:
Execution Plan:
Diff:
Completion Packet:
Validações:
Classe de risco:
Arquivos/áreas:
```

---

## Fontes que devem ser consultadas

```text
Execution Plan
diff
Completion Packet
LOCAL_COMMANDS.md
DONE_CRITERIA.md
RISK_SURFACES.md
PROJECT_STATE.md
OPERATIONAL_REALITY.md
```

Fontes globais:

```text
core/protocols/07-review-protocol.md
core/protocols/06-evidence-standard.md
core/protocols/10-entropy-management.md
templates/packets/Review_Report.template.md
templates/checklists/Pre_Merge_Review.checklist.md
templates/checklists/Anti_Slop.checklist.md
```

---

## Skills prováveis

Acionar conforme objeto revisado:

```text
skills/orchestration/testing-verifier/SKILL.md
skills/security/secure-coding-baseline/SKILL.md
skills/hygiene/architecture-drift-auditor/SKILL.md
skills/hygiene/consistency-scanner/SKILL.md
skills/hygiene/dependency-hygiene-review/SKILL.md
skills/engineering/architecture-by-pain-check/SKILL.md
skills/engineering/performance-and-capacity-review/SKILL.md
```

Stack específica se o diff tocar stack.

---

## Processo

### 1. Identificar objeto de review

Classificar:

```text
Execution Plan
diff
Completion Packet
artifact
handoff
combinação
```

### 2. Comparar com objetivo

Verificar se a entrega:

- atende objetivo;
- respeita escopo;
- preserva fora de escopo;
- não inclui refactor lateral.

### 3. Revisar evidência

Checar:

- comandos executados;
- testes;
- build;
- lint;
- diff review;
- validações ausentes;
- lacunas declaradas.

### 4. Revisar risco

Verificar:

- classe de risco correta;
- risco residual;
- segurança;
- operação;
- banco/dados;
- produção;
- arquitetura;
- entropia.

### 5. Emitir veredito

Usar exatamente um:

```text
aprovado
aprovado com ressalvas
reavaliar
bloquear
```

---

## Output obrigatório

Produzir `Review Report` usando:

```text
templates/packets/Review_Report.template.md
```

A saída deve conter:

```text
Objeto revisado
Escopo da revisão
Veredito
Qualidade geral
Aderência ao objetivo
Aderência ao plano
Evidências revisadas
Problemas encontrados
Lacunas de evidência
Riscos remanescentes
Ações obrigatórias
Ações recomendadas
Necessita escalonamento?
Necessita Project State Entry?
```

---

## Prompt operacional sugerido

```text
Use o comando review.

Revise o objeto abaixo de forma conservadora e baseada em evidência.

Objeto:
<colar Execution Plan, diff, Completion Packet ou handoff>

Contexto:
<colar validações, comandos, issue ou observações>

Regras:
- Não implemente.
- Não aprove sem evidência.
- Verifique escopo, validação, segurança, produção, arquitetura e entropia.
- Emita veredito claro: aprovado, aprovado com ressalvas, reavaliar ou bloquear.
- Use templates/packets/Review_Report.template.md.
```

---

## Critérios de bloqueio

Bloquear se:

- objetivo não foi atendido;
- escopo foi violado;
- validação essencial está ausente;
- segredo apareceu;
- risco de dados/produção não foi tratado;
- arquitetura mudou sem aprovação;
- Completion Packet contradiz evidência;
- slop relevante foi introduzido.

---

## Critério de sucesso

O comando foi bem-sucedido quando:

- veredito é explícito;
- evidência foi revisada;
- lacunas foram declaradas;
- riscos estão visíveis;
- ações obrigatórias e recomendadas estão separadas.

---

## Anti-patterns

Evitar:

- “LGTM” sem evidência;
- review só de estilo;
- bloquear por gosto pessoal;
- aprovar teste não rodado como detalhe;
- ignorar risco residual;
- sugerir refactor lateral.