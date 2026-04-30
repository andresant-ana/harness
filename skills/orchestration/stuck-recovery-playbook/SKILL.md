# Skill — Stuck Recovery Playbook

## Finalidade

Esta skill orienta a detecção e recuperação de travamento durante investigação, planejamento, execução, validação ou review.

Seu papel é impedir que o agente continue tentando aleatoriamente, aumentando contexto, mutando arquivos sem causalidade ou transformando bug em refactor.

---

## Quando usar

Use esta skill quando:

- a mesma falha aparecer mais de uma vez;
- o agente estiver repetindo comandos sem aprendizado;
- o contexto estiver crescendo sem clareza;
- a execução desviou do plan;
- a validação falhou sem hipótese nova;
- a task começou a expandir escopo;
- houver mutação especulativa;
- o agente não souber mais qual é a causa do problema;
- o humano perceber que a execução está girando em falso.

---

## Quando não usar

Não use esta skill quando:

- a task está progredindo normalmente;
- há uma falha simples com causa clara;
- o plan ainda explica bem a realidade;
- a execução só precisa de validação final;
- a pausa criaria mais custo do que benefício.

---

## Tese central

Quando não há convergência, continuar produzindo ação não é produtividade.

Travamento exige pausa, reconstrução factual, redução de escopo e nova estratégia.

---

## Sinais de travamento

Tratar como sinais fortes:

- repetição da mesma tentativa;
- comandos sem insight novo;
- arquivos abertos sem mapa;
- edição “para ver se resolve”;
- erro recorrente;
- troca de hipótese sem registro;
- plano original deixando de fazer sentido;
- task simples virando reestruturação;
- linguagem confiante sem evidência.

---

## Método de recuperação

### 1. Parar mutação

Interromper alterações especulativas.

Antes de editar mais, entender o estado.

### 2. Reconstituir o estado atual

Responder:

- qual era o objetivo?
- qual era o plan?
- o que foi tentado?
- o que falhou?
- o que funcionou?
- quais arquivos foram tocados?
- qual erro permanece?

### 3. Separar fato de hipótese

Registrar:

- fatos confirmados;
- hipóteses plausíveis;
- hipóteses descartadas;
- lacunas.

### 4. Verificar diff

Se houve mutação, inspecionar:

- o diff tem causalidade?
- há mudanças especulativas?
- algo deve ser revertido?
- a task misturou assuntos?

### 5. Reclassificar risco

Perguntar:

- a classe de risco subiu?
- virou R2, R3 ou R4?
- precisa de Core Architect?
- precisa de Escalation Note?

### 6. Escolher estratégia

Opções:

- voltar para discovery;
- reduzir escopo;
- isolar subproblema;
- reverter mutação especulativa;
- produzir Investigation Note;
- produzir Escalation Note;
- pedir revisão;
- abrir nova task.

### 7. Retomar com novo plano

Não continuar como se nada tivesse acontecido.

Retomar apenas com:

- plano ajustado;
- hipótese nova;
- escopo reduzido;
- ou escalonamento.

---

## Estratégias recomendadas

### Voltar para discovery

Use quando a causa ainda não está entendida.

### Reduzir escopo

Use quando a task ficou ampla demais.

### Isolar subproblema

Use quando há múltiplos sintomas misturados.

### Reverter experimento

Use quando mudanças recentes não têm evidência.

### Gerar Investigation Note

Use quando a saída mais útil agora é conhecimento factual.

### Gerar Escalation Note

Use quando a decisão saiu da autonomia do executor.

---

## Output esperado

A skill pode produzir:

- diagnóstico de travamento;
- resumo do estado atual;
- lista de tentativas;
- hipóteses e lacunas;
- novo plano reduzido;
- Investigation Note;
- Escalation Note;
- recomendação de revert parcial;
- Completion Packet com bloqueio.

---

## Checklist de recuperação

Antes de retomar, confirmar:

- sabemos o que falhou?
- sabemos o que foi tentado?
- há hipótese nova?
- o escopo foi controlado?
- o risco foi reclassificado?
- o diff ainda é confiável?
- há mutações a reverter?
- é melhor escalar?
- o próximo passo é factual e não especulativo?

---

## Critérios de escalonamento

Escalar quando:

- o problema depende de decisão arquitetural;
- a solução exigiria refactor amplo;
- há risco de segurança;
- há risco operacional;
- a validação essencial não converge;
- o agente não consegue reduzir incerteza;
- a task está consumindo contexto sem progresso;
- a execução exigiria produção, segredo ou ação sensível.

---

## Anti-patterns

Evitar:

- rodar o mesmo comando várias vezes sem hipótese;
- instalar dependência para contornar erro desconhecido;
- reescrever arquitetura para resolver bug local;
- abrir muitos arquivos sem mapa;
- esconder tentativas falhas;
- continuar editando sem entender causa;
- aumentar escopo para escapar do problema;
- declarar sucesso depois de travamento sem evidência forte.

---

## Declaração operacional curta

Travamento não se vence com insistência cega.  
O harness pausa, reconstrói fatos, reduz ruído e só então retoma ou escala.