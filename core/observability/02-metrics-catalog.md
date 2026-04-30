# Catálogo de Métricas do Harness

## Finalidade

Este documento define métricas qualitativas e quantitativas que podem ser usadas para observar a qualidade, eficiência e degradação do harness.

Seu papel é orientar o que vale medir sem transformar a engenharia em painel burocrático.

Métrica boa ajuda decisão.  
Métrica ruim vira teatro.

---

## Tese central

O harness deve medir sinais que indiquem se ele está:

- reduzindo risco;
- melhorando evidência;
- preservando contexto;
- evitando slop;
- melhorando review;
- preservando continuidade;
- ou apenas adicionando cerimônia.

Métricas devem servir à engenharia, não dominar a engenharia.

---

## Princípios de métricas

### 1. Medir o que muda decisão

Se uma métrica não ajuda a decidir, revisar ou melhorar o harness, ela provavelmente é ruído.

### 2. Evitar métrica de vaidade

Quantidade de arquivos, tamanho de documentação ou número de artifacts não provam qualidade.

### 3. Combinar qualitativo e quantitativo

Nem tudo importante é numérico.  
Review, handoff e arquitetura exigem julgamento.

### 4. Medir proporcionalidade

O harness deve ser rigoroso em risco alto e leve em risco baixo.

### 5. Observar tendência

Uma medição isolada importa menos do que padrão recorrente.

---

## Categorias de métricas

1. fluxo;
2. planning;
3. discovery;
4. evidência;
5. review;
6. handoff;
7. contexto;
8. segurança;
9. produção;
10. entropia;
11. autonomia/escalonamento;
12. state maintenance;
13. eficiência.

---

## Métricas de fluxo

### Flow adherence

Mede se a task seguiu o fluxo esperado para sua classe de risco.

Escala sugerida:
- 0: fluxo ignorado;
- 1: fluxo parcial;
- 2: fluxo adequado;
- 3: fluxo forte.

### Stage skip rate

Indica se etapas críticas foram puladas.

Observar:
- plan pulado;
- discovery pulado;
- validação pulada;
- review pulado;
- handoff pulado.

### Risk-flow alignment

Mede se o peso do fluxo combinou com a classe de risco.

Sinais ruins:
- R1 com burocracia excessiva;
- R3 tratado como R1;
- R2 sem review;
- R0 com implementação disfarçada.

---

## Métricas de planning

### Plan specificity

Avalia se o Execution Plan foi específico.

Critérios:
- arquivos/áreas-alvo;
- etapas concretas;
- validação;
- riscos;
- critérios de escalonamento.

### Plan usefulness

Avalia se o plan realmente guiou a execução.

Sinais de baixa utilidade:
- execução ignorou o plan;
- plan era genérico;
- plan não previu riscos óbvios;
- plan não ajudou review.

### Plan revision rate

Mede quantas vezes o plan precisou ser corrigido.

Nem toda revisão é ruim.  
Revisões por discovery novo podem ser saudáveis.  
Revisões por plan fraco indicam problema.

---

## Métricas de discovery

### Authority source coverage

Avalia se fontes locais de verdade foram consultadas.

Critérios:
- authority files;
- authority commands;
- documentação local;
- config real;
- PROJECT_STATE.

### Discovery precision

Mede se o discovery focou na área certa sem abrir contexto inútil demais.

### Missed critical file

Sinaliza quando um arquivo importante foi ignorado e isso prejudicou execução ou review.

---

## Métricas de evidência

### Evidence strength

Escala:
- 0: sem evidência;
- 1: evidência verbal/fraca;
- 2: evidência suficiente;
- 3: evidência robusta.

### Validation coverage

Avalia se validações previstas foram feitas.

Pode observar:
- build;
- test;
- lint;
- diff review;
- validação funcional;
- segurança;
- operação.

### Explicit gap quality

Mede se lacunas foram explicitadas com honestidade.

Lacuna declarada é melhor do que lacuna escondida.

---

## Métricas de review

### Review decision clarity

Avalia se o review produziu veredito claro.

Vereditos esperados:
- aprovado;
- aprovado com ressalvas;
- reavaliar;
- bloquear.

