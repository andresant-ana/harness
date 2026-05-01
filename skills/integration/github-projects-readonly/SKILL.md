# Skill — GitHub Projects Read-Only

## Finalidade

Esta skill orienta a leitura segura de GitHub Projects, boards, items, status, prioridades e issues vinculadas em modo read-only.

Seu papel é ajudar o agente a entender sequência de trabalho, contexto organizacional e estado de tarefas sem confundir board com verdade técnica do projeto.

---

## Quando usar

Use esta skill quando a task precisar consultar:

- board do GitHub Projects;
- status de item;
- prioridade;
- issue vinculada;
- etapa do workflow;
- dependências entre tasks;
- escopo planejado;
- backlog;
- sequência de execução.

---

## Quando não usar

Não use esta skill quando:

- a task já estiver clara no workspace;
- o board não for fonte relevante;
- a consulta seria apenas administrativa;
- a operação exigiria mover item, mudar status ou editar issue;
- o board seria usado como substituto de `PROJECT_STATE.md`.

---

## Tese central

Board organiza trabalho.  
`PROJECT_STATE.md` preserva verdade técnica.

GitHub Projects pode dizer o que está planejado, em progresso ou priorizado.  
Ele não deve ser tratado como arquitetura, documentação técnica ou estado real do código.

---

## Método

### 1. Definir pergunta de board

Antes de consultar, declarar:

- que item precisamos entender;
- que status importa;
- que prioridade ou dependência será verificada;
- como isso afetará a task.

---

### 2. Ler item e issue vinculada

Quando houver item de board, verificar:

- título;
- descrição;
- status;
- prioridade;
- labels;
- issue vinculada;
- comentários relevantes;
- links para PR/ADR/docs.

---

### 3. Separar planejamento de realidade

Classificar informações como:

- intenção;
- prioridade;
- escopo planejado;
- decisão técnica;
- estado técnico confirmado;
- lacuna.

O board quase sempre representa intenção ou coordenação, não realidade final.

---

### 4. Verificar alinhamento com workspace

Quando o board sugerir algo técnico, validar contra:

- código;
- `PROJECT_STATE.md`;
- ADR;
- docs locais;
- commits;
- PRs.

---

### 5. Não escrever no board

Em modo read-only, o agente pode sugerir atualização, mas não executar.

Permitido:

- “sugerir mover para Review”;
- “sugerir adicionar link para PR”;
- “sugerir criar follow-up”.

Proibido sem autorização:

- mover item;
- fechar issue;
- editar status;
- alterar prioridade;
- criar item;
- comentar.

---

## Output esperado

```md
# GitHub Projects Read-Only Note

## Pergunta
<o que precisava ser entendido no board>

## Item/issue consultado
<referência>

## Estado no board
<status, prioridade, labels ou etapa>

## Achados relevantes
- <achado 1>
- <achado 2>

## Separação board vs verdade técnica
<o que é coordenação e o que é fato técnico>

## Implicação para a task
<como isso orienta o próximo passo>

## Sugestão de atualização
<nenhuma | sugestão read-only para humano>

## Veredito
<suficiente | checar workspace | investigar mais | escalar>
```

---

## Checklist de qualidade

Antes de concluir, verificar:

- a pergunta de board estava clara?
- item correto foi consultado?
- issue vinculada foi lida quando relevante?
- status foi separado de estado técnico real?
- board não substituiu `PROJECT_STATE.md`?
- workspace foi considerado quando necessário?
- nenhuma escrita foi feita?
- sugestão de atualização foi deixada para humano?

---

## Critérios de escalonamento

Escalar quando:

- board e `PROJECT_STATE.md` divergirem;
- issue estiver vaga demais para implementação;
- prioridade depender de decisão humana;
- item sugerir risco R3/R4;
- board indicar trabalho bloqueado;
- o próximo passo exigiria atualização remota.

---

## Anti-patterns

Evitar:

- tratar card como specification completa;
- copiar board para `PROJECT_STATE.md`;
- mover status automaticamente;
- fechar issue sem autorização;
- implementar só pelo título do card;
- ignorar comentários técnicos da issue;
- transformar backlog em documentação técnica;
- confundir “Done” no board com validação real.

---

## Declaração operacional curta

GitHub Projects orienta coordenação.  
O harness pode ler o board, mas a verdade técnica continua no código, artifacts, ADRs e `PROJECT_STATE.md`.