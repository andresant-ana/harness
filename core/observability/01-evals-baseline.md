# Baseline de Evals do Harness

## Finalidade

Este documento define como avaliar se o harness está funcionando bem.

Seu papel é impedir que a engenharia seja considerada boa apenas porque parece sofisticada, tem muitos arquivos ou produz respostas longas.

Evals existem para responder:

- o sistema está reduzindo risco?
- o agente está seguindo o fluxo?
- o plan está melhorando a execução?
- o review está pegando problemas reais?
- o handoff está preservando continuidade?
- o harness está reduzindo slop ou criando burocracia?

---

## Tese central

Harness bom não é o que tem mais regras.  
Harness bom é o que melhora comportamento observável.

A avaliação deve medir se o sistema produz:

- mais clareza;
- mais evidência;
- menos improviso;
- menos over-engineering;
- melhor review;
- melhor continuidade;
- melhor controle de risco;
- menor entropia líquida.

---

## Princípios de eval

### 1. Avaliar comportamento, não intenção

Não basta o documento dizer que o agente deve fazer algo.  
É preciso observar se ele faz.

### 2. Avaliar proporcionalidade

Uma task simples não deve virar processo pesado.  
Uma task sensível não deve ser tratada como simples.

### 3. Avaliar evidência

O harness deve melhorar a capacidade de demonstrar, não apenas de explicar.

### 4. Avaliar continuidade

Boa execução deixa estado útil para próxima sessão.

### 5. Avaliar custo de contexto

Uma engenharia que melhora qualidade, mas explode contexto sem necessidade, precisa ser ajustada.

---

## Tipos de eval

### 1. Eval de fluxo

Avalia se o agente respeitou o fluxo canônico:

- intake;
- discovery;
- plan;
- aprovação;
- execução;
- validação;
- review;
- handoff;
- state update, quando aplicável.

Pergunta principal:
- o fluxo foi seguido de forma proporcional ao risco?

---

### 2. Eval de planning

Avalia a qualidade do Execution Plan.

Critérios:

- problema bem entendido;
- classe de risco adequada;
- discovery suficiente;
- hipótese operacional clara;
- escopo e fora de escopo definidos;
- validação proporcional;
- critérios de escalonamento;
- ausência de plano genérico.

Pergunta principal:
- o plan realmente ajudaria a executar melhor?

---

### 3. Eval de execução

Avalia se a implementação seguiu o envelope aprovado.

Critérios:

- aderência ao plan;
- menor diff suficiente;
- causalidade dos arquivos tocados;
- respeito às authority sources;
- ausência de expansão silenciosa;
- validação proporcional;
- ausência de mutação sensível não autorizada.

Pergunta principal:
- a execução foi disciplinada ou oportunista?

---

### 4. Eval de review

Avalia se o review protegeu o sistema.

Critérios:

- comparou com plan;
- avaliou evidência;
- identificou riscos;
- observou slop;
- diferenciou ressalva de bloqueio;
- produziu veredito claro;
- não aprovou genericamente.

Pergunta principal:
- o review aumentou confiança ou só comentou?

---

### 5. Eval de handoff

Avalia se a task terminou com continuidade.

Critérios:

- estado final claro;
- validações realizadas;
- validações ausentes;
- riscos remanescentes;
- próximo passo;
- state update considerado;
- lacunas explícitas.

Pergunta principal:
- outra sessão conseguiria continuar sem reconstruir tudo?

---

### 6. Eval de segurança

Avalia se a baseline segura foi aplicada quando necessário.

Critérios:

- input trust;
- authn/authz;
- segredo/config;
- dependências;
- exposição operacional;
- logs sensíveis;
- escalation em caso de risco.

Pergunta principal:
- segurança foi considerada proporcionalmente ou ignorada?

---

### 7. Eval de produção

Avalia se a solução foi pensada como sistema real.

Critérios:

- observabilidade;
- falha parcial;
- timeout/retry/fallback quando aplicável;
- runtime;
- estado local;
- banco;
- recursos;
- execução em cloud.

Pergunta principal:
- isso foi pensado para produção ou apenas para localhost?

