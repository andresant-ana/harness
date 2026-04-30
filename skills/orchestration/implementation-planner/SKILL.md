# Skill — Implementation Planner

## Finalidade

Esta skill orienta a criação de um Execution Plan a partir de uma demanda, Implementation Packet, issue, ticket, contexto de workspace ou pedido direto do humano.

Seu papel é transformar intenção em plano executável, revisável e proporcional ao risco, impedindo que o agente pule de desejo para mutação sem discovery, sem escopo e sem estratégia de validação.

---

## Quando usar

Use esta skill quando:

- a task não for trivial;
- houver mudança em código, documentação, arquitetura, operação ou configuração;
- for necessário produzir Execution Plan antes de implementar;
- houver risco R1 ou superior;
- a demanda envolver múltiplos arquivos, módulos ou decisões;
- o humano pedir um plano antes da execução;
- o Core Architect precisar revisar a estratégia antes da mutação.

---

## Quando não usar

Não use esta skill quando:

- a task for puramente investigativa R0;
- a saída esperada for apenas Investigation Note;
- já existir Execution Plan aprovado e ainda válido;
- a demanda estiver vaga demais para planejar sem intake adicional;
- a decisão depender de trade-off estratégico ainda não resolvido.

---

## Inputs esperados

A skill pode consumir:

- objetivo da task;
- Implementation Packet;
- issue ou ticket;
- contexto do workspace;
- authority sources;
- PROJECT_STATE.md;
- discovery inicial;
- restrições conhecidas;
- classe de risco preliminar.

---

## Método

### 1. Enquadrar a demanda

Antes de planejar, identificar:

- o que precisa ser resolvido;
- por que a task existe;
- o que está dentro do escopo;
- o que está fora do escopo;
- quais critérios de aceite existem;
- qual classe de risco preliminar se aplica.

Se a demanda não permitir responder isso minimamente, não produzir plano fingindo certeza.

### 2. Confirmar fontes de autoridade

Localizar ou solicitar:

- authority files;
- authority commands;
- documentação local relevante;
- estrutura do projeto;
- contexto técnico atual;
- comandos reais de validação.

Conhecimento genérico nunca deve vencer verdade local.

### 3. Fazer discovery proporcional

O discovery deve ser suficiente para entender:

- topologia relevante;
- áreas candidatas de impacto;
- arquivos ou módulos prováveis;
- riscos conhecidos;
- lacunas;
- pontos sensíveis.

Discovery não é leitura massiva.  
Discovery é mapa operacional.

### 4. Validar ou corrigir a classe de risco

A classe de risco preliminar deve ser confirmada ou ajustada com base no discovery.

Se o risco subir, o plano deve refletir maior rigor.

### 5. Definir hipótese operacional

Escolher uma abordagem concreta e explicar por que ela é proporcional.

A hipótese deve evitar:

- over-engineering;
- abstração preventiva;
- dependência nova desnecessária;
- refactor lateral;
- alteração fora do escopo.

### 6. Definir escopo operacional

Registrar claramente:

- o que será feito;
- o que não será feito;
- quais áreas ou arquivos devem ser tocados;
- quais áreas devem ser evitadas.

### 7. Definir etapas de execução

As etapas devem ser pequenas, ordenadas e revisáveis.

Cada etapa deve ter causalidade com o objetivo da task.

### 8. Definir validação

Planejar validação proporcional:

- build;
- test;
- lint;
- format;
- diff review;
- checagem funcional;
- checagem de segurança;
- checagem operacional;
- documentação ou state update.

### 9. Definir critérios de escalonamento

Registrar sinais que exigem pausa, replanejamento ou Escalation Note.

### 10. Produzir Execution Plan

Usar o schema canônico de Execution Plan.

---

## Checklist de qualidade

Antes de entregar o plano, verificar:

- o problema real foi entendido?
- o escopo está delimitado?
- o fora de escopo está explícito?
- o discovery foi suficiente?
- a classe de risco faz sentido?
- há hipótese operacional clara?
- as etapas são executáveis?
- a validação é proporcional?
- há critérios de escalonamento?
- o plano evita complexidade sem dor real?
- o plano ajuda review futuro?

---

## Outputs esperados

Output principal:

- Execution Plan.

Outputs secundários possíveis:

- Escalation Note;
- Investigation Note;
- recomendação de Core Architect;
- lista de lacunas antes da execução.

---

## Critérios de escalonamento

Escalar quando:

- a task revelar risco R3 ou R4;
- houver decisão arquitetural relevante;
- houver conflito entre simplicidade e sofisticação;
- houver risco de segurança não trivial;
- houver impacto operacional importante;
- o discovery não permitir plano confiável;
- a task exigir produção, segredo ou ação sensível;
- houver necessidade de mudar escopo.

---

## Anti-patterns

Evitar:

- plano genérico;
- plano bonito sem arquivos ou áreas-alvo;
- plano que não cita validação;
- plano que ignora authority sources;
- plano que transforma feature simples em arquitetura pesada;
- plano que esconde incerteza;
- plano que tenta resolver várias tasks de uma vez;
- plano escrito depois que a mutação já começou.

---

## Declaração operacional curta

Planejar é transformar intenção em caminho verificável.  
Um bom Execution Plan reduz improviso, risco e entropia antes da primeira mutação.