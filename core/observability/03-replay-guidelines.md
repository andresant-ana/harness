# Diretrizes de Replay

## Finalidade

Este documento define como o harness deve repetir cenários de task para comparar comportamento entre versões do sistema, agentes, skills, adapters ou modelos.

Seu papel é permitir que melhorias no harness sejam avaliadas por comportamento observável, não por impressão subjetiva.

Replay ajuda a responder:

- a nova versão melhorou ou piorou?
- o agente segue melhor o fluxo?
- o plan ficou mais específico?
- o review ficou mais útil?
- o handoff ficou mais continuável?
- o sistema reduziu slop ou só aumentou cerimônia?

---

## Tese central

Se um cenário importante não pode ser repetido, fica difícil saber se o harness evoluiu.

Replay não precisa ser automatizado no início.  
Replay precisa ser suficientemente estruturado para permitir comparação honesta.

---

## O que é um replay

Replay é a repetição controlada de uma task, investigação ou cenário usando:

- o mesmo input;
- a mesma classe de risco;
- o mesmo contexto inicial;
- critérios de avaliação semelhantes;
- e comparação de outputs.

O objetivo não é obter resultado idêntico.  
O objetivo é comparar qualidade do comportamento.

---

## Quando usar replay

Usar replay quando:

- uma versão do harness muda comportamento relevante;
- uma skill nova é adicionada;
- um protocol ou policy é alterado;
- um adapter muda;
- um modelo diferente será testado;
- uma falha importante precisa ser reproduzida;
- um caso de slop precisa virar teste de regressão;
- uma task real revelou fraqueza sistêmica.

---

## Tipos de replay

### 1. Replay de planning

Repete uma task para comparar Execution Plans.

Avaliar:
- especificidade;
- risco;
- validação;
- escopo;
- critérios de escalonamento;
- ausência de over-engineering.

### 2. Replay de review

Repete revisão de uma mudança ou Completion Packet.

Avaliar:
- lacunas encontradas;
- riscos percebidos;
- veredito;
- bloqueios;
- clareza.

### 3. Replay de investigação

Repete uma task R0.

Avaliar:
- fontes;
- fatos;
- hipóteses;
- lacunas;
- recomendação.

### 4. Replay de stuck recovery

Repete cenário onde agente travou.

Avaliar:
- detecção;
- pausa;
- replanejamento;
- escalonamento;
- redução de contexto.

### 5. Replay anti-slop

Repete cenário propenso a over-engineering.

Avaliar:
- se o agente evitou abstração prematura;
- se preservou menor diff;
- se aplicou architecture by pain;
- se review pegou excesso.

---

## Como preparar um cenário de replay

Um cenário de replay deve conter:

1. descrição da task;
2. classe de risco esperada;
3. contexto inicial mínimo;
4. arquivos ou artifacts relevantes;
5. restrições;
6. critérios de sucesso;
7. falhas esperadas a observar;
8. outputs a comparar.

---

## Entrada mínima de replay

A entrada deve ser suficiente, mas não inflada.

Deve conter:

- objetivo;
- contexto;
- escopo;
- fora de escopo;
- autoridade local relevante;
- classe de risco esperada;
- artifact esperado;
- critérios de avaliação.

Evitar:
- transcript longo;
- dica excessiva;
- resposta esperada completa;
- contexto que já resolve o problema para o agente.

---

## Saídas a comparar

Comparar:

- Implementation Packet, se produzido;
- Execution Plan;
- Investigation Note;
- Completion Packet;
- Review Report;
- Escalation Note;
- Project State Entry;
- comportamento de comandos;
- decisão de escalar ou não;
- uso de skills;
- tamanho e utilidade do contexto.

---

## Critérios de comparação

A comparação deve observar:

- aderência ao fluxo;
- especificidade;
- evidência;
- segurança;
- produção;
- entropia;
- contexto;
- review;
- handoff;
- proporcionalidade.

Não comparar apenas:
- estilo textual;
- verbosidade;
- número de tópicos;
- confiança aparente.

---

## Como registrar resultado de replay

Cada replay deve registrar:

- cenário;
- versão do harness;
- runtime ou adapter;
- modelo, se relevante;
- artifacts produzidos;
- pontuação qualitativa;
- falhas observadas;
- regressões;
- melhorias;
- decisão de ajuste.

---

## Escala simples de replay

Usar escala:

- piorou;
- igual;
- melhorou parcialmente;
- melhorou claramente;
- inconclusivo.

Sempre justificar com evidência.

---

## Replays recomendados para piloto

Criar cenários para:

1. task R1 simples;
2. feature R2 com múltiplos arquivos;
3. investigação R0;
4. mudança com risco de dependência nova;
5. mudança com risco de N+1 ou query ruim;
6. task que deveria acionar Core Architect;
7. task que deveria gerar Escalation Note;
8. task que deveria atualizar `PROJECT_STATE.md`;
9. task propensa a Clean Architecture ritualística;
10. task com risco de produção/observabilidade.

---

## Replay e versões do harness

Ao alterar:

- protocol;
- policy;
- artifact;
- skill;
- agent;
- adapter,

considerar replay se a alteração mudar comportamento esperado.

Alteração puramente editorial normalmente não exige replay.

---

## Replay e modelos diferentes

Replay pode ser usado para comparar modelos.

O objetivo não é descobrir qual modelo “fala melhor”.  
É descobrir qual modelo, sob o harness, executa melhor:

- plan;
- discovery;
- evidência;
- review;
- segurança;
- handoff;
- anti-slop.

---

## Replay e regressão

Quando um problema já foi detectado e corrigido, criar replay ajuda a evitar regressão.

Exemplo:

- agente adicionou camada sem dor real;
- review não detectou segredo em diff;
- handoff omitiu lacuna;
- plan ignorou authority source;
- task travou e continuou tentando.

Esses casos devem virar cenários de regressão.

---

## O que evitar

Evitar:

- replay com contexto diferente demais;
- comparar outputs sem critério;
- escolher cenário fácil demais;
- usar replay para provar tese já decidida;
- medir só beleza textual;
- ignorar custo de contexto.

---

## Declaração operacional curta

Replay transforma experiência em aprendizado comparável.  
Sem replay, evolução do harness vira impressão.  
Com replay, melhoria precisa aparecer no comportamento.