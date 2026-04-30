# Skill — Testing Verifier

## Finalidade

Esta skill orienta a definição e verificação de validação proporcional para uma task.

Seu papel é impedir que o agente considere uma entrega concluída apenas porque o código parece correto, compila mentalmente ou recebeu explicação convincente.

Validação precisa produzir evidência.

---

## Quando usar

Use esta skill quando:

- houver implementação;
- houver mudança funcional;
- houver alteração em API, banco, frontend, integração, config, pipeline ou runtime;
- o Completion Packet precisar registrar validações;
- a classe de risco for R1 ou superior;
- o review precisar avaliar suficiência de evidência;
- houver dúvida sobre qual teste, build, lint ou checagem executar.

---

## Quando não usar

Não use esta skill quando:

- a task for R0 puramente investigativa;
- não houver mutação;
- a saída for apenas análise documental;
- a validação já estiver definida por authority command claro e suficiente.

---

## Tese central

Validação é proporcional ao risco.

Task simples não exige ritual pesado.  
Task sensível não pode encerrar com “parece certo”.

---

## Tipos de validação

### 1. Validação de leitura

Usada quando a evidência vem de arquivo, documentação, diff ou authority source.

Exemplos:

- confirmar configuração;
- revisar diff;
- comparar com schema;
- verificar README, PROJECT_STATE ou comando local.

### 2. Validação de build

Confirma que o sistema compila ou monta.

Exemplos:

- `dotnet build`;
- build frontend;
- build de container;
- build de pipeline local, quando aplicável.

### 3. Validação de teste

Confirma comportamento esperado.

Exemplos:

- unit tests;
- integration tests;
- component tests;
- endpoint tests;
- regression tests.

### 4. Validação de lint/format

Confirma conformidade estrutural ou estilística.

Exemplos:

- lint;
- format check;
- static analysis;
- typecheck.

### 5. Validação funcional

Confirma que o fluxo atende ao critério de aceite.

Pode ser manual ou automatizada, mas precisa ser descrita.

### 6. Validação de segurança

Aplicável quando a task toca:

- input externo;
- auth;
- segredo;
- dependência;
- API;
- config;
- IaC;
- exposição operacional.

### 7. Validação operacional

Aplicável quando a task toca:

- runtime;
- cloud;
- observabilidade;
- banco;
- fila;
- performance;
- concorrência;
- falha parcial.

---

## Método

### 1. Ler classe de risco

Usar a classe R0–R4 para calibrar profundidade.

### 2. Identificar superfície tocada

Perguntar:

- código?
- API?
- banco?
- frontend?
- dependência?
- segurança?
- runtime?
- documentação?
- state?

### 3. Consultar authority commands

Preferir comandos reais do projeto.

Não inventar comando genérico se o workspace define outro.

### 4. Definir validação mínima

Escolher o menor conjunto de validações que gera confiança proporcional.

### 5. Executar ou registrar impossibilidade

Se a validação não puder ser executada, registrar:

- o que não foi validado;
- por que não foi validado;
- qual risco permanece;
- que validação futura é recomendada.

### 6. Registrar evidência

No Completion Packet, registrar validações realizadas e não realizadas.

---

## Validação por classe de risco

### R0

Validação esperada:

- fontes consultadas;
- achados factuais;
- lacunas.

### R1

Validação esperada:

- leitura de diff;
- comando local simples, se aplicável;
- checagem visual ou factual proporcional.

### R2

Validação esperada:

- build/test/lint quando aplicável;
- validação funcional;
- diff review;
- lacunas explícitas.

### R3

Validação esperada:

- validação forte;
- review explícito;
- segurança e operação quando aplicável;
- possível Core Architect;
- possível Project State Entry.

### R4

Validação esperada:

- autorização humana;
- plano de mitigação;
- rollback;
- evidência máxima;
- tratamento excepcional.

---

## Checklist de validação

Antes de encerrar, perguntar:

- quais comandos foram executados?
- quais testes rodaram?
- o build foi verificado?
- lint/typecheck/format foram considerados?
- a mudança foi validada funcionalmente?
- segurança foi considerada?
- produção/operação foi considerada?
- o diff foi revisado?
- o que não foi validado?
- o risco residual foi declarado?

---

## Outputs esperados

A skill pode produzir:

- estratégia de validação;
- lista de comandos recomendados;
- evidência para Completion Packet;
- lacunas de validação;
- recomendação de review;
- recomendação de Escalation Note.

---

## Critérios de escalonamento

Escalar quando:

- validação essencial não pode ser executada;
- comando de validação é desconhecido e arriscado;
- há falha recorrente sem hipótese;
- validação revela risco maior;
- a task toca produção, segredo ou dado real;
- há suspeita de regressão estrutural.

---

## Anti-patterns

Evitar:

- “não rodei, mas parece certo”;
- esconder teste não executado;
- rodar comando aleatório sem authority source;
- aceitar build mental;
- validar só caminho feliz em task sensível;
- transformar validação em ritual sem relação com risco;
- usar ausência de teste como prova de que não há problema.

---

## Declaração operacional curta

Validação transforma entrega em evidência.  
Sem evidência, a conclusão é apenas retórica.