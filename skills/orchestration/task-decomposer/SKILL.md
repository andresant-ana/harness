# Skill — Task Decomposer

## Finalidade

Esta skill orienta a decomposição de uma demanda em unidades menores, executáveis, revisáveis e coerentes.

Seu papel é impedir que o agente tente resolver uma task grande demais em uma única execução, misture frentes diferentes ou transforme uma demanda simples em arquitetura excessiva.

---

## Quando usar

Use esta skill quando:

- a task parecer grande demais;
- houver múltiplas frentes de trabalho;
- a demanda misturar discovery, implementação, refactor e documentação;
- houver risco de escopo escorregar;
- o Execution Plan estiver ficando amplo demais;
- a task puder ser melhor resolvida por etapas;
- houver necessidade de separar investigação de implementação.

---

## Quando não usar

Não use esta skill quando:

- a task já for pequena e local;
- a decomposição criaria burocracia;
- dividir a task reduziria clareza;
- a task precisa ser atômica por consistência técnica;
- a decomposição for apenas estética.

---

## Tese central

Decompor não é fragmentar por fragmentar.

Boa decomposição reduz risco e melhora revisão.  
Má decomposição cria overhead, dependências artificiais e perda de contexto.

---

## Método

### 1. Identificar objetivo final

Antes de quebrar, entender:

- qual resultado final se espera;
- qual problema real está sendo resolvido;
- qual é o critério de aceite global.

### 2. Separar tipos de trabalho

Classificar partes da demanda como:

- investigação;
- decisão estratégica;
- implementação;
- validação;
- documentação;
- state update;
- review;
- follow-up.

Misturar tudo em uma execução só costuma aumentar risco.

### 3. Identificar dependências

Perguntar:

- que etapa depende de outra?
- o que precisa ser descoberto antes de implementar?
- que decisão precisa ser tomada antes de mutar?
- que validação deve acontecer antes de prosseguir?

### 4. Identificar cortes naturais

Cortes bons costumam ser baseados em:

- módulo;
- fluxo;
- camada;
- artifact;
- tipo de risco;
- fronteira técnica;
- sequência causal.

Cortes ruins são baseados apenas em tamanho ou conveniência.

### 5. Preservar atomicidade quando necessário

Nem toda task deve ser quebrada.

Preservar unidade quando dividir:

- deixaria o sistema quebrado;
- criaria estado intermediário confuso;
- aumentaria risco de inconsistência;
- separaria mudança de validação essencial.

### 6. Definir entregáveis por etapa

Cada subtask deve ter:

- objetivo;
- escopo;
- fora de escopo;
- classe de risco;
- artifact esperado;
- validação mínima;
- critério de conclusão.

### 7. Ordenar execução

Ordenar por:

1. discovery;
2. decisão;
3. implementação mínima;
4. validação;
5. review;
6. documentação/state;
7. follow-up.

---

## Padrões de decomposição

### Investigação antes de implementação

Use quando o problema ainda não está claro.

Saída:

- Investigation Note;
- depois Execution Plan.

### Implementação por vertical slice

Use quando uma feature pode ser entregue em fluxo pequeno, ponta a ponta, sem espalhar arquitetura.

Saída:

- mudança funcional mínima;
- validação proporcional.

### Separação de refactor e feature

Use quando a feature revelou necessidade de refactor.

Regra:

- não misturar refactor amplo com feature sem aprovação.

### Separação de risco

Use quando parte da task é R1/R2, mas outra parte é R3/R4.

Regra:

- executar o que está dentro da autonomia;
- escalar o que saiu do envelope.

### Separação de documentação durável

Use quando a implementação muda estado técnico.

Regra:

- Completion Packet encerra task;
- Project State Entry atualiza memória durável.

---

## Outputs esperados

A skill pode produzir:

- plano de decomposição;
- lista de subtasks;
- proposta de sequência;
- critérios de corte;
- recomendação de Escalation Note;
- recomendação de Investigation Note;
- recomendação de Project State Entry.

---

## Checklist de qualidade

Uma decomposição boa responde:

- cada subtask tem objetivo claro?
- cada subtask tem critério de conclusão?
- a ordem é causal?
- o risco foi separado corretamente?
- há escopo e fora de escopo?
- a decomposição reduz review burden?
- evita estado intermediário quebrado?
- preserva verticalidade quando útil?
- evita fragmentação artificial?

---

## Critérios de escalonamento

Escalar quando:

- a decomposição exigir decisão arquitetural;
- houver disputa entre monólito modular, microserviço, mensageria, CQRS ou outra abordagem estrutural;
- a task original estiver mal definida;
- houver risco de quebrar boundary;
- houver risco R3/R4;
- o humano precisar escolher trade-off.

---

## Anti-patterns

Evitar:

- criar subtasks demais;
- decompor por camada sem necessidade;
- separar controller, service, repository, DTO e mapper por ritual;
- transformar feature pequena em projeto;
- misturar bugfix com refactor lateral;
- esconder uma mudança estrutural dentro de subtask “simples”;
- quebrar tanto que ninguém entende o todo.

---

## Declaração operacional curta

Boa decomposição reduz risco sem perder causalidade.  
Ela transforma trabalho grande em passos governáveis, não em burocracia.