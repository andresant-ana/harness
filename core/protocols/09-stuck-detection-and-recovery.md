# Protocolo de Detecção e Recuperação de Travamento

## Finalidade

Este protocolo define como o harness deve detectar quando a execução está travada, improdutiva, girando em falso ou consumindo contexto sem convergir.

Seu papel é impedir que o agente continue insistindo em uma estratégia ruim apenas porque ainda consegue gerar texto, comandos ou tentativas.

---

## Tese central

Persistência sem convergência não é virtude.  
Quando o sistema para de produzir evidência, clareza ou progresso real, ele deve desacelerar, diagnosticar e mudar de estratégia.

Travamento bom é detectado cedo.  
Travamento ruim vira consumo de contexto, slop e risco.

---

## O que conta como travamento

A execução pode estar travada quando:

- várias tentativas falham pelo mesmo motivo;
- o agente repete comandos sem novo insight;
- o contexto cresce, mas a clareza não;
- o plan deixa de explicar a realidade encontrada;
- o executor muda coisas sem entender causalidade;
- a validação falha sem hipótese nova;
- o erro observado não está sendo reduzido;
- a task começa a expandir escopo para fugir do problema real.

---

## Sinais de travamento

### 1. Repetição sem aprendizado
O agente executa variações do mesmo passo sem extrair nova informação.

### 2. Crescimento de contexto sem decisão
Mais arquivos são abertos, mas o mapa do problema não melhora.

### 3. Mutação especulativa
O agente começa a alterar código para “ver se resolve”.

### 4. Mudança de hipótese sem registro
A estratégia muda, mas ninguém registra por que a hipótese anterior caiu.

### 5. Erro recorrente
Build, test, lint ou runtime continuam falhando sem redução causal do problema.

### 6. Escopo escorregando
A task começa a puxar refactors, reestruturações ou melhorias laterais.

### 7. Linguagem confiante com evidência fraca
O agente parece explicar bem, mas não demonstra progresso factual.

---

## Gatilhos de pausa

O executor deve pausar quando:

- a mesma falha ocorrer mais de uma vez sem nova hipótese;
- três ou mais ações consecutivas não produzirem clareza nova;
- a classe de risco parecer ter aumentado;
- o plan original deixar de servir;
- a execução exigir decisão arquitetural não aprovada;
- o consumo de contexto começar a prejudicar precisão;
- a solução depender de adivinhação.

---

## Processo de recuperação

Quando houver suspeita de travamento, o sistema deve seguir este fluxo:

### 1. Parar mutação
Antes de continuar alterando arquivos, interromper mudança especulativa.

### 2. Reconstituir estado
Responder:
- o que foi tentado?
- o que funcionou?
- o que falhou?
- qual erro ou incerteza permanece?
- que arquivos foram tocados?

### 3. Separar fato de hipótese
Registrar:
- fatos confirmados;
- hipóteses ainda plausíveis;
- hipóteses descartadas;
- lacunas.

### 4. Reavaliar classe de risco
Verificar se a task continua no envelope original.

### 5. Escolher estratégia de recuperação
Possibilidades:
- voltar para discovery;
- reduzir escopo;
- isolar subproblema;
- criar Investigation Note;
- gerar Escalation Note;
- pedir decisão do Core Architect;
- encerrar com bloqueio documentado.

### 6. Retomar com novo plan ou escalar
Não retomar execução como se nada tivesse acontecido.

---

## Estratégias de recuperação

### Voltar para discovery
Use quando o problema parece mal compreendido.

### Reduzir escopo
Use quando a task ficou grande demais ou misturou problemas.

### Isolar subproblema
Use quando há muitos sintomas concorrentes.

### Reverter mudança especulativa
Use quando as alterações recentes não têm causalidade demonstrável.

### Gerar Investigation Note
Use quando a saída mais valiosa agora é conhecimento factual.

### Gerar Escalation Note
Use quando a decisão saiu do envelope do executor.

---

## Relação com context economy

Travamento costuma causar inflação de contexto.

Quando o contexto estiver grande demais, o sistema deve:
- compactar fatos;
- descartar ruído;
- preservar apenas estado atual, tentativas relevantes e próximas hipóteses;
- abrir nova sessão se necessário.

Não se recupera precisão acumulando transcript infinito.

---

## Relação com git e worktree

Quando o travamento envolver muitas mutações, o sistema deve considerar:

- inspecionar diff;
- separar mudanças boas de experimentos ruins;
- descartar alterações especulativas;
- mover experimento para worktree;
- preservar branch limpa para caminho estável.

---

## Relação com review

O reviewer deve desconfiar de entregas que vieram de período de travamento e depois “pareceram funcionar”.

Nesses casos, exigir:
- evidência mais clara;
- explicação do caminho final;
- declaração do que foi descartado;
- leitura de risco residual.

---

## O que evitar durante travamento

Evitar:

- insistir em comando aleatório;
- aumentar escopo;
- reescrever arquitetura;
- adicionar dependência nova sem causa;
- esconder falhas anteriores;
- transformar bug em refactor;
- produzir narrativa de sucesso sem resolver causa.

---

## Artifact esperado

Quando o travamento for relevante, a saída deve gerar um dos seguintes artifacts:

- Investigation Note;
- Escalation Note;
- Review Report;
- Completion Packet com lacunas explícitas.

O importante é não deixar o travamento sem memória.

---

## Declaração operacional curta

Quando o sistema para de convergir, ele deve parar de improvisar.  
Travamento exige diagnóstico, redução de ruído e nova estratégia.