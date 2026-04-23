# Política de Git

## Finalidade

Esta policy define como o harness deve se comportar diante de branches, worktrees, staging, commits e histórico local do repositório.

Seu papel é impedir:
- uso desorganizado do Git;
- histórico confuso;
- mistura de tasks;
- commits sem causalidade;
- operações destrutivas acima da autonomia legítima.

---

## Tese central

Git não é apenas ferramenta de versionamento.  
É parte da trilha factual da engenharia.

Por isso, o harness trata Git como:
- instrumento de isolamento;
- instrumento de revisão;
- instrumento de reversibilidade;
- e instrumento de clareza histórica.

---

## Regra operacional principal

Toda operação de Git feita pelo sistema deve melhorar, ou no mínimo preservar:
- a legibilidade do histórico;
- a separação entre tasks;
- a rastreabilidade da mudança;
- a revisão futura.

Se uma ação em Git piora essas quatro coisas, ela não está alinhada ao harness.

---

## Branches

### Regra geral
Toda task relevante que gera mutação real deve preferencialmente ter branch própria.

A branch deve refletir uma unidade coerente de trabalho, não múltiplas frentes misturadas.

### Branch não é obrigatória para toda microação
Mas é esperada quando:
- a task tem vida própria;
- haverá review;
- haverá continuidade;
- a mudança não é trivial;
- a unidade de trabalho precisa ser distinguível.

---

## Worktrees

Worktree é o mecanismo preferencial para paralelismo real.

Deve ser usado quando:
- há duas tasks relevantes em paralelo;
- existe experimento sem garantia de adoção;
- há risco de colisão entre mudanças;
- o operador quer preservar clareza entre trilhas.

Git e worktree devem andar juntos como políticas de isolamento.

---

## Staging

O staging deve refletir intenção.

O harness rejeita staging caótico em que:
- arquivos entram “porque estavam modificados”;
- mudanças parcialmente relacionadas são empilhadas;
- o que vai para o commit não corresponde à narrativa da task.

Antes de commitar, o sistema deve ser capaz de explicar:
- por que cada arquivo staged está ali;
- e por que ele pertence ao mesmo commit narrativo.

---

## Commits

### Regra geral
Commits devem representar unidades de mudança explicáveis.

O commit bom:
- tem causalidade;
- tem escopo identificável;
- conversa com a task;
- preserva review futuro;
- e não mistura assuntos.

### O que o executor não deve fazer por padrão
Sem autorização explícita, o executor não deve:
- sair produzindo vários commits locais arbitrariamente;
- reescrever histórico por conveniência;
- fazer operações agressivas de reset/rebase;
- decidir sozinho a estratégia final de granularidade do histórico.

### Papel do executor em relação a commit
Por padrão, o executor deve:
- preparar estado;
- sugerir mensagem de commit;
- organizar handoff;
- deixar o humano confortável para concluir o fechamento.

---

## Mensagem de commit

Mensagens devem ser:
- claras;
- curtas o suficiente para leitura rápida;
- específicas o suficiente para rastreabilidade.

A mensagem deve refletir a mudança real, não a intenção genérica do dia.

Exemplos bons:
- `fecha constitution inicial do harness`
- `adiciona bloco inicial de protocols do harness`

Exemplos ruins:
- `updates`
- `fixes`
- `refactor`
- `ajustes gerais`

---

## Operações sensíveis de Git

As operações abaixo exigem cautela reforçada e, em muitos casos, devem ficar fora da autonomia padrão:

- reset destrutivo;
- checkout que perde trabalho;
- rebase agressivo;
- squash ou rewrite de histórico sem alinhamento;
- force push;
- remoção de branch ainda relevante;
- resolução arriscada de conflito sem entendimento suficiente.

---

## Relação com classes de risco

### R0
Git pode ser lido, inspecionado e usado para contexto.

### R1
Mudanças pequenas podem gerar branch e staging simples.

### R2
Git já passa a fazer parte explícita do fluxo de task.

### R3
Paralelismo, conflito, refactor ou mudança estrutural pedem maior disciplina.

### R4
Operações sensíveis ficam fora da autonomia padrão.

---

## Relação com review

Histórico em Git deve facilitar review, não dificultá-lo.

Sinais de mau uso:
- branch contendo várias trilhas misturadas;
- diff impossível de narrar;
- commit message que não explica nada;
- staging desordenado;
- “limpezas” paralelas misturadas à solução principal.

---

## Papel do humano no fechamento

O fechamento sensível continua preferencialmente humano.

O harness prepara o terreno, mas a autoridade final para:
- commit final,
- push,
- merge,
- e promoção de branch

permanece sob controle humano, salvo exceção claramente autorizada.

---

## Declaração operacional curta

Git é parte da engenharia, não apêndice dela.  
O histórico deve contar a verdade da task com clareza, isolamento e reversibilidade.