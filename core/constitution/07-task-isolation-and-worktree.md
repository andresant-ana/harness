# Isolamento por Task e Política de Worktree

## Finalidade

Esta policy existe para garantir que o harness opere com isolamento suficiente entre frentes de trabalho, preservando clareza de contexto, rastreabilidade, review e reversibilidade.

Ela protege o sistema contra:

- sessões longas demais e contaminadas;
- mistura de múltiplas tasks no mesmo fluxo;
- paralelismo desorganizado;
- colisão entre mudanças concorrentes;
- review confuso;
- perda de causalidade entre decisão e execução.

---

## Tese central

Uma task deve ter identidade própria.

Isso significa que:
- cada task relevante deve possuir contexto operacional próprio;
- cada sessão deve ter escopo claro;
- paralelismo deve ser explícito;
- mudanças concorrentes não devem compartilhar o mesmo espaço de execução por conveniência.

A regra base da engenharia é:
**isolamento primeiro, paralelismo depois**.

---

## Unidade mínima de trabalho

No contexto do harness, uma task é uma unidade de trabalho que possui:

- objetivo claro;
- escopo delimitado;
- artefato de entrada ou contexto equivalente;
- plano ou investigação específica;
- evidência associada;
- handoff ou fechamento próprio.

Se não é possível dizer com clareza “qual é a task”, a sessão provavelmente está aberta demais.

---

## Regra de sessão

### Cada task relevante deve preferencialmente ter sua própria sessão
O sistema deve evitar:
- reaproveitar indefinidamente uma mesma conversa;
- misturar vários problemas na mesma thread;
- levar contexto histórico excessivo para dentro de nova execução.

### Sessão longa só é aceitável quando
- a continuidade factual ainda é útil;
- o escopo continua sendo o mesmo;
- a task ainda é essencialmente a mesma unidade de trabalho;
- não há contaminação relevante por frentes paralelas.

Quando isso deixar de ser verdade, a sessão deve ser encerrada e uma nova deve ser aberta.

---

## Sinais de contaminação de sessão

Uma sessão está contaminada quando:

- duas ou mais tasks diferentes estão sendo tratadas como uma só;
- o agente começa a trazer contexto histórico irrelevante;
- o review fica difícil porque não se sabe mais a cadeia causal da mudança;
- o objetivo original já foi resolvido ou mudou de natureza;
- a conversa está carregando muita informação que deveria ter virado artifact formal;
- o operador sente que o contexto está “pesado” e pouco preciso.

Quando esses sinais aparecerem, o comportamento correto é:
**abrir nova sessão e reinicializar o envelope**.

---

## Isolamento por branch e worktree

### Branch
Toda task relevante deve ter branch coerente com sua identidade.

A branch não precisa nascer para toda microinteração, mas deve existir sempre que:
- houver mudança real no código;
- a task tiver vida própria;
- o review e o histórico precisarem de separação clara.

### Worktree
Worktree é a ferramenta preferencial para paralelismo real no mesmo repositório.

Deve ser usado quando:
- duas tasks relevantes evoluem em paralelo;
- existe comparação entre abordagens;
- há risco de colisão entre mudanças concorrentes;
- um experimento não deve contaminar o workspace principal;
- o operador deseja revisão clara e separada por trilha.

---

## Quando worktree é recomendado

Use worktree quando houver qualquer uma destas condições:

1. duas frentes paralelas no mesmo repositório;
2. spike ou experimento com risco de abandono;
3. refactor relevante coexistindo com feature ou bugfix;
4. comparação entre duas soluções possíveis;
5. necessidade de manter uma linha “estável” e outra “experimental”.

---

## Quando worktree não é necessário

Não é obrigatório usar worktree quando:
- a mudança é pequena e única;
- não existe paralelismo real;
- o escopo está totalmente contido e linear;
- não há risco de colisão com outra frente.

A engenharia prefere worktree por necessidade, não por ritual.

---

## Regra de não mistura

Uma mesma worktree não deve carregar, por padrão:

- mais de uma task relevante não relacionada;
- mais de um experimento estrutural importante;
- mudança tática e refactor sistêmico misturados sem separação.

Se duas frentes já não conseguem ser explicadas por uma mesma narrativa curta, elas merecem separação.

---

## Relação com PROJECT_STATE e board

O isolamento da task não elimina o contexto do projeto.

A função dos artifacts é esta:
- o board registra estado de trabalho;
- o PROJECT_STATE registra estado técnico e operacional durável;
- a sessão da task registra o estado efêmero da execução.

Isso significa que o isolamento por task não causa perda de memória, desde que:
- os artifacts formais sejam mantidos;
- o PROJECT_STATE seja atualizado quando necessário;
- a task não dependa de transcript cru como memória principal.

---

## Regras para naming e disciplina

Toda task isolada deve, idealmente, permitir responder rapidamente:

- qual problema ela resolve;
- qual branch ou worktree corresponde a ela;
- qual packet ou plan a originou;
- qual artifact final a encerra.

Se essa identificação não for fácil, o isolamento está fraco.

---

## Relação com review

O review deve ocorrer sobre unidades de mudança compreensíveis.

Mudanças misturadas em excesso:
- aumentam risco de aprovação errada;
- dificultam regressão dirigida;
- tornam handoff ruim;
- escondem slop sob volume.

Por isso, o isolamento também é uma política de qualidade de review.

---

## Heurística de decisão rápida

### Abra nova sessão quando:
- o problema mudou;
- a tarefa mudou;
- o contexto anterior virou ruído;
- a execução entrou em trilha própria.

### Crie nova branch quando:
- houver mutação relevante;
- você precisar de histórico claro;
- a mudança merecer review separado.

### Use worktree quando:
- houver paralelismo real;
- houver experimento ou risco de colisão;
- o workspace principal não deve ser contaminado.

---

## Declaração operacional curta

Task relevante merece contexto próprio.  
Paralelismo real merece worktree.  
Sessão contaminada deve ser encerrada, não arrastada.