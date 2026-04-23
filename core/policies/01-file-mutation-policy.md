# Política de Mutação de Arquivos

## Finalidade

Esta policy define como o harness deve escrever, editar, criar, mover ou remover arquivos dentro do repositório e, quando permitido, em superfícies adjacentes ao projeto.

Seu papel é impedir:
- mutação excessiva;
- diffs desproporcionais;
- alteração fora do escopo;
- geração de arquivos desnecessários;
- mudanças que pioram navegabilidade e entropia.

---

## Tese central

Arquivo não deve ser alterado porque “está perto”.  
Arquivo só deve ser alterado quando a causalidade da task realmente o exigir.

A mutação correta é:
- mínima;
- deliberada;
- justificada;
- reversível quando possível;
- e coerente com a verdade local do projeto.

---

## Regra operacional principal

Toda mutação de arquivo deve responder:

1. por que este arquivo precisa ser tocado;
2. qual parte do escopo exige isso;
3. se a mudança respeita convenção local;
4. se existe modo mais simples de resolver sem ampliar superfície;
5. se a alteração aumenta ou reduz entropia.

Se o arquivo não consegue ser ligado claramente ao problema, ele não deveria estar no diff.

---

## Princípio do menor diff suficiente

O harness deve preferir o menor conjunto de mudanças capaz de resolver o problema corretamente.

Isso não significa fazer gambiarra ou evitar refactor necessário.  
Significa evitar:
- tocar arquivos por proximidade casual;
- refatorar lateralmente sem necessidade;
- “aproveitar o embalo” para reescrever áreas não aprovadas;
- espalhar uma task simples em muitos lugares.

---

## Tipos de mutação

### 1. Mutação local direta
Alteração em arquivo ou conjunto pequeno de arquivos claramente ligados à task.

É o padrão preferencial quando:
- a causalidade é curta;
- o risco é controlado;
- o escopo está claro.

### 2. Mutação estrutural controlada
Alteração em múltiplos arquivos por necessidade arquitetural, refactor legítimo ou propagação de mudança coerente.

Só deve ocorrer quando:
- o plan justificar;
- o escopo exigir;
- a complexidade for proporcional.

### 3. Mutação em massa
Alteração em muitos arquivos por geração, migração, padronização ou mudança transversal.

Deve ser tratada com alta cautela porque:
- dificulta review;
- mascara slop;
- amplia blast radius;
- e tende a exigir justificação mais forte.

---

## Regra de não expansão silenciosa

O executor não deve tocar arquivos adicionais apenas porque:
- percebeu “oportunidade de melhoria”;
- encontrou código feio ao lado;
- achou uma abstração “mais elegante”;
- deseja deixar tudo “mais limpo”.

Se a melhoria não pertence à causalidade da task, ela:
- vira outra task;
- ou precisa de aprovação explícita.

---

## Criação de arquivos novos

Criar arquivo novo é legítimo quando:
- a tarefa exige artifact novo;
- a convenção local pede isso;
- a separação melhora clareza real;
- a criação reduz acoplamento de forma proporcional;
- o arquivo tem identidade funcional clara.

Não é legítimo criar arquivo novo só para:
- inflar cerimônia;
- reproduzir padrão sem dor real;
- separar por estética;
- antecipar abstração.

---

## Remoção de arquivos

Arquivo só deve ser removido quando:
- a remoção é parte explícita da solução;
- o arquivo ficou obsoleto de fato;
- a causalidade é clara;
- não há dependência oculta não verificada.

Remoção é particularmente sensível porque pode parecer “limpeza” e ser, na prática, regressão silenciosa.

---

## Renomeação e movimentação

Mover ou renomear arquivo só é aceitável quando:
- a convenção local realmente exige;
- a mudança reduz confusão real;
- a causalidade da task pede isso;
- o custo de review continua aceitável.

Renomeação ampla por capricho editorial é anti-pattern dentro da execução de task.

---

## Relação com arquitetura por dor real

Mutação de arquivo deve respeitar a doutrina anti-cerimônia.

Sinais de mutação ruim:
- feature pequena tocando muitos arquivos sem ganho claro;
- geração de camadas, DTOs, mappers e interfaces sem dor real;
- separação ritualística;
- novos diretórios ou wrappers que só aumentam navegação.

---

## Relação com PROJECT_STATE e documentação local

Quando a mutação altera a realidade durável do projeto, a política exige considerar atualização de:

- `PROJECT_STATE.md`
- documentação local relevante
- authority sources impactadas

Mas isso não significa atualizar documentação a cada linha alterada.  
A regra é: atualizar quando a verdade do projeto mudou.

---

## Relação com review

O reviewer deve desconfiar de diffs em que:
- a área tocada é maior do que o problema;
- há arquivos sem causalidade clara;
- a mudança parece “feature + limpeza + refactor + reorganização” ao mesmo tempo;
- a mutação aumentou entropia estrutural;
- o executor parece ter seguido estética em vez de necessidade.

---

## Relação com classes de risco

### R0
Sem mutação.

### R1
Mutação pequena e local é o padrão.

### R2
Mutação deve seguir Execution Plan com razoável fidelidade.

### R3
Mutação estrutural exige cautela, justificativa e escalonamento.

### R4
Mutação sensível ou irreversível está fora da autonomia padrão.

---

## Regra de visibilidade

Toda mutação relevante deve deixar o sistema capaz de responder:
- quais arquivos foram tocados;
- por que foram tocados;
- o que mudaram;
- por que o diff não ficou menor.

Se isso não estiver claro, o diff perdeu qualidade explicativa.

---

## Declaração operacional curta

Arquivo só entra no diff quando o problema puxa ele para dentro.  
O harness muta com causalidade, não por conveniência, estética ou entusiasmo.