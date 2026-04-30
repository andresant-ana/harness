# Schema — Project State Entry

## Finalidade

O Project State Entry é o schema canônico para registrar mudanças duráveis no estado técnico e operacional de um projeto.

Seu papel é orientar como uma task, investigação, decisão, risco ou entrega deve ser incorporada ao `PROJECT_STATE.md` do workspace quando alterar a realidade do projeto.

O Project State Entry não substitui o `PROJECT_STATE.md`.  
Ele define como uma nova entrada ou atualização de estado deve ser escrita.

---

## Quando deve ser usado

O Project State Entry deve ser usado quando uma task produzir informação durável sobre o projeto, como:

- mudança arquitetural;
- mudança de módulo, boundary ou fluxo;
- novo risco conhecido;
- nova limitação técnica;
- alteração de comandos locais;
- alteração de execution model;
- mudança em integração externa;
- descoberta factual relevante;
- decisão técnica que precisa sobreviver à sessão;
- dívida técnica assumida conscientemente;
- follow-up estrutural necessário.

---

## Papel no fluxo

No fluxo canônico, o Project State Entry pode ser derivado de:

- Completion Packet;
- Investigation Note;
- Review Report;
- Escalation Note;
- ADR;
- atualização de board;
- decisão do Core Architect;
- revisão humana.

Ele serve para transformar saída de task em memória operacional durável.

---

## Diferença entre Project State Entry e Completion Packet

O Completion Packet encerra uma task.  
O Project State Entry atualiza o estado durável do projeto.

Nem todo Completion Packet gera Project State Entry.  
Só gera quando a task muda algo que precisa ser lembrado depois.

Exemplo:

- corrigir typo local: normalmente não gera Project State Entry.
- alterar estrutura de módulos: gera.
- descobrir que uma migration depende de comando específico: gera.
- confirmar uma limitação operacional: gera.
- implementar detalhe interno sem impacto durável: talvez não gere.

---

## Diferença entre Project State Entry e board

Board registra estado de trabalho.  
Project State Entry registra estado técnico e operacional.

O board responde:
- o que está planejado?
- o que está em andamento?
- o que foi concluído?
- qual issue representa a task?

O Project State Entry responde:
- em que estado técnico o projeto ficou?
- que decisão agora é verdadeira?
- que risco passou a existir?
- que limitação precisa ser lembrada?
- que comando, boundary ou comportamento mudou?

---

## Campos obrigatórios

### 1. Data ou referência temporal
Quando a entrada foi criada ou atualizada.

Pode ser:
- data;
- commit;
- issue;
- PR;
- milestone;
- ou identificador de task.

### 2. Origem da entrada
De onde a atualização veio.

Exemplos:
- Completion Packet;
- Investigation Note;
- Review Report;
- Escalation Note;
- decisão humana;
- decisão do Core Architect;
- ADR;
- issue;
- PR.

### 3. Tipo de atualização
Classificação da entrada.

Valores recomendados:
- estado técnico;
- decisão;
- risco;
- limitação;
- dívida técnica;
- comando;
- integração;
- arquitetura;
- operação;
- segurança;
- follow-up.

### 4. Resumo
Resumo curto e claro do que mudou ou foi descoberto.

### 5. Descrição
Explicação objetiva do estado novo.

### 6. Impacto
O que essa entrada muda na forma de entender, operar ou evoluir o projeto.

### 7. Área afetada
Módulo, diretório, contexto, domínio, serviço, integração ou superfície operacional impactada.

### 8. Status
Estado atual da entrada.

Valores recomendados:
- ativo;
- resolvido;
- substituído;
- obsoleto;
- em observação;
- pendente de decisão.

### 9. Próxima ação
Se houver continuidade necessária, registrar qual é.

### 10. Referências
Links, arquivos, commits, issues, PRs, ADRs ou artifacts relacionados.

---

## Campos recomendados

### 11. Classe de risco relacionada
R0, R1, R2, R3 ou R4, quando aplicável.

### 12. Pressões reais associadas
Indicar se a entrada se relaciona com:
- concorrência;
- throughput;
- latência;
- consistência;
- observabilidade;
- estado local;
- runtime;
- cloud;
- segurança;
- custo de complexidade;
- entropia.

