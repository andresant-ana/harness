# Skill — Refactoring Safety

## Finalidade

Esta skill orienta refactors seguros, proporcionais e rastreáveis.

Seu papel é impedir que o agente transforme uma task funcional em reescrita ampla, misture limpeza com feature, ou altere estrutura sem evidência de necessidade.

Refactor bom reduz risco ou entropia.  
Refactor ruim espalha mudança e dificulta review.

---

## Quando usar

Use esta skill quando:

- a task exigir refactor;
- o agente sugerir reorganização de código;
- houver duplicação real;
- houver mudança estrutural localizada;
- uma feature exigir ajuste interno antes da implementação;
- o diff começar a crescer;
- houver risco de mudança lateral;
- review apontar entropia ou drift.

---

## Quando não usar

Não use esta skill quando:

- a mudança for puramente aditiva e simples;
- o refactor for cosmético;
- a task não autorizar reorganização;
- o refactor for só preferência estética;
- a alteração ampla deveria ser outra task.

---

## Tese central

Refactor precisa ter causalidade.

A pergunta não é:

“este código poderia ser mais bonito?”

A pergunta é:

“este refactor é necessário para resolver a task, reduzir risco real ou controlar entropia?”

---

## Tipos de refactor

### 1. Refactor preparatório local

Pequena reorganização necessária para implementar a task com segurança.

Aceitável quando:
- é local;
- tem causalidade;
- reduz duplicação ou confusão imediata;
- não muda comportamento esperado.

### 2. Refactor corretivo

Corrige estrutura que já está causando problema.

Aceitável quando:
- há dor real;
- há evidência;
- há validação.

### 3. Refactor de hygiene

Reduz entropia documentada.

Aceitável quando:
- tem escopo próprio;
- não se mistura com feature;
- melhora clareza mensurável.

### 4. Refactor especulativo

Reorganiza pensando em necessidade futura.

Deve ser rejeitado ou escalado.

---

## Método

### 1. Declarar motivo

Todo refactor deve responder:

- por que isso é necessário?
- que dor resolve?
- o que acontece se não fizer?
- pertence à task atual?

---

### 2. Delimitar escopo

Definir:

- arquivos envolvidos;
- comportamento que não deve mudar;
- partes fora de escopo;
- validação esperada.

---

### 3. Separar feature de refactor

Se a feature e o refactor forem ambos relevantes, considerar:

- primeiro refactor pequeno, depois feature;
- ou feature primeiro, refactor em follow-up;
- ou Escalation Note se o refactor for estrutural.

Não misturar mudanças demais no mesmo diff.

---

### 4. Preservar comportamento

Refactor deve preservar comportamento, salvo quando a mudança de comportamento for explícita.

Se comportamento mudar, não é refactor puro.

---

### 5. Validar proporcionalmente

Usar:

- testes existentes;
- build;
- lint/typecheck;
- diff review;
- validação funcional;
- review se R2+.

---

### 6. Registrar risco residual

Se não houver teste suficiente, declarar lacuna.

---

## Output esperado

```md
# Refactoring Safety Note

## Motivo do refactor
<dor real ou necessidade>

## Tipo de refactor
<preparatório local | corretivo | hygiene | outro>

## Escopo
- <arquivo/área 1>
- <arquivo/área 2>

## Fora de escopo
- <item 1>
- <item 2>

## Comportamento esperado
<deve permanecer igual | muda explicitamente em X>

## Validação prevista
- <validação 1>
- <validação 2>

## Riscos
- <risco 1>
- <risco 2>

## Veredito
<seguir | reduzir escopo | separar task | escalar>
```

---

## Checklist de segurança

Antes de aceitar refactor, verificar:

- há dor real?
- o escopo está claro?
- o comportamento deve permanecer?
- a feature está separada da limpeza?
- o diff é revisável?
- há validação suficiente?
- o refactor não cria abstração prematura?
- o Core Architect precisa revisar?

---

## Critérios de escalonamento

Escalar quando:

- o refactor alterar boundary;
- tocar muitos módulos;
- mudar arquitetura;
- exigir nova abstração importante;
- alterar comportamento junto;
- não houver teste suficiente para risco alto;
- a task original não autorizava esse escopo;
- houver risco de quebrar produção.

---

## Anti-patterns

Evitar:

- “já que estou aqui”;
- refactor cosmético dentro de feature;
- reescrever arquivo inteiro sem necessidade;
- mudar nomes em massa sem valor;
- introduzir padrão novo durante bugfix;
- esconder mudança de comportamento como refactor;
- usar refactor para escapar de bug mal entendido;
- criar muitos arquivos para parecer limpo.

---

## Declaração operacional curta

Refactor seguro tem motivo, escopo e validação.  
Sem causalidade, refactor vira entropia.