# Protocolo de Handoff

## Finalidade

Este protocolo define como o harness deve encerrar uma task, uma investigação, uma revisão ou uma execução de forma útil, honesta e continuável.

Seu papel é impedir que o trabalho termine apenas com uma mensagem final vaga, sem memória operacional, sem lacunas explícitas e sem próximo passo claro.

---

## Tese central

Uma task não termina quando o executor para de agir.  
Ela termina quando o estado resultante fica compreensível para outro humano, outro agente ou uma futura sessão.

Handoff bom preserva continuidade.  
Handoff ruim cria reinvestigação, ambiguidade e perda de contexto.

---

## Quando o handoff deve acontecer

O handoff deve acontecer ao final de:

- implementação;
- investigação;
- review;
- escalonamento;
- task interrompida;
- task bloqueada;
- task concluída com ressalvas;
- sessão que precisa ser continuada depois.

Nem todo handoff precisa ser longo, mas toda task relevante precisa deixar rastro claro.

---

## Formas de handoff

### 1. Completion Packet

Usado quando houve execução ou entrega.

Deve registrar:
- o que foi feito;
- o que não foi feito;
- validações;
- lacunas;
- riscos;
- próximo passo.

### 2. Investigation Note

Usada quando a saída principal foi descoberta factual, sem implementação.

Deve registrar:
- fontes;
- achados;
- hipóteses;
- incertezas;
- recomendação.

### 3. Review Report

Usado quando a saída principal foi avaliação crítica.

Deve registrar:
- objeto revisado;
- pontos fortes;
- pontos de atenção;
- bloqueios;
- veredito.

### 4. Escalation Note

Usada quando a task não pode seguir dentro do envelope do executor.

Deve registrar:
- motivo da escalada;
- opções;
- trade-offs;
- decisão pendente.

---

## Handoff mínimo esperado

Todo handoff relevante deve responder:

1. qual era o objetivo;
2. o que aconteceu;
3. o que foi produzido;
4. o que foi validado;
5. o que não foi validado;
6. que risco permanece;
7. qual é o próximo passo;
8. se há algo que precisa virar estado durável.

Se essas perguntas não estiverem respondidas, o handoff está incompleto.

---

## Handoff de task concluída

Quando a task for concluída, o handoff deve deixar claro:

- entrega realizada;
- arquivos ou áreas tocadas;
- validações executadas;
- divergências em relação ao plan;
- riscos remanescentes;
- recomendação de commit, PR ou follow-up;
- necessidade de atualizar `PROJECT_STATE.md`.

---

## Handoff de task bloqueada

Quando a task for bloqueada, o handoff deve deixar claro:

- onde a execução parou;
- por que parou;
- que tentativa foi feita;
- o que foi aprendido;
- qual decisão ou dependência falta;
- qual é a recomendação de destravamento.

Task bloqueada sem handoff vira perda de contexto.

---

## Handoff de investigação

Quando a task foi investigativa, o handoff deve separar:

- fatos;
- hipóteses;
- lacunas;
- riscos;
- recomendações.

Investigação não deve terminar como “não encontrei” sem explicar onde procurou e o que isso significa.

---

## Handoff de review

Quando a saída for review, o handoff deve deixar claro:

- o que foi revisado;
- o que não foi revisado;
- quais pontos bloqueiam;
- quais pontos são ressalvas;
- qual é o veredito;
- que ação vem depois.

---

## Handoff para Core Architect

Quando o handoff for direcionado ao Core Architect, ele deve priorizar:

- decisão pendente;
- trade-off real;
- risco arquitetural;
- complexidade proporcional;
- alternativas percebidas;
- recomendação do executor, se houver base.

O Core Architect não deve receber transcript bruto quando pode receber problema organizado.

---

## Handoff para humano operador

Quando o handoff for direcionado ao humano, ele deve priorizar:

- estado atual;
- decisão necessária;
- risco;
- evidência;
- próximo passo prático;
- comandos ou ações recomendadas.

O humano deve conseguir decidir sem reconstruir toda a sessão.

---

## Handoff para futura sessão

Quando o handoff existir para continuidade futura, ele deve priorizar:

- contexto mínimo;
- estado atual;
- artifacts relevantes;
- arquivos ou áreas importantes;
- lacunas abertas;
- próximos passos.

A futura sessão deve conseguir retomar sem depender de memória conversacional antiga.

---

## Relação com PROJECT_STATE

O handoff deve sempre considerar se algo merece virar memória durável.

A atualização de `PROJECT_STATE.md` deve ser considerada quando:
- houve mudança arquitetural;
- houve nova limitação;
- houve descoberta técnica relevante;
- houve alteração de comandos;
- houve mudança operacional;
- houve decisão que evitará rediscussão futura.

---

## Relação com board

O handoff pode indicar atualização de board quando:

- uma task foi concluída;
- uma task foi bloqueada;
- surgiu follow-up;
- surgiu dependência nova;
- o status real diverge do status registrado.

Mas board não substitui handoff técnico.

---

## O que evitar no handoff

Evitar:

- narrativa triunfal;
- resumo genérico;
- omitir lacunas;
- esconder falha de validação;
- despejar transcript;
- deixar próximo passo implícito;
- misturar várias tasks em uma conclusão só.

---

## Critério de bom handoff

Um bom handoff permite que alguém responda rapidamente:

- onde estamos?
- o que mudou?
- dá para confiar?
- o que falta?
- qual é o próximo movimento?

Se isso não for possível, o handoff falhou.

---

## Declaração operacional curta

Handoff é transferência de continuidade.  
Sem handoff, a task pode até ter parado, mas a engenharia não terminou.