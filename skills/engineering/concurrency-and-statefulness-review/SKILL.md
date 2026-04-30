# Skill — Concurrency and Statefulness Review

## Finalidade

Esta skill orienta a revisão de concorrência, estado local, compartilhamento de dados e comportamento sob múltiplas execuções simultâneas.

Seu papel é impedir que o agente construa soluções que funcionam em execução isolada, mas falham com requisições paralelas, múltiplas instâncias, workers concorrentes ou escala horizontal.

---

## Quando usar

Use esta skill quando a task tocar:

- estado em memória;
- cache local;
- sessão;
- singleton;
- static state;
- background worker;
- fila;
- processamento assíncrono;
- atualização concorrente;
- transação;
- lock;
- rate limit;
- idempotência;
- escala horizontal;
- múltiplas réplicas;
- consistência de dados;
- recursos compartilhados.

---

## Quando não usar

Não use esta skill quando:

- a mudança for puramente estática ou documental;
- não houver estado nem concorrência relevante;
- a execução for local, determinística e sem compartilhamento;
- a análise só adicionaria especulação.

---

## Tese central

Concorrência quebra suposições invisíveis.

Uma solução pode estar correta para um usuário, uma request e uma instância, mas incorreta para tráfego real.

A pergunta correta é:

“o que acontece quando isso roda ao mesmo tempo, em mais de um processo ou mais de uma instância?”

---

## Método

### 1. Identificar estado

Mapear se a mudança usa:

- variável global;
- static;
- singleton;
- cache local;
- arquivo local;
- sessão em memória;
- coleção mutável;
- recurso compartilhado;
- banco;
- fila;
- storage externo.

---

### 2. Identificar modelo de execução

Perguntar:

- roda em request web?
- roda em background?
- roda em job?
- roda em worker concorrente?
- roda em múltiplas réplicas?
- roda em container?
- roda em serverless?

---

### 3. Identificar acesso concorrente

Verificar:

- duas requests podem tocar o mesmo recurso?
- dois workers podem processar o mesmo item?
- duas instâncias podem escrever o mesmo dado?
- existe race condition?
- existe lost update?
- existe duplicidade?
- existe ordem assumida sem garantia?

---

### 4. Avaliar idempotência

Perguntar:

- se a operação rodar duas vezes, o resultado fica correto?
- se a mensagem for reentregue, há duplicidade?
- se o retry acontecer depois de falha parcial, o sistema se corrompe?
- há chave de idempotência ou constraint?

---

### 5. Avaliar consistência

Classificar necessidade:

- consistência forte;
- consistência eventual;
- ordem garantida;
- ordem irrelevante;
- conflito aceitável;
- conflito inaceitável.

---

### 6. Avaliar escala horizontal

Perguntar:

- a solução depende de memória local?
- depende de arquivo local?
- depende de affinity?
- depende de cache por instância?
- funciona com duas réplicas?
- funciona após restart?

---

### 7. Definir mitigação proporcional

Possíveis ações:

- remover estado local;
- usar banco como fonte de verdade;
- usar constraint;
- usar lock com cuidado;
- tornar operação idempotente;
- limitar concorrência;
- registrar risco;
- escalar decisão.

---

## Output esperado

```md
# Concurrency and Statefulness Review

## Modelo de execução
<request | worker | job | container | serverless | outro>

## Estado identificado
- <estado 1>
- <estado 2>

## Risco de concorrência
- <risco 1>
- <risco 2>

## Risco de escala horizontal
- <risco 1>
- <risco 2>

## Idempotência
<suficiente | insuficiente | não aplicável | incerto>

## Consistência esperada
<forte | eventual | ordem necessária | ordem irrelevante | incerto>

## Mitigação recomendada
- <ação 1>
- <ação 2>

## Veredito
<suficiente | ajustar | escalar>
```

---

## Checklist de qualidade

Antes de aceitar a solução, verificar:

- há estado local mutável?
- há singleton perigoso?
- há static state?
- há cache sem invalidação?
- há risco de lost update?
- há risco de duplicidade?
- a operação é idempotente?
- funciona em múltiplas réplicas?
- funciona após restart?
- a consistência necessária está clara?
- há teste ou validação proporcional?

---

## Critérios de escalonamento

Escalar quando:

- houver risco de corrupção de dado;
- houver necessidade de lock distribuído;
- houver disputa entre consistência forte e throughput;
- houver escolha entre fila, transação, evento ou chamada direta;
- a solução depender de estado local em ambiente escalável;
- houver falha parcial com retry e duplicidade;
- a decisão afetar arquitetura de runtime.

---

## Anti-patterns

Evitar:

- cache local como fonte de verdade;
- estado em memória para fluxo crítico;
- assumir execução única;
- assumir ordem de mensagens sem garantia;
- ignorar retry;
- usar lock sem entender escopo;
- resolver concorrência só com delay;
- depender de sticky session sem decisão explícita;
- tratar serverless/container como se fosse processo fixo único.

---

## Declaração operacional curta

Concorrência exige pensar além do caminho feliz.  
O harness deve proteger o sistema contra estado invisível, race conditions e suposições de instância única.