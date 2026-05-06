# Project Board Permissions — OpenCode

## Finalidade

Este arquivo define permissões específicas para uso de GitHub Projects, boards, issues e status de trabalho pelo OpenCode.

A regra padrão é leitura.

O board orienta coordenação, não define verdade técnica.

---

## Regra central

```text
GitHub Projects organiza trabalho.
PROJECT_STATE.md preserva verdade técnica.
```

O OpenCode pode ler o board para entender contexto, mas não deve alterar o board sem autorização explícita.

---

## Fonte canônica

Fontes principais:

```text
core/policies/03-mcp-policy.md
core/policies/10-project-state-vs-board-policy.md
core/policies/07-trusted-integrations-policy.md
core/protocols/12-external-state-reading.md
skills/integration/github-projects-readonly/SKILL.md
adapters/opencode/mcp/github-projects.md
```

---

## Modo padrão

```text
read-only
```

---

## Operações permitidas

Permitido em modo read-only:

```text
listar board
ler item
ler status
ler prioridade
ler campos
ler labels
ler milestone
ler issue vinculada
ler PR vinculado
ler comentários relevantes
resumir contexto
identificar dependências
identificar bloqueios
```

---

## Operações proibidas sem autorização explícita

```text
mover card
alterar status
alterar prioridade
editar campo
criar item
deletar item
arquivar item
aplicar label
remover label
fechar issue
reabrir issue
comentar issue
comentar PR
atribuir responsável
alterar milestone
```

---

## Quem pode ler o board

| Agente | Pode ler board? | Condição |
|--------|------------------|----------|
| planner | sim | quando board ajudar a planejar task |
| researcher | sim | quando a pergunta de investigação depender do board |
| implementer | limitado | apenas se o Execution Plan exigir contexto do item |
| reviewer | sim | quando revisar aderência a issue/PR/status |
| architect-critic | limitado | quando board contiver discussão arquitetural relevante |
| delivery-prep | sim | para sugerir atualização de status/handoff |
| mcp-observer | sim | agente principal para leitura board via MCP |

---

## Quem pode escrever no board

Por padrão:

```text
nenhum agente
```

Escrita só com autorização explícita humana.

Mesmo com autorização, a ação deve ser específica:

```text
mover item X de In Progress para Review
adicionar comentário Y na issue Z
aplicar label A na issue B
```

Não aceitar autorização genérica como:

```text
arrume o board
organize tudo
atualize o projeto
mova o que precisar
```

---

## Sugestões permitidas

O OpenCode pode sugerir atualizações sem executar.

Formato recomendado:

```md
# Sugestão de atualização do board

## Item
<item/issue>

## Status atual
<status atual>

## Status sugerido
<status sugerido>

## Motivo
<justificativa factual>

## Evidência
- <commit/PR/artifact/validação>

## Lacunas
- <lacuna, se houver>

## Ação humana necessária
<ação exata>
```

---

## Status do board

Status deve ser interpretado como coordenação.

Exemplo:

| Status | Interpretação | Limite |
|--------|---------------|--------|
| Backlog | item planejado | não prova escopo pronto |
| Ready | pronto para intake | ainda exige discovery |
| In Progress | trabalho em andamento | não prova implementação correta |
| Review | precisa revisão | não prova qualidade |
| Done | marcado como concluído | não substitui validação |
| Blocked | impedimento | exige leitura do motivo |

---

## Board vs artifacts

### Board pode gerar

- Implementation Packet;
- contexto para Execution Plan;
- referência para Review Report;
- sugestão de handoff;
- follow-up.

### Board não substitui

- Execution Plan;
- Completion Packet;
- Review Report;
- ADR;
- Project State Entry;
- validação técnica.

---

## Board vs PROJECT_STATE

Board não deve receber memória técnica profunda.

`PROJECT_STATE.md` não deve receber status granular de board.

Exemplo correto:

```text
Board:
Issue #15 está em Review.

PROJECT_STATE:
Auth usa refresh token com rotação pendente; risco de sessão registrado para revisão futura.
```

Exemplo errado:

```text
PROJECT_STATE:
Issue #15 movida para Review hoje.
```

---

## Quando consultar o board

Consultar quando:

- task veio de board;
- status do item importa;
- prioridade está em dúvida;
- dependências precisam ser lidas;
- issue vinculada contém critério de aceite;
- entrega precisa sugerir próximo status;
- há divergência entre trabalho planejado e estado local.

---

## Quando não consultar o board

Não consultar quando:

- task já está clara localmente;
- board não muda decisão;
- consulta seria curiosidade;
- estado técnico está em `PROJECT_STATE.md`;
- o agente quer evitar discovery local;
- a próxima ação seria escrita não autorizada.

---

## Leitura de issue vinculada

Ao ler item de board, quando houver issue vinculada, verificar:

- título;
- descrição;
- critérios de aceite;
- comentários relevantes;
- labels;
- links para PR/ADR/docs;
- bloqueios.

Mas lembrar:

```text
issue não é especificação técnica completa
```

---

## Divergência entre board e workspace

Quando houver divergência:

```text
board diz Done, mas código não confirma
board diz Backlog, mas implementação existe
issue pede algo contrário ao ADR
PROJECT_STATE indica risco que board ignora
PR está fechado, mas task aparece em progresso
```

Procedimento:

1. registrar divergência;
2. não corrigir automaticamente;
3. verificar fonte mais específica;
4. escalar se impactar decisão;
5. sugerir atualização humana.

---

## Escrita autorizada

Se houver autorização explícita para escrita no board, registrar:

```text
Autorizador:
Ação exata:
Item:
Campo:
Valor anterior:
Valor novo:
Motivo:
Evidência:
Risco:
```

Ainda assim, evitar escrita se houver ambiguidade.

---

## Critérios para mover item

Mover item só deve ser sugerido quando:

- Completion Packet existe;
- validação está registrada;
- Review Report existe quando necessário;
- lacunas estão declaradas;
- status sugerido corresponde à realidade;
- humano aprova.

---

## Critérios para fechar issue

Fechar issue é ação sensível.

Só sugerir quando:

- critérios de aceite foram atendidos;
- validação foi feita;
- review necessário foi concluído;
- PR/commit está referenciado;
- lacunas não bloqueiam;
- humano aprova.

---

## Anti-patterns

Evitar:

- mover card automaticamente;
- fechar issue automaticamente;
- usar board como fonte única;
- implementar pelo título do card;
- copiar board para `PROJECT_STATE.md`;
- tratar Done como validação;
- ignorar issue vinculada;
- comentar em PR sem autorização;
- atualizar prioridade sem decisão humana;
- sincronizar board por chute.

---

## Declaração operacional curta

O OpenCode pode observar o board.  
Para agir no board, precisa de autorização explícita e ação específica.