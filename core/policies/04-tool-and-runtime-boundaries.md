# Limites de Ferramentas e Runtime

## Finalidade

Esta policy define as fronteiras entre:
- o núcleo canônico do harness;
- o runtime concreto;
- ferramentas auxiliares;
- plugins;
- integrações;
- e superfícies externas.

Seu papel é impedir:
- acoplamento excessivo a uma ferramenta específica;
- confusão entre engenharia e adapter;
- dependência estrutural de UX, CLI ou recurso transitório do runtime;
- expansão descontrolada da superfície operacional.

---

## Tese central

Ferramenta é meio.  
Runtime é adapter.  
O núcleo da engenharia vale mais do que qualquer implementação concreta.

Por isso, a engenharia deve preservar:
- independência conceitual;
- portabilidade;
- governabilidade;
- e clareza entre o que é canônico e o que é específico do runtime.

---

## Regra operacional principal

Sempre que houver dúvida entre:
- modelar algo no núcleo,
- ou modelar algo no runtime,

a decisão correta é perguntar:

1. isso é durável entre projetos?
2. isso é conceitual ou é detalhe de implementação?
3. isso continuaria verdadeiro se o runtime mudasse?
4. isso é lei do sistema ou conveniência da ferramenta?

Se a resposta pender para durabilidade e independência, pertence ao núcleo.  
Se pender para semântica operacional específica, pertence ao adapter.

---

## O que pertence ao núcleo canônico

Pertencem ao núcleo:

- missão;
- princípios;
- leis operacionais;
- classes de risco;
- protocolos;
- policies;
- artifacts;
- taxonomias;
- contratos canônicos de agentes;
- skills globais;
- templates;
- governança.

Esses elementos não devem depender de:
- sintaxe de CLI;
- formato de plugin;
- UX específica do runtime;
- detalhe acidental de uma ferramenta.

---

## O que pertence ao adapter do runtime

Pertence ao adapter:

- AGENTS.md do runtime;
- opencode.json;
- wiring de agents;
- commands do runtime;
- configuração de permissões;
- plugin loading;
- surface de MCP específica da ferramenta;
- nomes e atalhos operacionais dependentes da CLI.

O adapter existe para traduzir a engenharia para o runtime, não para redefini-la.

---

## O que pertence ao workspace do projeto

Pertence ao workspace:

- architecture local;
- authority sources;
- authority commands;
- project state;
- operational reality;
- comandos específicos do projeto;
- riscos locais;
- peculiaridades do repositório;
- critérios locais de done.

O harness não deve absorver verdade local de projeto.

---

## Fronteira entre ferramenta e julgamento

Ferramenta pode:
- acelerar execução;
- ampliar contexto;
- melhorar ergonomia;
- automatizar repetição.

Ferramenta não pode:
- substituir julgamento humano;
- legitimar complexidade ruim;
- definir arquitetura por conta própria;
- virar critério de qualidade.

A engenharia rejeita tool worship.

---

## IDE, terminal, dashboards e inspeção

A engenharia reconhece que o centro de gravidade da execução pode migrar da IDE para orquestração, terminal e painel de agentes. Ainda assim, nenhuma ferramenta de inspeção substitui:
- review humano;
- leitura crítica;
- validação proporcional;
- entendimento de sistema real.

A IDE pode deixar de ser o centro da digitação, mas continua sendo superfície válida de inspeção, revisão e diagnóstico.

---

## Plugins e extensões

Plugins devem ser tratados como superfície opcional, não como fundamento do sistema.

Antes de adotar plugin, o harness deve perguntar:
- isso reduz fricção real?
- isso cria acoplamento estrutural?
- isso altera risco?
- isso complica portabilidade?
- isso é necessário agora?

Plugin não deve virar muleta para falha de arquitetura canônica.

---

## Ferramentas auxiliares

Ferramentas auxiliares de:
- observabilidade;
- profiling;
- build;
- segurança;
- integração;
- documentação;
- cloud inspection

são legítimas quando têm função clara e risco compreendido.

Mas o harness não deve pressupor sua presença universal sem:
- documentação;
- classificação;
- e boundary claro.

---

## Relação com MCP

MCP é parte da superfície do runtime, não do núcleo conceitual do sistema.

O núcleo define:
- a política;
- os limites;
- a governança.

O adapter define:
- como a integração é concretamente ligada ao runtime.

---

## Relação com evolução futura

Se um dia o runtime mudar, a engenharia deve continuar sendo compreensível e reaproveitável.

Esse é o teste de boundary saudável:
- se trocar o runtime e o sistema desmoronar conceitualmente, houve acoplamento demais;
- se trocar o runtime e só o adapter precisar ser refeito, a fronteira está correta.

---

## Sinais de boundary ruim

A fronteira está ruim quando:
- regra de engenharia vive apenas em config do runtime;
- skill depende de UX específica da ferramenta;
- agent canônico só faz sentido num provider;
- CLI e arquitetura começam a se confundir;
- o time passa a falar mais da ferramenta do que do sistema.

---

## Declaração operacional curta

O runtime executa.  
O adapter traduz.  
O núcleo governa.  
Quando essas fronteiras se misturam, a engenharia perde portabilidade, clareza e maturidade.