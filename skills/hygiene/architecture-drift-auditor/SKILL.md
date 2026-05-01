# Skill — Architecture Drift Auditor

## Finalidade

Esta skill orienta a detecção de drift arquitetural: quando o código, os módulos, os boundaries, as dependências ou os fluxos começam a divergir da arquitetura pretendida ou documentada.

Seu papel é impedir que pequenas mudanças locais, feitas sem intenção ruim, degradem gradualmente a coerência estrutural do projeto.

---

## Quando usar

Use esta skill quando houver risco de:

- módulo importando outro módulo indevidamente;
- boundary de domínio sendo quebrado;
- lógica de negócio vazando para camada errada;
- duplicação de regra entre contextos;
- dependência circular;
- feature simples espalhada por arquivos demais;
- arquitetura documentada divergindo do código;
- padrão local sendo ignorado;
- refactor introduzindo estrutura paralela;
- agente seguindo heurística genérica em vez de convenção local.

---

## Quando não usar

Não use esta skill quando:

- a task for puramente local e sem impacto estrutural;
- não houver módulos, boundaries ou arquitetura relevante envolvidos;
- a checagem viraria revisão abstrata sem objeto concreto;
- o problema já estiver coberto por review arquitetural mais específico.

---

## Tese central

Drift arquitetural raramente nasce de uma grande decisão errada.

Ele nasce de pequenas exceções:

- import temporário;
- helper duplicado;
- regra copiada;
- abstração criada fora do padrão;
- dependência adicionada “só desta vez”;
- documentação que deixou de refletir o código.

O auditor deve detectar cedo, antes que o desvio vire novo normal.

---

## Método

### 1. Identificar arquitetura esperada

Localizar fontes de verdade:

- `PROJECT_STATE.md`;
- `WORKSPACE_GUIDE.md`;
- ADRs;
- README;
- estrutura de módulos;
- convenções locais;
- boundaries documentados;
- imports existentes;
- padrões de teste.

Não auditar drift sem saber qual era a intenção arquitetural.

---

### 2. Identificar mudança ou área analisada

Mapear:

- arquivos tocados;
- módulos afetados;
- dependências novas;
- imports novos;
- responsabilidades movidas;
- regras duplicadas;
- documentação impactada.

---

### 3. Comparar intenção e realidade

Perguntar:

- esta mudança respeita o boundary local?
- algum módulo passou a conhecer detalhe que não deveria?
- regra de domínio foi duplicada?
- infra vazou para domínio?
- UI passou a carregar regra que deveria estar no backend?
- a arquitetura documentada ainda descreve o código?

---

### 4. Detectar sinais de drift

Sinais comuns:

- import cruzado indevido;
- lógica em pasta errada;
- DTO usado como entidade de domínio;
- camada acessando banco diretamente fora do padrão;
- regra duplicada em frontend/backend sem contrato claro;
- módulo novo sem fronteira;
- dependência criada para contornar boundary;
- nomenclatura divergente.

---

### 5. Classificar severidade

Classificar drift como:

- leve: inconsistência pequena, corrigível localmente;
- moderado: pode confundir futuras tasks;
- alto: quebra boundary ou cria precedente estrutural;
- crítico: contradiz decisão arquitetural ou risco de produção/segurança.

---

### 6. Recomendar ação

Ações possíveis:

- aceitar com ressalva;
- corrigir no mesmo diff;
- criar follow-up;
- atualizar documentação;
- propor ADR;
- escalar ao Core Architect;
- bloquear mudança.

---

## Output esperado

```md
# Architecture Drift Audit

## Área analisada
<módulo, fluxo, diff ou diretório>

## Arquitetura esperada
<fonte local de verdade e intenção arquitetural>

## Sinais de drift encontrados
- <sinal 1>
- <sinal 2>

## Severidade
<leve | moderada | alta | crítica>

## Impacto
<como isso afeta manutenção, contexto, boundary ou evolução>

## Ação recomendada
<aceitar | corrigir | documentar | criar follow-up | escalar | bloquear>

## Risco residual
<risco que permanece>
```

---

## Checklist de qualidade

Antes de concluir, verificar:

- a arquitetura esperada foi localizada?
- o diff respeita boundaries?
- há imports indevidos?
- há dependência circular?
- há regra duplicada?
- a documentação segue verdadeira?
- a mudança cria precedente perigoso?
- a severidade foi proporcional?
- a recomendação é acionável?

---

## Critérios de escalonamento

Escalar quando:

- o drift quebra boundary de domínio;
- há conflito com ADR;
- a correção exige refactor amplo;
- a mudança cria dependência estrutural nova;
- a arquitetura documentada parece errada ou obsoleta;
- há trade-off entre preservar arquitetura e entregar feature;
- o drift pode afetar segurança, dados ou operação.

---

## Anti-patterns

Evitar:

- chamar toda diferença de drift;
- bloquear mudança pequena por purismo;
- ignorar boundary por conveniência;
- corrigir drift com refactor gigante não aprovado;
- atualizar documentação para justificar arquitetura ruim;
- tratar padrão genérico da internet como autoridade local;
- aceitar “só desta vez” sem registrar risco.

---

## Declaração operacional curta

Drift arquitetural é perda silenciosa de coerência.  
O harness deve detectar cedo, corrigir proporcionalmente e escalar quando o boundary estiver em jogo.