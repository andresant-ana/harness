# Skill — Delivery Wrapup

## Finalidade

Esta skill orienta o encerramento de uma task com Completion Packet, handoff, lacunas explícitas, riscos remanescentes e possível atualização de estado do projeto.

Seu papel é impedir que a execução termine com resumo genérico, otimismo verbal ou perda de continuidade.

---

## Quando usar

Use esta skill quando:

- uma implementação foi concluída;
- uma investigação terminou;
- uma review foi realizada;
- uma task foi bloqueada;
- houve divergência em relação ao plano;
- é necessário preparar commit, PR ou handoff;
- algo pode precisar virar Project State Entry;
- o humano precisa entender o estado final sem reconstruir a sessão.

---

## Quando não usar

Não use esta skill para:

- mascarar falta de validação;
- substituir review técnico;
- transformar uma execução ruim em narrativa bonita;
- encerrar task que ainda exige Escalation Note;
- copiar transcript bruto para o handoff.

---

## Tese central

Entrega boa não é só código alterado.  
Entrega boa deixa continuidade, evidência e risco residual claros.

---

## Método

### 1. Reconstituir objetivo e escopo

Registrar:

- qual era o objetivo;
- o que estava dentro do escopo;
- o que estava fora;
- qual classe de risco foi usada.

### 2. Resumir o que foi feito

Listar mudanças factuais.

Evitar linguagem vaga como:

- “ajustes gerais”;
- “melhorias diversas”;
- “refatorações necessárias”.

### 3. Registrar o que não foi feito

Explicitar:

- itens fora de escopo;
- validações não realizadas;
- follow-ups;
- decisões adiadas;
- riscos aceitos.

### 4. Listar arquivos ou áreas tocadas

Agrupar por área, não necessariamente listar cada arquivo se isso gerar ruído.

### 5. Registrar validações

Separar:

- validações realizadas;
- validações não realizadas;
- motivo das lacunas;
- risco residual.

### 6. Comparar com o plano

Registrar divergências em relação ao Execution Plan.

Se houve desvio não aprovado, isso deve aparecer.

### 7. Avaliar necessidade de Project State Entry

Perguntar:

- a task mudou realidade durável do projeto?
- alterou arquitetura, boundary, comando, risco, integração ou operação?
- revelou limitação importante?
- criou dívida consciente?
- evitaria reinvestigação futura?

Se sim, propor Project State Entry.

### 8. Preparar próximo passo

Indicar:

- commit;
- review;
- PR;
- nova task;
- Escalation Note;
- atualização de board;
- atualização de PROJECT_STATE;
- validação adicional.

---

## Outputs esperados

Output principal:

- Completion Packet.

Outputs possíveis:

- Project State Entry;
- Review Report summary;
- Escalation Note;
- sugestão de commit message;
- handoff para Core Architect;
- handoff para humano operador.

---

## Checklist de encerramento

Antes de encerrar, confirmar:

- o objetivo foi atendido?
- o escopo foi respeitado?
- o que foi feito está claro?
- o que não foi feito está claro?
- as validações estão registradas?
- lacunas foram assumidas?
- risco residual foi declarado?
- divergências do plan foram explicadas?
- state update foi considerado?
- há próximo passo claro?

---

## Handoff por situação

### Task concluída

Produzir Completion Packet com:

- resumo;
- mudanças;
- validações;
- riscos;
- próximo passo.

### Task bloqueada

Produzir handoff com:

- onde parou;
- por que parou;
- o que foi tentado;
- o que falta decidir;
- recomendação de destravamento.

### Task investigativa

Produzir Investigation Note com:

- fontes;
- fatos;
- hipóteses;
- lacunas;
- recomendação.

### Task com decisão pendente

Produzir Escalation Note com:

- motivo;
- opções;
- trade-offs;
- pergunta exata.

---

## Sugestão de commit

Quando apropriado, sugerir commit message curta e causal.

Exemplos bons:

- `adiciona skills de orchestration do harness`
- `fecha núcleo canônico inicial do harness`
- `normaliza quebras de linha do repositório`

Exemplos ruins:

- `updates`
- `fix`
- `ajustes`
- `mudanças`

---

## Critérios de escalonamento

Escalar quando:

- a task não pode ser encerrada honestamente;
- há lacuna crítica de validação;
- há risco R3/R4 descoberto tarde;
- houve desvio grande do plan;
- a decisão final depende do Core Architect;
- o estado do projeto mudou, mas a atualização exige arbitragem.

---

## Anti-patterns

Evitar:

- handoff triunfalista;
- esconder teste não rodado;
- declarar “feito” sem critério de aceite;
- omitir risco residual;
- copiar transcript;
- colocar tudo no PROJECT_STATE;
- encerrar sem próximo passo;
- usar commit message genérica.

---

## Declaração operacional curta

Wrapup fecha a task sem apagar a verdade.  
Entrega madura deixa evidência, lacunas e continuidade.