### Review catch rate

Observa se reviews identificam problemas reais antes do humano.

### Review depth alignment

Avalia se o review foi proporcional à classe de risco.

### False approval signal

Sinaliza quando o review aprovou algo que depois se mostrou problemático.

---

## Métricas de handoff

### Handoff continuity score

Avalia se uma futura sessão consegue continuar.

Critérios:
- estado atual claro;
- próximos passos;
- validações;
- lacunas;
- riscos;
- artifacts referenciados.

### Missing next step

Sinaliza handoff sem próximo movimento claro.

### State update detection

Avalia se o handoff detectou necessidade de atualizar `PROJECT_STATE.md`.

---

## Métricas de contexto

### Context load

Avalia se a quantidade de contexto usada foi proporcional.

Sinais de alerta:
- leitura massiva sem mapa;
- transcript arrastado;
- skills demais;
- docs demais para task simples.

### Compaction quality

Avalia se compactação preservou fatos e removeu ruído.

### Context-to-progress ratio

Observa se aumento de contexto gerou aumento real de clareza ou ação.

---

## Métricas de segurança

### Security baseline application

Avalia se segurança foi considerada quando relevante.

### Secret exposure incidents

Sinaliza qualquer exposição ou quase exposição de segredo.

### Unsafe command prevention

Mede se comandos sensíveis foram bloqueados, reclassificados ou escalados.

### Dependency risk review

Avalia se dependências novas ou atualizadas foram justificadas.

---

## Métricas de produção

### Production-minded coverage

Avalia se a task considerou:

- observabilidade;
- falha parcial;
- runtime;
- estado local;
- banco;
- cloud;
- recursos.

### Observability adequacy

Avalia se mudança relevante ficou observável.

### Localhost-only risk

Sinaliza soluções que funcionam localmente, mas ignoram operação real.

---

## Métricas de entropia

### Entropy delta

Avalia se a task aumentou, preservou ou reduziu entropia.

Valores possíveis:
- reduziu;
- preservou;
- aumentou justificadamente;
- aumentou injustificadamente.

### Diff causality

Avalia se cada arquivo alterado tem causalidade clara com a task.

### Abstraction justification

Avalia se nova camada, interface, dependency ou pattern tem dor real.

### Documentation drift

Sinaliza divergência entre documentação e realidade.

---

## Métricas de autonomia e escalonamento

### Correct escalation rate

Avalia se o agente escalou quando deveria.

### Missed escalation

Sinaliza quando o agente continuou decidindo fora do envelope.

### Over-escalation

Sinaliza quando o agente escalou problema que estava dentro da autonomia.

### Risk reclassification quality

Avalia se o agente corrigiu classe de risco quando o discovery revelou nova realidade.

---

## Métricas de state maintenance

### Project state update accuracy

Avalia se updates de `PROJECT_STATE.md` foram feitos quando deveriam.

### Project state noise

Avalia se o state está recebendo ruído demais.

### Project state usefulness

Avalia se o state ajuda futuras sessões.

---

## Métricas de eficiência

### Time-to-plan

Tempo ou esforço até produzir um plan útil.

### Rework rate

Quanto retrabalho surgiu por plan ruim, discovery fraco ou review insuficiente.

### Stuck recovery time

Quanto tempo levou para detectar e sair de travamento.

### Automation usefulness

Avalia se commands, skills ou templates reduziram fricção real.

---

## Métricas que devem ser evitadas

Evitar medir como sinal principal de sucesso:

- número de arquivos criados;
- tamanho dos artifacts;
- quantidade de skills chamadas;
- quantidade de commits;
- número de palavras do plan;
- quantidade de comandos rodados.

Essas métricas podem indicar atividade, mas não necessariamente qualidade.

---

## Registro inicial recomendado

Durante piloto, registrar manualmente por task:

- classe de risco;
- artifacts usados;
- score de plan;
- score de evidência;
- score de review;
- score de handoff;
- entropy delta;
- necessidade de state update;
- falhas percebidas.

---

## Declaração operacional curta

Métrica boa melhora julgamento.  
Métrica ruim cria teatro.  
O harness mede para aprender, não para parecer sofisticado.