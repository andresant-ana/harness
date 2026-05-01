# Skill — GitHub Read-Only Ops

## Finalidade

Esta skill orienta a leitura segura de repositórios, commits, branches, pull requests, issues e arquivos no GitHub em modo read-only.

Seu papel é permitir inspeção factual do estado remoto sem confundir GitHub com o workspace local, sem mutação remota e sem substituir review local.

---

## Quando usar

Use esta skill quando a task precisar consultar:

- repositório remoto;
- arquivos no GitHub;
- commits recentes;
- histórico;
- branches;
- PRs;
- issues;
- comentários;
- diffs remotos;
- status de CI;
- estado remoto para auditoria ou comparação.

---

## Quando não usar

Não use esta skill quando:

- o workspace local já contém a informação mais atual;
- a task exige mutação remota;
- o GitHub remoto não é fonte relevante para a decisão;
- a consulta não tem pergunta clara;
- a leitura do remoto substituiria revisão do diff local.

---

## Tese central

GitHub remoto é fonte de contexto, não substituto automático do workspace.

O agente deve saber diferenciar:

- estado local;
- estado remoto;
- branch atual;
- branch default;
- PR;
- issue;
- commit;
- artifact de CI.

---

## Método

### 1. Definir objetivo da leitura

Declarar:

- o que será consultado;
- por que o remoto importa;
- qual branch/ref interessa;
- qual decisão depende dessa leitura.

---

### 2. Identificar ref correta

Antes de concluir algo, confirmar:

- repositório;
- branch;
- commit;
- PR;
- issue;
- data ou ordem temporal.

Evitar assumir que `main` representa o workspace local.

---

### 3. Ler com escopo

Preferir consulta específica:

- arquivo específico;
- commit específico;
- PR específico;
- issue específica;
- diff específico.

Evitar varredura ampla sem necessidade.

---

### 4. Separar remoto de local

Quando houver divergência entre GitHub e workspace:

- registrar divergência;
- não sobrescrever entendimento local automaticamente;
- recomendar checagem local com `git status`, `git diff`, `git log`.

---

### 5. Tratar CI como evidência contextual

Status de CI ajuda, mas não substitui review.

Registrar:

- workflow;
- commit;
- status;
- falha ou sucesso;
- limitação.

---

### 6. Registrar achados

Achados relevantes devem alimentar:

- Investigation Note;
- Execution Plan;
- Review Report;
- Completion Packet;
- Escalation Note.

---

## Output esperado

```md
# GitHub Read-Only Ops Note

## Pergunta
<o que precisava ser verificado>

## Repositório/ref
<repo, branch, PR, issue ou commit>

## Fontes consultadas
- <arquivo, PR, issue, commit ou workflow>

## Achados
- <achado 1>
- <achado 2>

## Divergência local/remoto
<nenhuma | descrita | incerta>

## Implicação
<como isso afeta a task>

## Veredito
<suficiente | checar localmente | investigar mais | escalar>
```

---

## Checklist de qualidade

Antes de concluir, verificar:

- repo correto foi consultado?
- branch/ref correta foi identificada?
- a consulta foi read-only?
- achado remoto foi diferenciado de estado local?
- CI foi interpretado no commit certo?
- issue/PR foi usada como contexto, não como verdade técnica absoluta?
- divergências foram registradas?
- não houve ação remota sem autorização?

---

## Critérios de escalonamento

Escalar quando:

- remoto e local divergirem em decisão relevante;
- CI falhar sem causa clara;
- PR envolver risco R3/R4;
- issue contradizer documentação técnica;
- branch estiver divergente de forma complexa;
- leitura revelar segredo ou dado sensível;
- a próxima ação exigiria escrita no GitHub.

---

## Anti-patterns

Evitar:

- assumir que GitHub remoto é igual ao workspace;
- ler `main` quando a task está em branch;
- usar issue como especificação completa;
- ignorar comentários relevantes de PR;
- aceitar CI verde como prova de arquitetura correta;
- comentar, fechar ou mover item em modo read-only;
- usar histórico remoto para justificar mudança sem olhar código local.

---

## Declaração operacional curta

GitHub read-only informa estado remoto.  
O harness deve ler com ref correta, escopo claro e separação entre remoto, local e decisão técnica.