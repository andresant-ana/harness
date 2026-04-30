# Modelo de Maturidade do Harness

## Finalidade

Este documento define os níveis de maturidade aplicáveis às peças da engenharia de harness.

Seu papel é impedir que todo arquivo, skill, agent, policy, protocol, template, integração ou adapter seja tratado como igualmente confiável desde o primeiro momento.

Maturidade existe para diferenciar:
- ideia;
- rascunho;
- experimento;
- peça pronta para piloto;
- peça estável;
- peça obsoleta;
- peça removida.

---

## Tese central

Nem toda peça do harness nasce estável.

O harness deve evoluir por maturação controlada, não por acúmulo impulsivo.

Uma peça só deve ser considerada confiável quando:
- tem finalidade clara;
- tem fronteira definida;
- reduz entropia;
- foi usada ou revisada em contexto real;
- não duplica responsabilidade;
- respeita o núcleo canônico.

---

## Escala de maturidade

A escala oficial é:

```text
draft
↓
experimental
↓
pilot-ready
↓
stable
↓
deprecated
↓
removed
```

---

## `draft`

### Definição

Peça em rascunho inicial.

Pode existir para:
- registrar uma ideia;
- iniciar estrutura;
- explorar uma abordagem;
- preparar uma futura implementação.

### Características

- ainda pode mudar bastante;
- não deve ser tratada como fonte estável;
- pode conter lacunas;
- pode depender de revisão conceitual.

### Uso permitido

Pode ser lida e discutida, mas não deve ser aplicada como regra operacional forte.

### Critério para promoção

Promover para `experimental` quando:
- o objetivo estiver claro;
- a peça tiver escopo definido;
- houver razão concreta para testar seu uso.

---

## `experimental`

### Definição

Peça funcional em teste, mas ainda não validada em uso real suficiente.

### Características

- possui forma utilizável;
- pode ser aplicada em piloto limitado;
- exige observação;
- pode ser alterada ou removida sem grande custo.

### Uso permitido

Pode ser usada em contexto controlado, com rastreabilidade e cautela.

### Critério para promoção

Promover para `pilot-ready` quando:
- seu uso fizer sentido em fluxo real;
- os riscos forem compreendidos;
- a peça tiver output claro;
- houver sinais de que reduz erro, ambiguidade ou entropia.

---

## `pilot-ready`

### Definição

Peça pronta para ser usada no piloto controlado do harness.

### Características

- suficientemente clara;
- alinhada à constitution;
- compatível com protocols e policies;
- ainda sob observação;
- não considerada definitiva.

### Uso permitido

Pode ser aplicada em tasks reais de piloto.

### Critério para promoção

Promover para `stable` quando:
- funcionar em mais de um cenário;
- não gerar fricção desproporcional;
- melhorar comportamento observável;
- não introduzir duplicidade ou contradição;
- passar por revisão pós-piloto.

---

## `stable`

### Definição

Peça considerada parte madura do harness.

### Características

- comportamento compreendido;
- utilidade validada;
- fronteira clara;
- baixa chance de remoção imediata;
- apta a orientar runtime, skills, agents e templates.

### Uso permitido

Pode ser tratada como fonte oficial do harness.

### Critério de manutenção

Peças estáveis ainda devem ser revisadas quando:
- houver mudança de runtime;
- houver falha recorrente;
- houver drift conceitual;
- houver sobreposição com outra peça;
- o piloto revelar custo maior que benefício.

---

## `deprecated`

### Definição

Peça ainda presente, mas não recomendada para novos usos.

### Características

- foi substituída;
- perdeu utilidade;
- ficou redundante;
- cria risco de confusão;
- será removida ou incorporada em outra peça futuramente.

### Uso permitido

Pode ser lida para histórico, mas não deve orientar novas implementações.

### Critério para remoção

Remover quando:
- não houver dependência ativa;
- substituição estiver clara;
- changelog registrar a mudança;
- documentação afetada for atualizada.

---

## `removed`

### Definição

Peça removida do harness.

### Características

- não faz mais parte do sistema;
- deve ter histórico no changelog quando relevante;
- pode ser mencionada apenas em contexto de depreciação ou migração.

---

## Aplicação por tipo de peça

### Protocols

Protocol deve virar `stable` apenas quando seu fluxo for usado em tasks reais sem gerar burocracia desnecessária.

### Policies

Policy deve virar `stable` quando seus limites forem claros e não contradisserem outras policies.

### Artifacts

Artifact deve virar `stable` quando seu schema for útil, preenchível e suficiente para preservar continuidade.

### Skills

Skill deve começar como `experimental` e só virar `stable` após provar que reduz erro recorrente.

### Agents

Agent deve virar `stable` quando seu papel for distinto, necessário e não sobreposto.

### Templates

Template deve virar `stable` quando funcionar em pelo menos um workspace real sem exigir retrabalho estrutural grande.

### Integrations

Integração deve seguir também a trusted integrations policy.

### Adapter

Adapter deve amadurecer depois do núcleo, pois traduz a engenharia para runtime concreto.

---

## Critérios gerais de promoção

Antes de promover qualquer peça, responder:

1. esta peça tem função clara?
2. ela reduz risco, ambiguidade ou entropia?
3. ela não duplica outra peça?
4. ela foi testada ou revisada em contexto adequado?
5. ela tem limites?
6. ela respeita o núcleo canônico?
7. ela melhora comportamento real?

---

## Critérios gerais de rebaixamento

Rebaixar ou marcar como deprecated quando:

- a peça gera fricção sem valor;
- duplica outra responsabilidade;
- ficou desatualizada;
- contradiz protocol ou policy estável;
- induz uso errado;
- aumenta contexto sem melhorar output;
- virou ritual.

---

## Registro de maturidade

Quando necessário, a maturidade de uma peça deve ser registrada em:

- changelog;
- experimental registry;
- release notes;
- backlog pós-piloto;
- ou cabeçalho do próprio documento, quando útil.

---

## Relação com piloto

Durante o piloto, muitas peças podem estar em `pilot-ready`.

A promoção para `stable` deve acontecer apenas depois de observar comportamento real.

---

## Declaração operacional curta

Maturidade é confiança conquistada.  
O harness não trata rascunho como lei, nem experimento como fundamento estável.