### 13. Decisão associada
Se a entrada registra ou deriva de uma decisão, registrar a decisão de forma curta.

### 14. Alternativas rejeitadas
Quando relevante, registrar caminhos descartados.

### 15. Critério de revisão futura
Quando essa entrada deve ser revisitada.

Exemplos:
- após MVP;
- antes de produção;
- após primeira carga real;
- após integração X;
- quando a segunda ocorrência aparecer;
- quando o risco deixar de ser hipotético.

---

## O que o Project State Entry não deve ser

Não deve ser:

- log de tudo que aconteceu;
- changelog detalhado de arquivos;
- duplicação do Completion Packet;
- cópia de issue;
- board paralelo;
- diário de sessão;
- despejo de conversa com agente.

O `PROJECT_STATE.md` deve ser memória operacional, não cemitério de detalhes.

---

## Qualidade esperada

Um bom Project State Entry deve ser:

- durável;
- factual;
- curto;
- contextual;
- acionável;
- fácil de revisar no futuro;
- ligado a referência verificável.

Uma entrada ruim:

- registra detalhe efêmero;
- não diz impacto;
- não tem status;
- não informa origem;
- não ajuda decisão futura;
- aumenta ruído em vez de memória útil.

---

## Critério para decidir se deve atualizar PROJECT_STATE

Atualize quando a informação for útil para uma futura sessão, futuro agente ou futuro humano entender o projeto melhor.

Perguntas de decisão:

1. isso muda como o projeto deve ser operado?
2. isso muda como o projeto deve ser evoluído?
3. isso muda comandos, riscos, boundaries ou arquitetura?
4. isso registra uma decisão que evitará rediscussão futura?
5. isso evita que outro agente investigue tudo de novo?
6. isso explica uma limitação ou dívida consciente?
7. isso ajuda a entender o estado real atual do sistema?

Se a resposta for “sim” para uma dessas perguntas, provavelmente merece entrada.

---

## Relação com arquitetura por dor real

Project State Entry também serve para registrar dores reais.

Quando uma dor técnica aparecer, mas ainda não justificar abstração, ela pode ser registrada como:

- risco em observação;
- limitação conhecida;
- dívida consciente;
- critério para revisão futura.

Isso impede dois erros:
- esquecer a dor;
- abstrair cedo demais.

---

## Relação com review

O reviewer deve verificar se uma task que mudou a realidade do projeto deixou state update quando necessário.

Sinais de ausência problemática:

- mudança arquitetural sem atualização de estado;
- novo risco conhecido sem registro;
- alteração de comandos sem documentação;
- nova integração sem memória operacional;
- dívida consciente não registrada.

---

## Template canônico

```md
# Project State Entry

## Data ou referência temporal
<data | commit | issue | PR | milestone | identificador>

## Origem da entrada
<completion packet | investigation note | review report | escalation note | decisão humana | ADR | issue | PR>

## Tipo de atualização
<estado técnico | decisão | risco | limitação | dívida técnica | comando | integração | arquitetura | operação | segurança | follow-up>

## Resumo
<resumo curto>

## Descrição
<descrição objetiva do estado novo>

## Impacto
<como isso muda entendimento, operação ou evolução do projeto>

## Área afetada
<módulo | contexto | diretório | serviço | integração | superfície operacional>

## Status
<ativo | resolvido | substituído | obsoleto | em observação | pendente de decisão>

## Classe de risco relacionada
R0 | R1 | R2 | R3 | R4 | não aplicável

## Pressões reais associadas
- <pressão 1>
- <pressão 2>

## Decisão associada
<decisão curta, se houver>

## Alternativas rejeitadas
- <alternativa 1>
- <alternativa 2>

## Próxima ação
<ação futura, se houver>

## Critério de revisão futura
<quando revisitar esta entrada>

## Referências
- <arquivo, commit, issue, PR, ADR, artifact ou link>
```

---

## Declaração operacional curta

Project State Entry transforma mudança relevante em memória durável.  
Ele existe para que o estado real do projeto sobreviva à task, à sessão e ao agente.