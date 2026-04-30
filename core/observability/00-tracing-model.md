# Modelo de Tracing do Harness

## Finalidade

Este documento define como o harness deve registrar a trilha factual de uma task, investigação, execução, review ou escalonamento.

Seu papel é permitir que humano, Core Architect ou agente futuro consigam reconstruir:

- o que foi pedido;
- o que foi entendido;
- quais fontes foram consultadas;
- qual plano foi aprovado;
- quais ações foram executadas;
- quais evidências foram produzidas;
- onde houve lacuna;
- qual foi o estado final.

Tracing não é logging infinito.  
Tracing é rastreabilidade útil.

---

## Tese central

O harness só é confiável se suas decisões e ações puderem ser reconstruídas.

A engenharia rejeita fluxo opaco em que o executor:

- decide sem registrar;
- muda sem explicar;
- valida sem evidência;
- escala sem contexto;
- encerra sem handoff;
- ou deixa a próxima sessão dependente de transcript bruto.

Tracing transforma execução em trilha auditável.

---

## O que tracing deve preservar

Tracing deve preservar fatos operacionais, não todo o raciocínio bruto.

Deve preservar:

- input da task;
- classe de risco;
- artifacts produzidos;
- fontes consultadas;
- comandos relevantes;
- decisões tomadas;
- divergências do plan;
- validações realizadas;
- lacunas reconhecidas;
- review;
- handoff;
- state update, quando aplicável.

Não deve preservar:

- transcript completo;
- tentativas irrelevantes;
- raciocínio verborrágico;
- outputs ruidosos;
- logs extensos sem síntese;
- segredo, credencial ou dado sensível.

---

## Unidade de tracing

A unidade primária de tracing é a task.

Cada task relevante deve permitir responder:

1. qual era o objetivo;
2. qual era a classe de risco;
3. qual artifact iniciou a execução;
4. qual plan foi seguido;
5. quais fontes foram usadas;
6. quais ações foram feitas;
7. quais evidências sustentam a conclusão;
8. qual artifact encerrou a task;
9. se houve atualização de estado durável.

---

## Eventos rastreáveis

### 1. Intake

Registrar:

- objetivo;
- contexto;
- escopo;
- fora de escopo;
- critérios de aceite;
- classe de risco preliminar.

Artifact típico:

- Implementation Packet.

---

### 2. Discovery

Registrar:

- authority sources consultadas;
- topologia relevante;
- áreas candidatas de impacto;
- lacunas descobertas;
- riscos percebidos.

Artifact típico:

- trecho do Execution Plan;
- Investigation Note, quando necessário.

---

### 3. Plan

Registrar:

- hipótese operacional;
- classe de risco validada;
- áreas e arquivos-alvo;
- estratégia de validação;
- critérios de escalonamento.

Artifact típico:

- Execution Plan.

---

### 4. Aprovação

Registrar:

- se o plan foi aprovado;
- por quem ou por qual camada;
- ressalvas;
- limites de execução;
- mudanças exigidas antes de executar.

Artifact típico:

- comentário humano;
- decisão do Core Architect;
- Review Report de plan, se aplicável.

---

### 5. Execução

Registrar:

- arquivos tocados;
- comandos relevantes;
- mudanças feitas;
- desvios do plan;
- pausas ou replanejamentos.

Artifact típico:

- diff;
- notas no Completion Packet.

---

### 6. Validação

Registrar:

- comandos executados;
- resultados relevantes;
- validações manuais;
- checagens de segurança;
- checagens operacionais;
- falhas e lacunas.

Artifact típico:

- Completion Packet;
- Evidence summary.

---

### 7. Review

Registrar:

- objeto revisado;
- escopo revisado;
- lacunas de evidência;
- riscos;
- bloqueios;
- veredito.

Artifact típico:

- Review Report.

---

### 8. Escalonamento

Registrar:

- motivo da escalada;
- opções percebidas;
- trade-offs;
- decisão pendente;
- classe de risco atualizada.

