# Arquitetura por Dor Real

## Finalidade

Esta policy existe para impedir que o harness trate complexidade como sinal automático de maturidade.

Seu papel é formalizar uma regra central da engenharia:  
**arquitetura boa não nasce de antecipação ansiosa, mas de dor real, pressão real e trade-off consciente**.

Este documento protege o sistema contra:

- over-engineering;
- cerimônia arquitetural vazia;
- abstração preventiva para problemas imaginários;
- introdução de camadas sem dor concreta;
- adoção de padrões por prestígio técnico em vez de necessidade.

---

## Tese central

A melhor arquitetura possível não é a mais sofisticada.  
É a arquitetura mais simples que respeita o problema real, o risco real e a evolução provável do sistema sem introduzir custo desnecessário.

A engenharia rejeita a lógica de:

- “vamos deixar pronto para o futuro” sem pressão real;
- “vamos colocar uma camada porque boas práticas mandam”;
- “vamos usar o padrão hypado porque o sistema pode crescer um dia”;
- “vamos separar tudo desde o começo para não refatorar depois”.

Arquitetura por dor real significa:

- abstrair quando dói;
- modularizar quando o acoplamento começa a custar;
- isolar quando a contaminação começa a gerar dano;
- distribuir quando a pressão operacional ou organizacional justificar;
- sofisticar apenas quando o ganho superar claramente o custo.

---

## Regra operacional principal

Nenhuma nova camada arquitetural deve entrar no sistema sem responder claramente:

1. qual dor real ela resolve;
2. qual risco real ela reduz;
3. que alternativa mais simples foi considerada;
4. qual custo cognitivo ela adiciona;
5. qual custo operacional ela adiciona;
6. qual custo de manutenção ela adiciona;
7. o que acontece se ela não for introduzida agora.

Se essas respostas não estiverem claras, a presunção correta é:
**não introduzir a camada ainda**.

---

## O que conta como dor real

Dor real é uma pressão concreta já observável no sistema ou no fluxo de trabalho.

Exemplos de dor real:

- repetição de lógica que já gerou divergência ou risco;
- boundary de domínio contaminado por detalhes externos frágeis;
- mudança frequente de contrato externo que polui o núcleo do sistema;
- carga, concorrência ou latência exigindo mudança de topologia;
- dificuldade recorrente de manutenção por acoplamento real;
- crescimento de módulo já tornando navegação e evolução ruins;
- necessidade factual de processamento assíncrono;
- necessidade factual de isolar falha, throughput ou consistência;
- risco operacional já conhecido e recorrente.

---

## O que não conta como dor real

Não conta como dor real:

- medo genérico de crescimento futuro;
- vontade de “deixar pronto” sem evidência de uso;
- preferência estética por arquitetura cerimonial;
- pressão social de mercado ou buzzword;
- desejo de “mostrar maturidade” via padrão sofisticado;
- exemplos de artigos, vídeos ou conferências sem aderência ao caso;
- hipótese de troca de tecnologia nunca vivida na prática;
- “talvez um dia precise” sem impacto atual.

---

## Heurística de decisão

Antes de aprovar qualquer aumento de complexidade, o sistema deve passar pelas perguntas abaixo.

### Pergunta 1 — Isso já doeu de verdade?
Se ainda não doeu em manutenção, domínio, operação, segurança, throughput, concorrência ou clareza, a tendência correta é não sofisticar.

### Pergunta 2 — Essa dor é local ou sistêmica?
Se a dor é local, a solução deve ser local.  
Complexidade sistêmica para dor local é anti-pattern.

### Pergunta 3 — Há segunda ocorrência real?
Extrações, interfaces, camadas e generalizações costumam ser mais legítimas na segunda ocorrência real do que na primeira hipótese imaginária.

### Pergunta 4 — Isso protege o domínio ou só aumenta a cerimônia?
Encapsulamento e boundary protection são diferentes de indireção ritualística.

### Pergunta 5 — O custo futuro de não fazer agora é realmente maior?
Nem todo refactor futuro é caro o suficiente para justificar complexidade presente.

### Pergunta 6 — Isso melhora ou piora a navegabilidade para humano e agente?
Arquitetura boa precisa continuar legível e rastreável.  
Se a proposta espalha uma feature simples em muitos arquivos sem ganho proporcional, isso é sinal de alerta.

---

## Regras por tipo de sofisticação

### Interfaces e inversão de dependência
Devem entrar quando:
- existe contrato externo frágil;
- o domínio precisa ser protegido de poluição externa;
- a troca real ou o isolamento real justifica a indireção;
- a testabilidade ou boundary clarity melhora de forma material.

Não devem entrar quando:
- a única justificativa é “boa prática genérica”;
- não existe probabilidade real de variação;
- a abstração só cria mais boilerplate.

### Camadas adicionais
Devem entrar quando:
- reduzem acoplamento real;
- tornam o domínio mais claro;
- isolam mudança frequente;
- reduzem risco operacional.

Não devem entrar quando:
- tornam uma mudança simples artificialmente distribuída;
- criam navegação ruim;
- forçam a mesma feature a tocar muitos arquivos sem ganho real.

### Mensageria e assíncrono
Devem entrar quando:
- há desacoplamento temporal necessário;
- há pressão de throughput;
- há absorção de burst relevante;
- há necessidade de isolamento entre partes do sistema;
- há processos naturalmente orientados a evento.

Não devem entrar quando:
- chamada síncrona resolve o problema com simplicidade;
- a motivação é apenas “escalar melhor no futuro”;
- o custo de tracing, operação e consistência supera o benefício atual.

### CQRS e Event Sourcing
Só devem ser considerados quando:
- o domínio realmente exige;
- a separação de leitura/escrita resolve dor real;
- o histórico de eventos tem valor operacional, auditável ou de reconstrução de estado;
- o time consegue sustentar a operação dessa escolha.

Não devem ser adotados como “upgrade automático” de maturidade.

### Distribuição e microserviços
Só devem ser considerados quando:
- há boundary organizacional ou operacional legítimo;
- há necessidade real de autonomia de deploy, escala ou isolamento;
- o monólito modular já começou a cobrar caro em pontos reais.

Microserviço por ansiedade de futuro é regressão disfarçada.

---

## Relação com IA, agente e custo de contexto

Arquiteturas cerimoniais custam caro não apenas para humanos, mas também para agentes.

Cada camada sem necessidade:
- adiciona arquivos;
- aumenta navegação;
- infla contexto;
- esconde causalidade;
- piora rastreabilidade;
- aumenta chance de slop.

Por isso, a arquitetura aprovada deve levar em conta não só elegância teórica, mas também:
- custo de leitura;
- custo de revisão;
- custo de implementação;
- custo de contexto para agentes.

---

## Padrão de justificativa esperado

Toda proposta arquitetural acima do trivial deve deixar explícito:

- dor observada;
- alternativa mais simples;
- ganho esperado;
- custo introduzido;
- risco de não fazer;
- risco de fazer cedo demais.

Sem esse padrão de justificativa, a proposta não está madura.

---

## Relação com review

O reviewer e o architect-critic devem tratar como sinal de risco:

- camadas novas sem dor observada;
- abstração criada antes de segunda ocorrência real;
- feature simples espalhada em muitos arquivos;
- argumento baseado em “boas práticas” sem contexto;
- adoção de padrão sem explicitação de custo;
- aumento de cerimônia sem redução equivalente de risco ou ambiguidade.

---

## Declaração operacional curta

A complexidade só entra quando paga aluguel.  
Antes disso, a postura correta da engenharia é preservar simplicidade, legibilidade e proporcionalidade.