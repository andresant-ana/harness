# Skill — Architecture Trade-off Analyst

## Finalidade

Esta skill orienta a análise de trade-offs arquiteturais em decisões técnicas relevantes.

Seu papel é impedir que o agente escolha arquitetura, padrão, ferramenta, integração ou estrutura apenas porque parece moderna, elegante ou comum em exemplos da internet.

A skill existe para forçar comparação explícita entre opções, custos, riscos, consequências e adequação ao contexto real do projeto.

---

## Quando usar

Use esta skill quando a task envolver:

- decisão arquitetural;
- escolha entre abordagens técnicas;
- dúvida entre simplicidade e sofisticação;
- introdução de padrão, camada, abstração ou integração;
- escolha entre solução síncrona e assíncrona;
- escolha entre SQL e NoSQL;
- escolha entre monólito modular e microsserviço;
- escolha entre implementar localmente ou adicionar dependência;
- alteração de boundary entre módulos;
- decisão com impacto em produção, escalabilidade, segurança ou manutenção.

---

## Quando não usar

Não use esta skill quando:

- a task for local e trivial;
- não houver decisão real entre opções;
- a escolha já estiver definida por authority source;
- a análise só adicionaria cerimônia;
- o problema for puramente sintático ou mecânico.

---

## Tese central

Toda decisão arquitetural deixa algo na mesa.

Não existe arquitetura perfeita.  
Existe arquitetura adequada para um contexto, com custos aceitos conscientemente.

A pergunta correta não é:

“qual é a melhor arquitetura?”

A pergunta correta é:

“qual opção resolve a dor real com o menor custo aceitável agora, preservando evolução futura suficiente?”

---

## Método

### 1. Definir a decisão real

Antes de comparar opções, declarar qual decisão precisa ser tomada.

Evitar analisar genericamente “arquitetura” sem uma pergunta concreta.

Exemplos bons:

- usar evento assíncrono ou chamada direta neste fluxo?
- criar interface para este gateway agora ou manter implementação concreta?
- separar este módulo ou manter no mesmo bounded context?
- adicionar dependência externa ou implementar utilitário local simples?

---

### 2. Mapear contexto

Levantar:

- objetivo da task;
- estágio do projeto;
- restrições;
- escala esperada;
- risco operacional;
- risco de segurança;
- capacidade do time;
- custo de manutenção;
- realidade de produção;
- authority sources locais.

---

### 3. Listar opções viáveis

Comparar no mínimo duas opções quando houver decisão real.

Exemplo:

- opção A: solução simples/local;
- opção B: abstração/padrão/ferramenta;
- opção C: adiar decisão e registrar critério de revisão futura.

---

### 4. Avaliar cada opção

Para cada opção, analisar:

- benefício;
- custo;
- risco;
- complexidade;
- impacto em manutenção;
- impacto em testabilidade;
- impacto em observabilidade;
- impacto em segurança;
- impacto em produção;
- reversibilidade;
- compatibilidade com arquitetura local.

---

### 5. Aplicar arquitetura por dor real

Perguntar:

- qual dor real justifica esta escolha?
- essa dor existe agora ou é antecipação?
- há evidência da dor?
- a complexidade paga aluguel?
- a solução simples falharia por quê?

Se a dor não for real, preferir simplicidade.

---

### 6. Considerar custo para agentes e humanos

Analisar:

- a solução melhora ou piora navegabilidade?
- aumenta número de arquivos por feature?
- aumenta indireção?
- exige mais contexto para entender?
- cria padrão que o agente pode repetir indevidamente?
- aumenta risco de AI slop?

---

### 7. Recomendar uma direção

A recomendação deve ser clara, mas não dogmática.

Ela deve declarar:

- opção recomendada;
- por que ela é adequada agora;
- custos aceitos;
- riscos remanescentes;
- critério para revisitar.

---

## Output esperado

A saída deve conter:

```md
# Architecture Trade-off Analysis

## Decisão
<decisão analisada>

## Contexto
<contexto relevante>

## Opções consideradas
- <opção A>
- <opção B>
- <opção C>

## Comparação
| Opção | Benefícios | Custos | Riscos | Reversibilidade |
|------|------------|--------|--------|-----------------|
| A | | | | |
| B | | | | |

## Dor real identificada
<dor atual ou ausência de dor>

## Recomendação
<opção recomendada e motivo>

## Custos aceitos
- <custo 1>
- <custo 2>

## Riscos remanescentes
- <risco 1>
- <risco 2>

## Critério de revisão futura
<quando reavaliar>
```

---

## Checklist de qualidade

Antes de recomendar, verificar:

- a decisão real foi formulada?
- opções foram comparadas?
- a dor real foi demonstrada?
- custo de complexidade foi considerado?
- reversibilidade foi considerada?
- produção foi considerada?
- segurança foi considerada?
- impacto em agentes e contexto foi considerado?
- a recomendação é proporcional?
- há critério de revisão futura?

---

## Critérios de escalonamento

Escalar para humano ou Core Architect quando:

- a decisão for R3 ou superior;
- houver impacto estrutural;
- houver conflito entre simplicidade e escalabilidade;
- houver risco de lock-in;
- houver impacto de segurança ou produção;
- a recomendação depender de contexto de negócio;
- houver mais de uma opção plausível com trade-offs fortes.

---

## Anti-patterns

Evitar:

- escolher tecnologia por hype;
- aplicar padrão porque “é boa prática” sem dor real;
- confundir testabilidade com excesso de interfaces;
- criar abstração para variação hipotética;
- decidir arquitetura sem considerar operação;
- ignorar custo de contexto para agentes;
- recomendar opção sofisticada sem critério de revisão;
- transformar todo trade-off em decisão R3.

---

## Declaração operacional curta

Trade-off bom explicita o que se ganha, o que se perde e por que a escolha faz sentido agora.