Artifact típico:

- Escalation Note.

---

### 9. Handoff

Registrar:

- resumo final;
- o que foi feito;
- o que não foi feito;
- risco residual;
- próximo passo;
- necessidade de atualização de state.

Artifact típico:

- Completion Packet;
- Investigation Note;
- Review Report;
- Escalation Note.

---

### 10. Atualização de estado

Registrar:

- se `PROJECT_STATE.md` deve ser atualizado;
- qual entrada foi criada ou alterada;
- que decisão ou estado durável mudou.

Artifact típico:

- Project State Entry.

---

## Trace mínimo por classe de risco

### R0

Rastrear:

- pergunta;
- fontes consultadas;
- achados;
- hipóteses;
- lacunas.

Artifact esperado:

- Investigation Note.

---

### R1

Rastrear:

- objetivo;
- arquivos tocados;
- validação local;
- lacunas;
- conclusão.

Artifact esperado:

- Completion Packet enxuto.

---

### R2

Rastrear:

- Implementation Packet;
- Execution Plan;
- discovery;
- validações;
- diff;
- Completion Packet;
- review proporcional.

Artifact esperado:

- Completion Packet;
- Review Report recomendado.

---

### R3

Rastrear:

- decisão estratégica;
- Escalation Note, quando aplicável;
- trade-offs;
- validação forte;
- review explícito;
- state update, se durável.

Artifact esperado:

- Escalation Note;
- Review Report;
- Project State Entry, quando aplicável.

---

### R4

Rastrear:

- autorização explícita;
- ação exata;
- ambiente alvo;
- risco;
- rollback ou mitigação;
- aprovação humana;
- evidência máxima.

Artifact esperado:

- documento excepcional;
- Escalation Note;
- registro humano.

---

## Formato recomendado de trace

O harness não precisa criar um arquivo de trace para toda microtask, mas toda task relevante deve deixar trilha nos artifacts.

Quando necessário, um trace pode ser resumido assim:

- Task ID ou referência;
- classe de risco;
- artifact de entrada;
- plan;
- comandos relevantes;
- arquivos tocados;
- validações;
- review;
- handoff;
- state update;
- lacunas.

---

## Relação com evidência

Tracing sem evidência vira narrativa.

Todo trace relevante deve apontar para evidência:

- arquivo lido;
- comando executado;
- diff;
- artifact;
- fonte externa;
- review;
- decisão humana.

A trilha não precisa conter tudo, mas precisa permitir reconstrução.

---

## Relação com contexto

Tracing reduz dependência de contexto conversacional.

Quando o trace é bom:

- futuras sessões não precisam reler transcript bruto;
- agentes conseguem retomar estado;
- humano entende o que aconteceu;
- Core Architect consegue revisar decisão sem reconstruir tudo.

---

## Relação com segurança

Trace não deve vazar:

- segredos;
- tokens;
- connection strings;
- dados pessoais;
- payloads sensíveis;
- logs extensos com informação confidencial.

Quando algo sensível for relevante, registrar sua existência e impacto sem reproduzir o conteúdo.

---

## Relação com PROJECT_STATE

Nem todo trace vira `PROJECT_STATE.md`.

Só deve virar state quando a task alterar realidade durável do projeto.

Tracing responde:
- o que aconteceu nesta task?

`PROJECT_STATE.md` responde:
- em que estado técnico o projeto ficou?

---

## Sinais de tracing ruim

Tracing está ruim quando:

- não dá para saber por que uma decisão foi tomada;
- não há conexão entre plan e diff;
- validação aparece como frase vaga;
- lacunas foram omitidas;
- a próxima sessão precisa reler tudo;
- o humano não consegue aprovar com confiança;
- o estado final depende de memória do agente.

---

## Declaração operacional curta

Tracing é a memória factual da execução.  
O harness não precisa guardar tudo.  
Precisa guardar o suficiente para reconstruir, revisar e continuar.