# Protocolo de Leitura de Estado Externo

## Finalidade

Este protocolo define como o harness deve consultar fontes externas de estado, como GitHub Projects, issues, PRs, documentação externa, observabilidade read-only, cloud metadata e integrações via MCP.

Seu papel é permitir que o executor enxergue contexto externo útil sem confundir leitura com autoridade irrestrita ou automação write.

---

## Tese central

Estado externo pode reduzir incerteza, mas não substitui a verdade local do repositório.

O harness deve ler estado externo com:
- intenção clara;
- escopo delimitado;
- preferência read-only;
- respeito às policies de MCP;
- e separação entre gestão de trabalho e estado técnico.

---

## Fontes externas possíveis

Podem ser fontes externas:

- GitHub Projects;
- GitHub Issues;
- pull requests;
- documentação oficial;
- documentação de fornecedor;
- observabilidade;
- logs read-only;
- cloud metadata;
- painéis internos;
- trackers de tarefa;
- sistemas de incidentes;
- registros de deploy.

---

## Quando consultar estado externo

Consultar quando:

- a task depende de issue, board ou prioridade;
- é preciso saber o que já foi feito;
- há dúvida sobre status de trabalho;
- é necessário confirmar decisão externa;
- há documentação oficial relevante;
- há logs, métricas ou sinais operacionais necessários;
- a execução local não explica sozinha o problema.

---

## Quando não consultar

Não consultar quando:

- a informação necessária está claramente no repo;
- a consulta externa é curiosidade;
- o custo de contexto não compensa;
- o agente está usando fonte externa para evitar discovery local;
- a integração não é confiável;
- a consulta pode expor ou ampliar risco sem necessidade.

---

## Ordem correta de leitura

### 1. Definir pergunta

Antes de consultar, o sistema deve saber:
- o que quer descobrir?
- por que isso é necessário?
- como essa resposta mudará o plan ou review?

### 2. Escolher fonte mínima

Preferir a fonte mais direta e confiável.

### 3. Ler em modo restrito

Preferir read-only, filtros estreitos e escopo mínimo.

### 4. Separar fato de interpretação

Estado externo pode informar, mas ainda precisa ser interpretado à luz do projeto.

### 5. Registrar uso

Se a leitura afetou decisão, registrar no artifact correspondente.

---

## GitHub Projects

GitHub Projects deve ser usado para entender:

- backlog;
- status de tasks;
- prioridade;
- sequência de trabalho;
- dependências entre issues;
- o que foi concluído ou pendente.

Não deve ser usado como fonte primária de arquitetura.

Board informa trabalho.  
Repositório informa implementação.  
`PROJECT_STATE.md` informa estado técnico durável.

---

## GitHub Issues e PRs

Issues e PRs podem informar:

- contexto da task;
- histórico de decisão;
- critérios de aceite;
- discussões relevantes;
- mudanças recentes;
- pendências;
- decisões de review.

Mas comentários antigos podem estar desatualizados.  
A leitura deve considerar data, contexto e relação com o estado atual do repositório.

---

## Documentação externa

Documentação externa deve ser usada quando:

- a task depende de API, framework, provider ou ferramenta;
- há dúvida factual sobre comportamento;
- há risco de usar conhecimento genérico desatualizado;
- há mudança recente de versão, SDK, CLI ou serviço.

A preferência deve ser por fontes oficiais ou altamente confiáveis.

---

## Observabilidade read-only

Observabilidade read-only pode ser usada para:

- entender falha;
- confirmar sintoma;
- comparar comportamento esperado e observado;
- apoiar investigação;
- validar hipótese operacional.

Deve ser usada com cuidado para não vazar dados sensíveis ou extrapolar além do sinal observado.

---

## Cloud metadata read-only

Cloud metadata pode ser usada para:

- confirmar configuração;
- entender runtime;
- verificar topologia;
- checar recurso, região, deployment target ou integration point.

Não deve se transformar em mutação de cloud sem política específica e autorização.

---

## Relação com MCP

Toda leitura externa via MCP deve respeitar:

- `03-mcp-policy.md`;
- princípio read-only first;
- menor privilégio;
- trusted integrations;
- registro de fonte consultada;
- limite de escopo.

MCP deve ampliar visão, não autonomia.

---

## Relação com evidência

Leitura externa pode gerar evidência quando:

- a fonte é confiável;
- a pergunta era clara;
- a resposta foi interpretada corretamente;
- a consulta foi relevante para a decisão.

Não basta citar fonte externa.  
É preciso explicar o que ela confirma ou não confirma.

---

## Relação com context economy

Estado externo pode inflar contexto rapidamente.

Por isso, o sistema deve evitar:
- abrir várias issues sem critério;
- importar board inteiro;
- despejar logs extensos;
- carregar documentação longa sem necessidade;
- tratar histórico externo como verdade permanente.

---

## Relação com artifacts

Quando a leitura externa influenciar decisão, ela deve aparecer em:

- Implementation Packet;
- Investigation Note;
- Execution Plan;
- Review Report;
- Escalation Note;
- Completion Packet;
- Project State Entry, se for durável.

---

## Sinais de mau uso

O uso está ruim quando:

- o agente consulta fontes externas sem pergunta clara;
- board substitui entendimento do código;
- documentação externa substitui authority source local;
- logs são lidos sem hipótese;
- MCP vira atalho para agir sem governança;
- estado externo desatualizado é tratado como verdade atual.

---

## Declaração operacional curta

Estado externo serve para reduzir incerteza.  
Ele não substitui discovery local, authority sources ou julgamento humano.  
O harness lê fora para decidir melhor dentro.