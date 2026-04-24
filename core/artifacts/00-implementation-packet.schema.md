# Schema — Implementation Packet

## Finalidade

O Implementation Packet é o artefato de entrada canônico da execução.

Seu papel é transformar uma intenção, ticket, issue, hipótese ou demanda em um pacote operacional suficientemente claro para que o executor possa:
- enquadrar a task;
- iniciar discovery;
- classificar risco;
- produzir Execution Plan;
- e identificar cedo o que depende de validação estratégica.

O Implementation Packet não é o plan.  
Ele é o insumo estruturado que antecede o plan.

---

## Quando deve ser usado

O Implementation Packet deve ser usado quando a task:
- não é trivial;
- tem impacto real em código, arquitetura, operação ou documentação;
- exige coordination entre humano, Core Architect e executor;
- ou precisa deixar claro o que entra, o que não entra e o que ainda está incerto.

Para tasks muito pequenas, ele pode ser mais enxuto.  
Para tasks moderadas ou sensíveis, ele deve ser explícito.

---

## Papel no fluxo

No fluxo canônico, o Implementation Packet:
1. enquadra a intenção;
2. limita o escopo;
3. torna a task auditável desde a entrada;
4. reduz improviso do executor;
5. prepara o terreno para discovery e plan.

---

## Campos obrigatórios

### 1. Objetivo
Descrição direta do que precisa ser resolvido, construído, alterado, investigado ou corrigido.

Pergunta que este campo responde:
- o que precisa acontecer ao final da task?

### 2. Contexto
Resumo do cenário que explica por que a task existe.

Perguntas que este campo responde:
- em que contexto esta demanda surgiu?
- o que motivou esta task?
- qual é a leitura inicial do problema?

### 3. Escopo
Lista do que está dentro da tarefa.

Pergunta que este campo responde:
- o que esta task cobre de fato?

### 4. Fora de escopo
Lista do que não deve ser puxado para dentro da task sem nova decisão.

Pergunta que este campo responde:
- o que explicitamente não deve ser resolvido aqui?

### 5. Critérios de aceite
Condições mínimas para considerar a task satisfatória.

Pergunta que este campo responde:
- como saber que a task foi bem resolvida?

### 6. Classe de risco preliminar
Classificação inicial entre R0 e R4.

Pergunta que este campo responde:
- qual o envelope inicial de cautela desta task?

### 7. Restrições
Limites conhecidos da execução.

Podem incluir:
- restrições arquiteturais;
- restrições de stack;
- limites de tempo;
- limites de mutação;
- decisões já tomadas;
- dependências externas;
- convenções locais.

### 8. Dependências e pré-condições
Tudo aquilo que precisa existir ou estar resolvido antes da execução madura.

### 9. Dúvidas abertas
Incertezas já conhecidas no momento da entrada.

### 10. Resultado esperado
Que tipo de saída se espera da task.

Exemplos:
- Execution Plan;
- implementação;
- Investigation Note;
- Completion Packet;
- Review Report;
- Escalation Note.

---

## Campos recomendados

### 11. Artefatos ou referências relevantes
Issue, board item, ADR, documentação, ticket, links, arquivos ou notas úteis para a task.

### 12. Áreas candidatas de impacto
Regiões prováveis do projeto que podem ser tocadas.

### 13. Risco percebido
Leitura inicial do principal risco:
- funcional;
- arquitetural;
- operacional;
- de segurança;
- de escopo;
- de entropia.

### 14. Pressões reais do sistema
Quando aplicável, registrar se a task toca:
- concorrência;
- throughput;
- latência;
- consistência;
- observabilidade;
- estado local;
- modelo de execução em cloud;
- custo de complexidade.

### 15. Necessidade de Core Architect
Indicar se há expectativa de arbitragem estratégica antes da execução.

---

## O que o Implementation Packet não deve ser

Não deve ser:
- um transcript bruto;
- um brainstorm inteiro;
- um plan disfarçado;
- uma especificação excessivamente longa sem priorização;
- uma mistura confusa de contexto, implementação e review.

---

## Qualidade esperada

Um bom Implementation Packet deve ser:
- claro;
- curto o suficiente para orientar;
- denso o suficiente para evitar improviso;
- explícito quanto a limites e dúvidas;
- útil para plan e escalonamento.

Um packet ruim:
- deixa escopo ambíguo;
- não diz o que fica fora;
- não explicita risco;
- trata desejo genérico como instrução operacional.

---

## Template canônico

```md
# Implementation Packet

## Objetivo
<o que precisa ser resolvido>

## Contexto
<cenário e motivação da task>

## Escopo
- <item 1>
- <item 2>

## Fora de escopo
- <item 1>
- <item 2>

## Critérios de aceite
- <critério 1>
- <critério 2>

## Classe de risco preliminar
R0 | R1 | R2 | R3 | R4

## Restrições
- <restrição 1>
- <restrição 2>

## Dependências e pré-condições
- <dependência 1>
- <dependência 2>

## Dúvidas abertas
- <dúvida 1>
- <dúvida 2>

## Áreas candidatas de impacto
- <área 1>
- <área 2>

## Pressões reais do sistema
- <pressão 1>
- <pressão 2>

## Resultado esperado
<execution plan | implementation | investigation note | outro>

## Referências relevantes
- <issue, board item, ADR, arquivo, link, nota>
```

---

## Declaração operacional curta
O Implementation Packet enquadra a task antes do plan.
Ele existe para impedir que a execução comece em cima de intenção vaga ou escopo mal delimitado.