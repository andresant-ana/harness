# Fluxo de Implementação

## Finalidade

Este protocolo define o fluxo operacional padrão do harness para transformar uma demanda em execução disciplinada, revisável e encerrável com evidência.

Seu papel é impedir que o sistema opere por improviso, saltando diretamente de intenção para mutação sem discovery, sem plano e sem handoff adequado.

---

## Tese central

Toda task relevante deve atravessar um fluxo previsível:

1. intake
2. discovery
3. plan
4. aprovação
5. execução
6. validação
7. review
8. handoff
9. atualização de estado, quando aplicável

Nem toda task exige o mesmo peso em cada etapa, mas toda task relevante deve respeitar essa lógica.

---

## Etapa 1 — Intake

### Objetivo
Receber e enquadrar a task.

### Inputs esperados
- objetivo;
- contexto;
- escopo;
- fora de escopo;
- critérios de aceite;
- classe de risco preliminar, se já existir;
- restrições conhecidas.

### Resultado esperado
Uma leitura inicial do problema, suficiente para decidir:
- se a task é realmente implementável;
- se precisa de discovery;
- se já há informação suficiente para produzir plan;
- se a questão é estratégica demais para o executor.

### Erros comuns
- começar a executar com input vago;
- tratar desejo genérico como task operacional;
- não delimitar fora de escopo;
- confundir decisão estratégica com implementação.

---

## Etapa 2 — Discovery

### Objetivo
Entender a topologia do repositório e localizar a verdade local antes de mutar.

### O que deve ser feito
- localizar authority files;
- localizar authority commands;
- identificar módulos, pastas e fronteiras relevantes;
- entender onde a mudança provavelmente tocará;
- identificar pontos sensíveis;
- estimar esforço e risco real.

### Resultado esperado
Mapa factual suficiente para produção de um Execution Plan coerente.

### Erros comuns
- abrir arquivos em massa sem direção;
- começar pelo detalhe sem entender a estrutura;
- inferir comportamento do sistema sem consultar authority sources.

---

## Etapa 3 — Plan

### Objetivo
Converter intenção em caminho operacional auditável.

### O que o plan deve responder
- qual é a leitura do problema;
- qual hipótese operacional será seguida;
- quais áreas serão afetadas;
- quais validações serão feitas;
- quais riscos existem;
- o que pode exigir escalonamento;
- qual budget operacional está implícito;
- qual impacto em segurança, operação e entropia é esperado.

### Resultado esperado
Execution Plan com clareza suficiente para revisão e aprovação.

### Erros comuns
- plano genérico demais;
- plano com passos bonitos, mas sem causalidade;
- plano sem risco, sem validação ou sem fronteiras de escopo.

---

## Etapa 4 — Aprovação

### Objetivo
Garantir que a execução só comece dentro de um envelope aprovado.

### Quando aprovação é obrigatória
- sempre que a task for acima do trivial;
- quando houver risco R2 ou superior;
- quando houver impacto estrutural;
- quando a classe de risco for incerta;
- quando a solução puder aumentar complexidade relevante.

### Quem aprova
- humano operador;
- com apoio do Core Architect quando houver trade-off arquitetural ou risco estrutural.

### Resultado esperado
Execução autorizada dentro de um envelope claro.

---

## Etapa 5 — Execução

### Objetivo
Implementar apenas o que foi aprovado, com disciplina de escopo, contexto e causalidade.

### Regras da execução
- mutar o mínimo necessário;
- respeitar a verdade local do projeto;
- não expandir escopo silenciosamente;
- registrar evidência enquanto executa;
- parar para replanejar ou escalar se o envelope deixar de servir.

### Resultado esperado
Mudança implementada sem desvio oculto.

### Erros comuns
- “resolver mais coisas” por entusiasmo;
- começar a arquitetar no meio da execução;
- acumular mudanças não previstas sem comunicar;
- tratar o plan como mera formalidade.

---

## Etapa 6 — Validação

### Objetivo
Demonstrar, de forma proporcional ao risco, que a mudança foi de fato verificada.

### Validação pode incluir
- build;
- test;
- lint;
- format;
- leitura de diff;
- checagens de segurança;
- comandos locais reais;
- validação funcional;
- validação de impacto operacional.

### Resultado esperado
Base factual para o Completion Packet.

### Regra importante
Validação insuficiente precisa ser explicitada, não escondida.

---

## Etapa 7 — Review

### Objetivo
Submeter a mudança a uma leitura conservadora.

### O review deve observar
- aderência ao plan;
- coerência com o sistema local;
- risco residual;
- regressão plausível;
- segurança;
- clareza;
- slop introduzido;
- complexidade desnecessária;
- evidência forte ou fraca.

### Resultado esperado
Aprovação, ressalva, reavaliação ou bloqueio.

---

## Etapa 8 — Handoff

### Objetivo
Encerrar a task de forma que outro humano ou agente consiga continuar com clareza.

### O handoff deve responder
- o que mudou;
- por que mudou;
- como foi validado;
- o que não foi validado;
- que risco permanece;
- qual é o próximo passo;
- se há pendência de documentação ou state update.

### Resultado esperado
Completion Packet claro, útil e honesto.

---

## Etapa 9 — Atualização de estado

### Objetivo
Atualizar o estado durável do projeto quando a task mudar a realidade técnica ou operacional.

### Quando atualizar
- quando a task altera arquitetura local;
- quando muda comandos, riscos ou execution model;
- quando muda o estado técnico geral do projeto;
- quando uma decisão relevante precisa virar memória durável.

### Artefatos típicos
- `PROJECT_STATE.md`
- documentação local
- contexto do board, quando aplicável
- authority sources do workspace

---

## Regra de proporcionalidade

Nem toda task terá o mesmo peso documental, mas nenhuma task relevante pode:

- pular discovery;
- pular plan;
- pular evidência;
- pular handoff;
- ou tratar review como acessório.

A diferença entre task leve e task pesada está no grau, não na lógica do fluxo.

---

## Declaração operacional curta

Intenção entra.  
Discovery enquadra.  
Plan organiza.  
Aprovação limita.  
Execução realiza.  
Validação prova.  
Review protege.  
Handoff preserva continuidade.