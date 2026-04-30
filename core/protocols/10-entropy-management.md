# Protocolo de Controle de Entropia

## Finalidade

Este protocolo define como o harness deve detectar, prevenir e reduzir entropia técnica, arquitetural, documental e operacional.

Seu papel é impedir que o uso de agentes produza degradação gradual do sistema por acúmulo de pequenas decisões aparentemente inofensivas.

---

## Tese central

Slop não é apenas código feio.  
Slop é perda progressiva de coerência.

A entropia aparece quando o sistema acumula:
- duplicação;
- abstração sem dor real;
- convenções quebradas;
- nomenclatura inconsistente;
- arquivos sem causalidade;
- documentação vencida;
- dependências desnecessárias;
- boundaries contaminados;
- artifacts que não refletem a realidade.

O harness deve agir contra essa degradação.

---

## Tipos de entropia

### 1. Entropia de código
Inclui:
- duplicação desnecessária;
- funções redundantes;
- helpers genéricos demais;
- lógica espalhada;
- tratamento inconsistente de erros;
- acoplamento acidental.

### 2. Entropia arquitetural
Inclui:
- boundaries quebrados;
- módulos se conhecendo demais;
- camadas adicionadas sem dor real;
- padrões aplicados por cerimônia;
- abstrações que escondem causalidade.

### 3. Entropia documental
Inclui:
- documentação desatualizada;
- `PROJECT_STATE.md` divergente;
- authority source imprecisa;
- README que não reflete comandos reais;
- decisões importantes não registradas.

### 4. Entropia operacional
Inclui:
- comandos locais confusos;
- validação não padronizada;
- observabilidade inconsistente;
- health checks frágeis;
- dependências operacionais implícitas.

### 5. Entropia de agente
Inclui:
- prompts contraditórios;
- rules espalhadas;
- skill bloat;
- agents com papéis sobrepostos;
- adapter redefinindo doutrina do núcleo.

---

## Sinais de slop

O sistema deve tratar como sinal de alerta:

- feature simples tocando muitos arquivos sem ganho;
- criação de interface sem variação real;
- DTO, mapper ou camada sem dor concreta;
- duplicação de padrão já existente;
- nomes diferentes para a mesma ideia;
- arquivo novo com responsabilidade vaga;
- documentação local que contradiz código;
- mudança que “funciona”, mas piora navegação.

---

## Regra operacional principal

Toda task relevante deve considerar se aumenta, reduz ou preserva a entropia do sistema.

A pergunta mínima é:
- esta mudança deixa o sistema mais claro ou mais confuso?

Se a mudança aumenta complexidade, deve explicar:
- que dor resolve;
- que risco reduz;
- que custo introduz;
- e por que o custo é aceitável.

---

## Entropia e arquitetura por dor real

Este protocolo opera em conjunto com `06-architecture-by-pain.md`.

A lógica é:

- dor real pode justificar complexidade;
- complexidade sem dor real aumenta entropia;
- abstração prematura é dívida;
- simplicidade sem responsabilidade também pode ser dívida.

O objetivo não é sempre simplificar.  
O objetivo é manter complexidade proporcional.

---

## Entropia e review

O review deve verificar:

- se o diff ficou maior do que o problema;
- se há arquivos sem causalidade clara;
- se a mudança criou convenção paralela;
- se houve abstração preventiva;
- se a solução duplicou algo já existente;
- se documentação durável precisa ser atualizada;
- se a entrega piorou a navegabilidade para humanos e agentes.

---

## Entropia e handoff

Quando a task introduzir risco de entropia, o handoff deve registrar:

- que complexidade foi adicionada;
- por que ela foi necessária;
- que risco ela reduz;
- que custo ela cria;
- se há follow-up de limpeza ou documentação.

---

## Entropia e PROJECT_STATE

Quando uma mudança altera a coerência durável do projeto, o estado deve ser atualizado.

Isso inclui:
- nova limitação conhecida;
- decisão de arquitetura;
- dívida técnica consciente;
- risco em observação;
- boundary alterado;
- comando ou validação modificados.

Sem state update, a entropia documental cresce.

---

## Heurísticas anti-slop

Antes de aceitar uma mudança, perguntar:

1. isso resolve o problema ou embeleza em volta?
2. isso criou camada sem dor?
3. isso espalhou uma feature local por arquivos demais?
4. isso duplicou conceito existente?
5. isso seguiu convenção local?
6. isso tornou a próxima task mais fácil ou mais difícil?
7. isso será compreensível em um mês?
8. isso ajuda o agente futuro ou confunde o agente futuro?

---

## Ações de controle

Quando entropia for detectada, o sistema pode:

- bloquear a mudança;
- pedir reavaliação;
- reduzir escopo;
- remover abstração;
- consolidar duplicação;
- atualizar documentação;
- criar follow-up;
- registrar dívida consciente;
- escalar para Core Architect.

---

## O que evitar

Evitar:

- refactor cosmético dentro de feature;
- limpeza lateral sem escopo;
- abstração por estética;
- documentação ornamental;
- skill ou policy nova para problema não recorrente;
- resolver entropia criando mais entropia.

---

## Relação com skills

Quando necessário, o sistema pode acionar:

- `architecture-drift-auditor`;
- `consistency-scanner`;
- `dependency-hygiene-review`;
- `doc-gardener`;
- `project-state-maintainer`;
- `architecture-by-pain-check`.

---

## Declaração operacional curta

Entropia é degradação silenciosa.  
O harness deve preservar clareza, causalidade e proporção em cada task.