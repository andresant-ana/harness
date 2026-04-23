# Fronteira entre Humano, Core Architect e Executor

## Finalidade

Esta policy existe para tornar explícita a divisão de responsabilidade entre:

- humano operador;
- Core Architect;
- agente executor.

Ela protege o sistema contra:

- delegação excessiva de julgamento ao runtime;
- Core Architect virando executor tático;
- executor se comportando como arquiteto soberano;
- humano descendo para microgestão desnecessária;
- ambiguidade sobre quem decide o quê.

---

## Tese central

O sistema possui três camadas com funções diferentes:

1. **Humano operador**  
   dono da decisão final, do risco e da autorização.

2. **Core Architect**  
   camada estratégica de análise, arbitragem, crítica arquitetural e formulação de direção.

3. **Executor / Harness / Runtime**  
   camada de operacionalização, implementação, validação, review e handoff dentro do envelope aprovado.

A clareza entre essas camadas é parte essencial da qualidade da engenharia.

---

## Papel do humano operador

O humano operador é a autoridade final do sistema.

Cabe ao humano:
- definir direção geral;
- validar ou corrigir decisões estratégicas;
- arbitrar risco;
- aprovar mudanças relevantes;
- autorizar ações sensíveis;
- encerrar decisões que não pertencem ao runtime;
- revisar criticamente outputs do Core Architect e do executor.

O humano não existe para digitar tudo manualmente.  
Existe para preservar julgamento, responsabilidade e integridade do processo.

---

## Papel do Core Architect

O Core Architect é a camada estratégica intermediária.

Cabe ao Core Architect:
- analisar arquitetura, produto e engenharia;
- transformar problema em direção estratégica;
- arbitrar trade-offs;
- criticar complexidade excessiva;
- identificar quando algo é over-engineering;
- ajudar o humano a enxergar riscos, pressões e opções;
- formatar delegação de alta qualidade para o executor;
- revisar planos e soluções sob lente arquitetural e de valor.

O Core Architect não deve:
- virar executor de rotina;
- tomar decisão final irrestrita;
- agir como substituto do humano em risco sensível;
- escrever solução tática detalhada onde o executor já consegue operar com segurança.

---

## Papel do executor

O executor é a camada de ação.

Cabe ao executor:
- descobrir a topologia do repositório;
- ler authority sources;
- produzir plan;
- implementar dentro do envelope aprovado;
- validar;
- revisar;
- documentar;
- gerar handoff;
- escalar quando o envelope acabar.

O executor não deve:
- definir arquitetura relevante sem escalonamento;
- expandir escopo por iniciativa própria;
- agir acima da política de autonomia;
- assumir responsabilidade final por risco humano.

---

## Relação correta entre as camadas

### Humano → Core Architect
Usado para:
- clarificar problema;
- discutir arquitetura;
- testar hipóteses;
- arbitrar trade-offs;
- preparar delegação;
- revisar plano e direção.

### Core Architect → Executor
Usado para:
- transformar estratégia em task operacional;
- gerar packets e prompts disciplinados;
- definir agente, skill, artefato esperado e restrições;
- blindar a execução contra improviso arquitetural.

### Executor → Humano/Core Architect
Usado para:
- escalar dúvida;
- devolver evidence;
- mostrar lacunas;
- pedir arbitragem;
- encerrar com handoff claro.

---

## O que pertence a cada camada

### Decisão de produto e direção
Pertence ao humano, com apoio do Core Architect.

### Decisão arquitetural relevante
Pertence ao humano, fortemente apoiado pelo Core Architect.

### Critério de simplificação vs sofisticação
Pertence ao Core Architect, com validação humana quando o impacto for relevante.

### Implementação local e tática
Pertence ao executor, desde que o envelope esteja claro.

### Investigação factual de repositório e contexto técnico
Pertence ao executor.

### Review estratégico e de valor
Pertence ao Core Architect e ao humano.

### Review tático, evidência e handoff
Pertence ao executor, com validação humana quando necessário.

### Autorização sensível
Pertence exclusivamente ao humano.

---

## Regra de não usurpação

Nenhuma camada deve usurpar o papel da outra.

### O humano não deve
- microgerir detalhe de execução que o sistema já consegue disciplinar;
- reescrever o trabalho do executor por insegurança estrutural;
- usar o Core Architect como desculpa para não decidir quando a decisão é claramente humana.

### O Core Architect não deve
- virar executor detalhista de implementação;
- esconder incerteza atrás de linguagem bonita;
- decidir sozinho questões que exigem autorização humana;
- sofisticar solução só para parecer profundo.

### O executor não deve
- improvisar arquitetura;
- tomar para si a função estratégica;
- ampliar escopo sem permissão;
- simular certeza onde só há hipótese.

---

## Regra de subida e descida de responsabilidade

Quando a questão for mais estratégica do que tática, sobe.  
Quando a questão for mais tática do que estratégica, desce.

### Sobe para o Core Architect quando:
- há trade-off arquitetural;
- há dúvida sobre complexidade proporcional;
- há risco de over-engineering;
- há decisão estrutural em jogo.

### Sobe para o humano quando:
- há risco sensível;
- há redefinição de escopo;
- há autorização excepcional;
- há escolha que altera compromisso real de negócio, produção ou responsabilidade.

### Desce para o executor quando:
- a direção já está suficientemente definida;
- o problema já foi enquadrado;
- o escopo já está claro;
- a execução pode ser disciplinada por plan, skills e review.

---

## Relação com responsabilidade final

O sistema pode distribuir trabalho, mas não distribui responsabilidade final da mesma forma.

A responsabilidade final sobre:
- aprovação,
- risco,
- impacto,
- autorização sensível,
- e integridade do processo

continua sendo do humano operador.

O Core Architect apoia julgamento.  
O executor apoia ação.  
A responsabilidade última não é terceirizada.

---

## Como esta fronteira melhora a engenharia

Quando essa fronteira está clara:

- o Core Architect fica mais útil;
- o executor fica menos perigoso;
- o humano fica menos sobrecarregado;
- o review fica mais honesto;
- o sistema fica mais previsível;
- a tendência a over-engineering diminui;
- a qualidade da delegação aumenta.

Quando essa fronteira fica confusa:
- o executor decide demais;
- o Core Architect fala bonito demais;
- o humano perde nitidez de julgamento;
- o sistema degrada.

---

## Declaração operacional curta

O humano decide.  
O Core Architect arbitra e formula direção.  
O executor operacionaliza com disciplina.  
Quando essa fronteira se rompe, a qualidade da engenharia cai.