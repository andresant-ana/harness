# Taxonomia de Skills

## Finalidade

Este documento classifica as famílias de skills do harness, explicando o papel de cada família, quando usar skills, quando não usar e como evitar skill bloat.

A taxonomia não substitui os arquivos `SKILL.md`.  
Ela define o mapa geral das capacidades acionáveis.

---

## Tese central

Skill é método acionável sob demanda.

Uma skill não é artigo, aula, manifesto ou memória genérica.  
Ela existe para ajudar o agente a executar melhor uma classe recorrente de trabalho.

Uma boa skill contém:
- finalidade;
- gatilhos de uso;
- passos recomendados;
- checklist;
- anti-patterns;
- outputs esperados;
- limites.

---

## Regras gerais

### Quando usar uma skill

Usar skill quando a task exigir:
- método recorrente;
- checklist especializado;
- revisão de risco;
- análise técnica específica;
- output formal;
- redução de erro comum.

### Quando não usar uma skill

Não usar skill quando:
- a task é simples;
- o método não é recorrente;
- a skill seria só teoria;
- a skill aumentaria contexto sem ação;
- o problema pertence ao Core Architect ou humano.

### Skill não deve substituir judgment

Skill orienta execução.  
Não decide sozinha.

Se a skill revelar trade-off estrutural, risco alto ou ambiguidade, o sistema deve escalar.

---

## Estrutura geral

```text
skills/
├─ orchestration/
├─ engineering/
├─ stack/
├─ platform/
├─ integration/
├─ security/
└─ hygiene/
```

---

## `skills/orchestration/`

### Função

Skills de orchestration regulam o fluxo da task, planejamento, risco, decomposição, validação e encerramento.

```text
skills/orchestration/
├─ implementation-planner/
├─ risk-classifier/
├─ task-decomposer/
├─ testing-verifier/
├─ delivery-wrapup/
└─ stuck-recovery-playbook/
```

### Quando usar

Usar quando:
- a task precisa ser organizada;
- a classe de risco está incerta;
- o problema precisa ser quebrado;
- a validação precisa ser planejada;
- há travamento ou fechamento.

### Exemplos de outputs

- Execution Plan;
- classificação de risco;
- plano de decomposição;
- Completion Packet;
- Escalation Note.

---

## `skills/engineering/`

### Função

Skills de engineering cobrem julgamento técnico transversal.

```text
skills/engineering/
├─ architecture-tradeoff-analyst/
├─ observability-first/
├─ refactoring-safety/
├─ product-impact-lens/
├─ repository-discovery-operator/
├─ architecture-by-pain-check/
├─ performance-and-capacity-review/
├─ concurrency-and-statefulness-review/
├─ failure-mode-and-reliability-review/
├─ runtime-resource-diagnostics/
├─ messaging-justification-review/
└─ database-load-and-query-shape-review/
```

### Quando usar

Usar quando a task tocar:
- trade-off;
- arquitetura;
- refactor;
- observabilidade;
- performance;
- concorrência;
- falha parcial;
- runtime;
- mensageria;
- banco;
- risco de over-engineering.

### Limite

Skills de engineering não devem virar desculpa para sofisticar.  
Elas devem aumentar clareza, não cerimônia.

---

## `skills/stack/`

### Função

Skills de stack cobrem capacidades recorrentes da stack principal.

```text
skills/stack/
├─ dotnet/
├─ react/
├─ postgres/
└─ azure/
```

### Quando usar

Usar quando a task exigir conhecimento aplicado da stack e houver risco de erro específico de plataforma, framework, runtime, persistência ou cloud.

### Limite

Skills de stack não devem transformar o harness em apostila técnica.  
Elas devem codificar formas recorrentes de operar melhor naquela stack.

---

## `skills/platform/`

### Função

Skills de platform cobrem ferramentas e superfícies operacionais comuns.

```text
skills/platform/
├─ bash-linux-ops/
├─ git-github-workflow/
├─ docker-container-baseline/
├─ ci-cd-pipeline-review/
├─ terraform-or-bicep-delivery/
├─ http-api-contract-debugging/
└─ cloud-runtime-choice-review/
```

### Quando usar

Usar quando a task tocar:
- shell;
- Git/GitHub;
- Docker;
- CI/CD;
- IaC;
- API contracts;
- escolha de runtime/cloud.

### Limite

Platform skill não substitui authority commands do projeto.  
A verdade local continua vencendo.

---

## `skills/integration/`

### Função

Skills de integration orientam leitura segura de contexto externo.

```text
skills/integration/
├─ mcp-readonly-operator/
├─ github-readonly-ops/
├─ github-projects-readonly/
├─ docs-research-operator/
├─ cloud-readonly-inspection/
└─ observability-readonly-inspection/
```

### Quando usar

Usar quando a task precisar consultar:
- MCP;
- GitHub;
- GitHub Projects;
- documentação externa;
- cloud metadata;
- observabilidade read-only.

### Limite

Integration skill opera preferencialmente em modo read-only.  
Escrita externa depende de policy, trusted integration e autorização.

---

## `skills/security/`

### Função

Skills de security ajudam a aplicar baseline de segurança e revisão de superfície de risco.

```text
skills/security/
├─ secure-coding-baseline/
├─ dependency-and-supply-chain-review/
├─ authn-authz-review/
├─ secrets-and-config-hygiene/
├─ api-abuse-and-input-validation/
├─ frontend-security-baseline/
└─ iac-security-review/
```

### Quando usar

Usar quando a task tocar:
- input externo;
- authn/authz;
- segredo;
- config;
- dependência;
- API;
- frontend surface;
- IaC;
- cloud/security boundary.

### Limite

Security skill não transforma toda task em AppSec profundo.  
Ela aplica profundidade proporcional ao risco.

---

## `skills/hygiene/`

### Função

Skills de hygiene controlam entropia, drift, consistência, documentação e state.

```text
skills/hygiene/
├─ architecture-drift-auditor/
├─ consistency-scanner/
├─ dependency-hygiene-review/
├─ doc-gardener/
└─ project-state-maintainer/
```

### Quando usar

Usar quando houver risco de:
- drift arquitetural;
- duplicação;
- inconsistência;
- dependência sem uso;
- documentação desatualizada;
- `PROJECT_STATE.md` fraco ou ausente.

### Limite

Hygiene não deve virar refactor lateral sem escopo.  
Limpeza precisa ter causalidade.

---

## Relação entre skills e artifacts

Skills podem ajudar a produzir ou revisar:

- Implementation Packet;
- Execution Plan;
- Completion Packet;
- Review Report;
- Escalation Note;
- Investigation Note;
- Project State Entry.

A skill não substitui artifact.  
Ela orienta sua qualidade.

---

## Relação entre skills e policies

Skills devem respeitar policies.

Uma skill nunca pode autorizar:
- comando inseguro;
- mutação fora do escopo;
- produção;
- segredo;
- dependência sem justificativa;
- MCP write sensível;
- automação prematura.

---

## Sinais de skill bloat

Há skill bloat quando:

- existe skill para problema raro;
- a skill só repete protocolo;
- a skill ensina teoria sem ação;
- a skill aumenta prompt sem reduzir erro;
- várias skills fazem a mesma coisa;
- ninguém sabe quando chamar a skill.

---

## Critério para criar nova skill

Criar nova skill apenas quando:

1. o problema é recorrente;
2. o erro é provável;
3. o método é acionável;
4. há checklist claro;
5. há output esperado;
6. ela reduz entropia líquida.

---

## Declaração operacional curta

Skill existe para aplicar método.  
Se não reduz erro, risco ou ambiguidade, não deveria existir.