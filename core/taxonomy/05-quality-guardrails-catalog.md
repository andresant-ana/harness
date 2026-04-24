# Catálogo de Guardrails de Qualidade

## Finalidade

Este documento cataloga os guardrails de qualidade reconhecidos pelo harness.

Seu papel é servir como índice operacional das lentes que o sistema deve aplicar para evitar slop, improviso, risco, over-engineering e entrega sem evidência.

Este catálogo não substitui constitution, protocols ou policies.  
Ele aponta qual guardrail deve ser lembrado em cada tipo de situação.

---

## Tese central

Qualidade não nasce de uma única regra.

Ela nasce da combinação de:
- escopo claro;
- discovery;
- autoridade local;
- contexto enxuto;
- segurança;
- produção;
- evidência;
- review;
- handoff;
- controle de entropia;
- autonomia limitada.

Guardrails existem para impedir que o agente pareça produtivo enquanto degrada o sistema.

---

## Lista de guardrails principais

| Guardrail | Origem principal | Função |
|-----------|------------------|--------|
| Planejamento antes de mutação | `02-operating-laws.md` / `00-implementation-flow.md` | Impedir execução improvisada |
| Discovery antes de edição | `01-repository-discovery.md` | Entender repo antes de tocar |
| Authority sources | `02-authority-sources.md` | Fazer verdade local vencer suposição |
| Economia de contexto | `03-context-economy-and-compaction.md` | Evitar contexto inflado |
| Engenharia segura | `04-secure-engineering-baseline.md` | Aplicar baseline de segurança |
| Produção desde o início | `05-production-minded-execution.md` | Evitar solução de localhost |
| Evidência acima de retórica | `06-evidence-standard.md` | Sustentar conclusão factual |
| Review conservador | `07-review-protocol.md` | Proteger qualidade antes de aceitar |
| Handoff honesto | `08-handoff-protocol.md` | Preservar continuidade |
| Stuck recovery | `09-stuck-detection-and-recovery.md` | Parar insistência sem convergência |
| Entropy management | `10-entropy-management.md` | Controlar slop e drift |
| Project state maintenance | `11-project-state-maintenance.md` | Preservar memória técnica |
| External state reading | `12-external-state-reading.md` | Ler fora sem confundir autoridade |
| Command safety | `00-command-safety-policy.md` | Governar comandos |
| File mutation | `01-file-mutation-policy.md` | Governar diffs |
| Git discipline | `02-git-policy.md` | Preservar histórico e isolamento |
| MCP read-only first | `03-mcp-policy.md` | Evitar integração perigosa |
| Runtime boundaries | `04-tool-and-runtime-boundaries.md` | Separar núcleo e adapter |
| Secret/prod protection | `05-secret-and-prod-policy.md` | Proteger superfícies sensíveis |
| Automation maturity | `06-automation-promotion-policy.md` | Evitar automação prematura |
| Trusted integrations | `07-trusted-integrations-policy.md` | Classificar integrações |
| Dependency discipline | `08-dependency-introduction-policy.md` | Tratar dependência como complexidade |
| Observability minimum | `09-observability-minimum-policy.md` | Garantir visibilidade |
| State vs board separation | `10-project-state-vs-board-policy.md` | Não confundir trabalho e verdade técnica |

---

## Guardrail — Planejamento antes de mutação

### Quando aplicar

Sempre que a task não for trivial.

### Protege contra

- execução impulsiva;
- escopo solto;
- mudança sem validação;
- plano inventado depois do diff.

### Pergunta-chave

Existe Execution Plan suficiente para esta classe de risco?

---

## Guardrail — Discovery antes de edição

### Quando aplicar

Antes de qualquer mutação relevante.

### Protege contra

- editar arquivo errado;
- ignorar convenção local;
- duplicar lógica;
- inflar contexto sem mapa.

### Pergunta-chave

O executor entende a topologia do repo antes de tocar nele?

---

## Guardrail — Authority sources

### Quando aplicar

Sempre que houver suposição sobre comandos, arquitetura, convenção ou fluxo local.

### Protege contra

- conhecimento genérico vencendo realidade do projeto;
- comando inventado;
- arquitetura assumida;
- validação errada.

### Pergunta-chave

Qual fonte local sustenta essa decisão?

---

## Guardrail — Economia de contexto

### Quando aplicar

Durante discovery, sessões longas e uso de skills.

### Protege contra

- transcript infinito;
- leitura massiva inútil;
- perda de foco;
- custo de contexto sem ganho.

### Pergunta-chave

Esse contexto ajuda a decisão atual ou só aumenta ruído?

---

## Guardrail — Engenharia segura

### Quando aplicar

Quando a task tocar input, auth, config, dependência, API, integração, infra ou dados.

### Protege contra

- input não confiável;
- authz ausente;
- segredo exposto;
- dependência arriscada;
- superfície abusável.

