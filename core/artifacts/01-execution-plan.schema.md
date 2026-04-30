# Schema — Execution Plan

## Finalidade

O Execution Plan é o artefato canônico que converte o Implementation Packet e o discovery em caminho operacional auditável.

Seu papel é impedir que o executor salte da intenção para a mutação sem:
- mapa estrutural;
- hipótese de solução;
- delimitação de escopo;
- validação prevista;
- e leitura explícita de risco.

---

## Quando deve ser usado

O Execution Plan deve existir para toda task acima do trivial.

Ele é especialmente importante quando a task:
- toca múltiplos arquivos;
- toca áreas sensíveis;
- tem risco R2 ou superior;
- pode inflar complexidade;
- pode gerar impacto operacional;
- ou depende de discovery para não cair em improviso.

---

## Papel no fluxo

No fluxo canônico, o Execution Plan:
1. sucede o Implementation Packet;
2. formaliza a leitura do problema;
3. registra discovery suficiente;
4. organiza a execução;
5. permite revisão antes da mutação;
6. serve de referência para review e handoff.

---

## Campos obrigatórios

### 1. Leitura do problema
Síntese objetiva do que foi entendido após intake e discovery.

Pergunta que este campo responde:
- qual é o problema real que estamos resolvendo?

### 2. Classe de risco validada
Confirma ou corrige a classe preliminar de risco.

### 3. Discovery summary
Resumo do que foi descoberto sobre:
- topologia do repo;
- authority sources;
- área afetada;
- pontos sensíveis;
- lacunas relevantes.

### 4. Hipótese operacional
Qual caminho de solução será seguido e por quê.

Pergunta que este campo responde:
- que abordagem concreta será executada?

### 5. Escopo operacional
O que será alterado ou produzido nesta execução.

### 6. Fora de escopo operacional
O que explicitamente não será atacado nesta execução.

### 7. Áreas e arquivos-alvo
Lista ou descrição das regiões do projeto que devem ser tocadas.

### 8. Etapas de execução
Passo a passo lógico da implementação.

Cada etapa deve:
- ser coerente com o escopo;
- ser pequena o suficiente para review;
- preservar causalidade;
- evitar ritual vazio.

### 9. Estratégia de validação
Como a mudança será verificada.

Pode incluir:
- build;
- test;
- lint;
- format;
- checagens de segurança;
- leitura de diff;
- validação funcional;
- validação operacional.

### 10. Riscos e pontos de atenção
Lista de riscos reais percebidos após discovery.

### 11. Critérios de escalonamento
Quais sinais indicam que o executor deve parar e escalar.

### 12. Resultado esperado
Que tipo de saída o executor deve produzir ao final.

---

## Campos recomendados

### 13. Authority sources consultadas
Arquivos e comandos de autoridade usados para embasar o plan.

### 14. Pressões reais do sistema
Registrar explicitamente se o plan toca:
- estado local;
- concorrência;
- throughput;
- latência;
- consistência;
- observabilidade;
- falha parcial;
- execution model;
- cloud/runtime;
- custo de complexidade.

### 15. Impacto esperado em documentação e state
Se a task deve alterar:
- `PROJECT_STATE.md`;
- authority docs locais;
- operational reality;
- ou outros artefatos duráveis.

### 16. Budget operacional
Estimativa qualitativa de esforço, superfície e risco do fluxo.

### 17. Skills recomendadas
Skills que deveriam orientar a execução ou review.

---

## O que o Execution Plan não deve ser

Não deve ser:
- uma lista vaga de intenções;
- um pseudo-manifesto sem sequência executável;
- um texto longo sem etapas acionáveis;
- uma tese arquitetural sem ligação com a task;
- uma tentativa de resolver o problema inteiro no próprio plan.

---

## Qualidade esperada

Um bom Execution Plan deve ser:
- específico;
- proporcional;
- aderente ao repo real;
- claro quanto a limites;
- explícito em risco e validação;
- útil para ser revisado por humano e Core Architect.

Um plan ruim:
- não conversa com o discovery;
- não diz onde tocar;
- não diz como validar;
- não deixa claro quando parar.

---

## Template canônico

```md
# Execution Plan

## Leitura do problema
<leitura consolidada da task>

## Classe de risco validada
R0 | R1 | R2 | R3 | R4

## Discovery summary
- <topologia relevante>
- <authority sources>
- <área afetada>
- <sensibilidades>

## Hipótese operacional
<abordagem escolhida e rationale>

## Escopo operacional
- <item 1>
- <item 2>

## Fora de escopo operacional
- <item 1>
- <item 2>

## Áreas e arquivos-alvo
- <área ou arquivo 1>
- <área ou arquivo 2>

## Etapas de execução
1. <etapa 1>
2. <etapa 2>
3. <etapa 3>

## Estratégia de validação
- <validação 1>
- <validação 2>

## Riscos e pontos de atenção
- <risco 1>
- <risco 2>

## Critérios de escalonamento
- <sinal 1>
- <sinal 2>

## Pressões reais do sistema
- <pressão 1>
- <pressão 2>

## Impacto em state/documentação
- <impacto 1>
- <impacto 2>

## Skills recomendadas
- <skill 1>
- <skill 2>

## Resultado esperado
<completion packet | review report | escalation note | outro>
```

---

## Declaração operacional curta
O Execution Plan é o mapa da execução.
Sem ele, a implementação tende a virar improviso com linguagem confiante.