# Registro Experimental

## Finalidade

Este documento registra peças experimentais do harness.

Seu papel é manter visíveis ideias, fluxos, skills, commands, plugins, integrations, adapter changes ou policies que ainda não devem ser tratadas como estáveis.

Experimento sem registro vira comportamento informal.  
Comportamento informal vira entropia.

---

## Tese central

Experimentar é permitido.  
Confundir experimento com fundamento não é.

Toda peça experimental deve ter:
- objetivo;
- escopo;
- risco;
- critério de sucesso;
- critério de abandono;
- dono ou contexto de avaliação;
- status.

---

## Quando registrar um experimento

Registrar quando uma peça nova ainda não validada for introduzida ou proposta, como:

- skill nova;
- agent novo;
- command novo;
- plugin;
- MCP integration;
- automation;
- template alternativo;
- policy candidate;
- protocol candidate;
- mudança no adapter;
- fluxo de review alternativo;
- eval/replay scenario novo.

---

## O que não precisa registrar

Não precisa registrar:

- correção editorial simples;
- ajuste de wording;
- renomeação sem impacto comportamental;
- arquivo draft que ainda não será testado;
- anotação pessoal fora do harness.

---

## Campos obrigatórios de experimento

Cada experimento deve registrar:

1. nome;
2. tipo;
3. objetivo;
4. hipótese;
5. escopo;
6. risco;
7. status;
8. critério de sucesso;
9. critério de abandono;
10. próxima revisão.

---

## Status possíveis

### `proposed`

Experimento proposto, ainda não executado.

### `active`

Experimento em teste.

### `paused`

Experimento pausado por falta de contexto, prioridade ou evidência.

### `promoted`

Experimento promovido para peça oficial.

### `rejected`

Experimento rejeitado.

### `deprecated`

Experimento que virou peça, mas depois foi depreciado.

---

## Template de registro

```md
## <nome do experimento>

### Tipo
<skill | agent | command | plugin | integration | template | protocol | policy | adapter | eval | outro>

### Status
<proposed | active | paused | promoted | rejected | deprecated>

### Objetivo
<o que este experimento tenta melhorar>

### Hipótese
<qual melhoria comportamental esperamos observar>

### Escopo
<onde será testado e onde não deve ser usado>

### Risco
<risco de contexto, segurança, entropia, acoplamento ou operação>

### Critério de sucesso
<como saberemos que funcionou>

### Critério de abandono
<quando removeremos ou rejeitaremos>

### Evidência esperada
<qual dado, replay, eval ou feedback deve sustentar decisão>

### Próxima revisão
<data, milestone ou condição>

### Observações
<notas adicionais>
```

---

## Experimentos iniciais

Nenhum experimento ativo registrado no momento.

Este arquivo deve permanecer vazio de experimentos até que uma peça seja explicitamente colocada em teste.

---

## Exemplos de bons experimentos futuros

### Skill nova de performance
Pode ser experimental se houver dúvida se reduz erro real ou só adiciona checklist desnecessário.

### Command de handoff
Pode ser experimental se ainda não sabemos se melhora fechamento ou cria ritual.

### MCP read-only de GitHub Projects
Pode ser experimental antes de virar trusted integration.

### Replay suite
Pode começar experimental até provar utilidade no piloto.

---

## Critérios para promover experimento

Promover quando:

- foi usado em cenário real ou replay relevante;
- reduziu erro ou ambiguidade;
- não aumentou entropia líquida;
- teve output útil;
- respeitou policies;
- não duplicou outra peça;
- sua manutenção parece aceitável.

---

## Critérios para rejeitar experimento

Rejeitar quando:

- não foi usado;
- gera ruído;
- aumenta contexto sem ganho;
- cria acoplamento ruim;
- é perigoso demais;
- duplica capacidade existente;
- resolve problema raro demais;
- não tem critério de sucesso observável.

---

## Relação com changelog

Promoção, rejeição ou remoção de experimento relevante deve ser registrada no changelog.

---

## Relação com backlog

Experimento pausado que ainda tem valor pode ser movido para backlog pós-piloto.

---

## Declaração operacional curta

Experimentos são bem-vindos quando têm fronteira.  
Sem registro, experimento vira regra invisível.