### Pergunta-chave

Que superfície de risco esta mudança altera?

---

## Guardrail — Produção desde o início

### Quando aplicar

Quando a task tocar fluxo funcional relevante, operação, runtime, cloud, banco ou integração.

### Protege contra

- solução só de localhost;
- invisibilidade operacional;
- falha parcial ignorada;
- autoscaling como muleta.

### Pergunta-chave

Como isso roda, falha, escala e será observado?

---

## Guardrail — Evidência acima de retórica

### Quando aplicar

Sempre que houver conclusão, plan, review ou entrega.

### Protege contra

- linguagem confiante sem base;
- validação ausente;
- fechamento prematuro;
- “parece certo”.

### Pergunta-chave

O que foi efetivamente observado, executado ou verificado?

---

## Guardrail — Review conservador

### Quando aplicar

Em R2+, mudanças sensíveis, diffs relevantes ou entregas com lacunas.

### Protege contra

- aprovação fraca;
- slop;
- complexidade injustificada;
- risco residual invisível.

### Pergunta-chave

Isso deve ser aprovado, aprovado com ressalvas, reavaliado ou bloqueado?

---

## Guardrail — Handoff honesto

### Quando aplicar

Ao encerrar qualquer task relevante.

### Protege contra

- perda de continuidade;
- lacunas escondidas;
- próxima sessão sem contexto;
- conclusão genérica.

### Pergunta-chave

Outra pessoa ou agente consegue continuar sem reconstruir tudo?

---

## Guardrail — Stuck recovery

### Quando aplicar

Quando execução não converge.

### Protege contra

- tentativas aleatórias;
- mutação especulativa;
- consumo de contexto;
- bug virando refactor.

### Pergunta-chave

O sistema ainda está aprendendo ou só repetindo tentativa?

---

## Guardrail — Entropy management

### Quando aplicar

Sempre que o diff ampliar estrutura, arquivos, convenções ou dependências.

### Protege contra

- AI slop;
- abstraction bloat;
- drift arquitetural;
- documentação vencida;
- navegação ruim.

### Pergunta-chave

Esta mudança deixa o sistema mais claro ou mais confuso?

---

## Guardrail — Project state maintenance

### Quando aplicar

Quando uma task muda verdade durável do projeto.

### Protege contra

- memória presa em conversa;
- estado técnico desatualizado;
- reinvestigação futura;
- decisões esquecidas.

### Pergunta-chave

Isso precisa sobreviver à sessão?

---

## Guardrail — External state reading

### Quando aplicar

Quando board, issues, docs, observabilidade ou MCP podem reduzir incerteza.

### Protege contra

- trabalhar em task errada;
- ignorar estado externo;
- mas também contra confundir board com arquitetura.

### Pergunta-chave

Que pergunta externa estamos tentando responder?

---

## Guardrail — Command safety

### Quando aplicar

Antes de rodar comandos.

### Protege contra

- comando destrutivo;
- script opaco;
- mutação ampla;
- produção acidental.

### Pergunta-chave

Esse comando lê, valida, muta localmente ou toca superfície sensível?

---

## Guardrail — File mutation

### Quando aplicar

Antes e depois de editar arquivos.

### Protege contra

- diff grande demais;
- edição sem causalidade;
- refactor lateral;
- arquivos novos sem necessidade.

### Pergunta-chave

Por que este arquivo precisa estar no diff?

---

## Guardrail — Dependency discipline

### Quando aplicar

Antes de adicionar ou atualizar dependência.

### Protege contra

- complexidade importada;
- supply chain;
- duplicação de capacidade;
- dependência por conveniência do agente.

### Pergunta-chave

Essa dependência reduz complexidade líquida ou só economiza esforço imediato?

---

## Guardrail — Observability minimum

### Quando aplicar

Em fluxos relevantes, integrações, erros, runtime e produção.

### Protege contra

- sistema invisível;
- diagnóstico difícil;
- health check enganoso;
- erro silencioso.

### Pergunta-chave

Como saberemos que isso funciona ou falha em produção?

---

## Guardrails por classe de risco

### R0

Priorizar:
- discovery;
- evidence;
- investigation note;
- external state reading, se necessário.

### R1

Priorizar:
- file mutation;
- command safety;
- completion enxuto;
- validação local.

### R2

Priorizar:
- Execution Plan;
- evidence;
- security baseline;
- production-minded execution;
- review;
- handoff.

### R3

Priorizar:
- escalation;
- architect-critic;
- review forte;
- project state;
- architecture by pain;
- observability.

### R4

Priorizar:
- secret/prod policy;
- autorização humana;
- tratamento excepcional;
- evidência máxima;
- rollback/mitigação.

---

## Declaração operacional curta

Guardrail é lente de proteção.  
O harness não confia em produtividade aparente.  
Ele exige clareza, evidência, proporção e continuidade.