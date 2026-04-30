# Política de Depreciação

## Finalidade

Este documento define como descontinuar, substituir, fundir ou remover peças do harness sem gerar perda de coerência.

Seu papel é impedir que a engenharia acumule arquivos, skills, agents, templates, policies, protocols ou integrações que já não reduzem risco, ambiguidade ou entropia.

Depreciação existe porque uma engenharia boa também sabe remover.

---

## Tese central

Tudo que entra no harness precisa poder sair.

Sem política de depreciação, o sistema tende a acumular:
- regras obsoletas;
- skills redundantes;
- agents sobrepostos;
- templates fracos;
- integrações sem uso;
- adapters confusos;
- documentos que ninguém deveria mais seguir.

A engenharia deve preservar o que funciona e remover o que degrada clareza.

---

## Quando deprecar

Uma peça deve ser considerada para depreciação quando:

- perdeu utilidade;
- foi substituída por solução melhor;
- duplica outra peça;
- causa confusão;
- aumenta contexto sem melhorar output;
- contradiz outra peça mais madura;
- induz comportamento ruim;
- virou ritual;
- não é usada no piloto;
- gera mais manutenção do que valor.

---

## O que pode ser depreciado

Podem ser depreciados:

- protocols;
- policies;
- artifacts;
- taxonomy entries;
- observability models;
- governance docs;
- skills;
- agents;
- templates;
- adapter files;
- commands;
- plugins;
- integrações;
- checklists.

---

## Estados de depreciação

### `active`

Peça em uso normal.

### `deprecated`

Peça ainda presente, mas não recomendada para novos usos.

### `replaced`

Peça substituída por outra.

### `merged`

Peça incorporada a outra peça.

### `removed`

Peça removida do repositório.

---

## Processo de depreciação

### 1. Identificar problema

Registrar por que a peça está sendo considerada para depreciação.

Motivos possíveis:
- redundância;
- baixa utilidade;
- contradição;
- custo de contexto;
- falha no piloto;
- melhor alternativa.

### 2. Verificar dependências

Antes de remover, entender se a peça é referenciada por:

- README;
- roadmap;
- protocols;
- policies;
- artifacts;
- taxonomy;
- skills;
- agents;
- templates;
- adapter;
- documentação externa.

### 3. Definir caminho

Escolher uma ação:

- manter;
- revisar;
- fundir;
- substituir;
- marcar como deprecated;
- remover.

### 4. Atualizar referências

Se houver substituição, atualizar documentos que apontam para a peça antiga.

### 5. Registrar no changelog

Mudanças estruturais devem aparecer no `CHANGELOG_HARNESS.md`.

### 6. Remover apenas quando seguro

Só remover quando não houver dependência ativa ou quando a migração estiver clara.

---

## Critérios para remover imediatamente

Remoção direta pode ser aceitável quando:

- a peça ainda está em draft;
- nunca foi usada;
- não é referenciada;
- é claramente erro estrutural;
- foi criada por engano;
- sua presença gera confusão.

Mesmo assim, registrar se a remoção for relevante.

---

## Critérios para manter deprecated temporariamente

Manter como deprecated quando:

- ainda há referência ativa;
- usuários ou agentes podem depender dela;
- a substituição precisa ser explicada;
- a remoção imediata quebraria entendimento;
- a peça tem valor histórico temporário.

---

## Como marcar depreciação

Uma peça deprecated deve conter aviso no topo:

```md
> Status: Deprecated
> Substituído por: <arquivo ou peça>
> Motivo: <motivo curto>
> Não usar para novas implementações.
```

---

## Depreciação de skills

Skill deve ser depreciada quando:

- não tem gatilho claro;
- duplica outra skill;
- é muito teórica;
- não produz output útil;
- nunca é chamada em tasks reais;
- aumenta contexto sem reduzir erro.

Ao deprecar skill, indicar:
- skill substituta;
- motivo;
- data;
- impacto esperado.

---

## Depreciação de agents

Agent deve ser depreciado quando:

- seu papel se sobrepõe a outro;
- sua função é melhor resolvida por skill;
- cria confusão no fluxo;
- não produz artifact distinto;
- incentiva violação da fronteira humano/Core Architect/executor.

---

## Depreciação de templates

Template deve ser depreciado quando:

- não é usado;
- produz ruído;
- duplica outro template;
- não ajuda bootstrap;
- não se adapta bem a projetos reais.

---

## Depreciação de integrations

Integração deve ser depreciada quando:

- perdeu confiança;
- ampliou risco;
- deixou de ser necessária;
- mudou permissões;
- passou a produzir outputs pouco confiáveis;
- não respeita mais trusted integrations policy.

---

## Depreciação de adapter

Peças do adapter devem ser depreciadas quando:

- contradizem o núcleo;
- dependem de comportamento antigo do runtime;
- duplicam regra canônica;
- ficaram incompatíveis com o OpenCode;
- reduzem portabilidade.

---

## Relação com maturity model

Depreciação é parte do ciclo de maturidade:

```text
stable → deprecated → removed
experimental → removed
pilot-ready → deprecated | stable
```

Nem toda peça precisa passar por todos os estados.

---

## Relação com backlog

Quando a peça não deve ser removida agora, mas precisa ser revista, registrar no backlog pós-piloto.

---

## Sinais de ausência de depreciação

O harness está sem higiene de depreciação quando:

- arquivos antigos continuam sendo citados;
- skills inúteis se acumulam;
- agents têm papéis confusos;
- templates duplicam estrutura;
- policies entram em conflito;
- ninguém sabe se uma peça ainda vale.

---

## Declaração operacional curta

Depreciação é higiene da engenharia.  
O harness deve crescer, mas também deve podar.