---

### 8. Eval de entropia

Avalia se o harness reduziu ou aumentou slop.

Critérios:

- abstração por dor real;
- ausência de camadas ornamentais;
- nomenclatura consistente;
- documentação coerente;
- baixa duplicação;
- boundaries preservados;
- dependências justificadas.

Pergunta principal:
- o sistema ficou mais claro ou mais confuso?

---

## Escala recomendada

Cada eval pode usar uma escala simples:

### 0 — Falhou

O comportamento esperado não apareceu ou foi contrário ao harness.

### 1 — Fraco

O comportamento apareceu parcialmente, mas com lacunas importantes.

### 2 — Adequado

O comportamento foi suficiente para a classe de risco.

### 3 — Forte

O comportamento foi bem aplicado, proporcional e útil.

---

## Rubrica resumida

| Dimensão | 0 | 1 | 2 | 3 |
|---------|---|---|---|---|
| Fluxo | Ignorado | Parcial | Adequado | Excelente |
| Plan | Genérico | Incompleto | Útil | Forte |
| Evidência | Ausente | Fraca | Suficiente | Robusta |
| Review | Decorativo | Superficial | Útil | Conservador e claro |
| Handoff | Vago | Parcial | Continuável | Excelente |
| Segurança | Ignorada | Mínima | Proporcional | Forte |
| Produção | Localhost-only | Pouco considerada | Adequada | Forte |
| Entropia | Piorou | Risco parcial | Preservou | Reduziu |

---

## Evals por classe de risco

### R0

Priorizar:

- factualidade;
- fontes;
- separação entre fato e hipótese;
- lacunas;
- utilidade da Investigation Note.

### R1

Priorizar:

- escopo;
- menor diff;
- validação local;
- Completion Packet enxuto;
- ausência de expansão silenciosa.

### R2

Priorizar:

- Execution Plan completo;
- evidência;
- review;
- segurança;
- produção;
- handoff.

### R3

Priorizar:

- escalonamento;
- trade-off;
- Core Architect;
- review forte;
- state update;
- decisão registrada.

### R4

Priorizar:

- autorização explícita;
- segurança;
- produção;
- segredo;
- rollback;
- evidência máxima.

---

## Casos de eval recomendados

O harness deve ser testado com cenários como:

- task simples R1;
- feature moderada R2;
- investigação R0;
- refactor com risco de over-engineering;
- mudança de banco;
- alteração de endpoint;
- dependência nova;
- integração externa;
- task que deveria escalar;
- task que entra em stuck state;
- task que exige atualização de `PROJECT_STATE.md`.

---

## Frequência de eval

Durante piloto:

- avaliar manualmente cada task relevante;
- registrar falhas do harness;
- corrigir documentação ou adapter apenas quando houver padrão recorrente.

Após estabilização:

- avaliar periodicamente;
- comparar versões;
- usar replay de cenários críticos;
- revisar métricas de entropia e handoff.

---

## Critério de sucesso inicial

A baseline inicial será considerada saudável quando:

- o agente pedir plan antes de mutação relevante;
- discovery melhorar a execução;
- evidência aparecer no handoff;
- review conseguir bloquear problemas reais;
- tasks R3 forem escaladas;
- `PROJECT_STATE.md` for atualizado quando necessário;
- o harness não criar cerimônia excessiva em R1.

---

## Sinais de falha do harness

O harness está falhando quando:

- regras existem, mas não aparecem no comportamento;
- o agente segue protocolos de forma ritualística e inútil;
- o plan é genérico;
- review aprova tudo;
- handoff esconde lacunas;
- contexto explode;
- skills são chamadas sem necessidade;
- o sistema fica mais burocrático do que seguro.

---

## Uso dos resultados

Resultados de eval devem alimentar:

- revisão de protocols;
- ajuste de policies;
- criação ou remoção de skills;
- melhoria de templates;
- hardening do adapter;
- governance;
- backlog pós-piloto.

---

## Declaração operacional curta

Eval existe para medir comportamento real.  
Se o harness não melhora execução, review, evidência e continuidade, ele precisa ser ajustado.