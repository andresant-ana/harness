# Skill — PostgreSQL Schema Change Safety

## Finalidade

Esta skill orienta alterações de schema em PostgreSQL, incluindo tabelas, colunas, tipos, índices, constraints, migrations, compatibilidade, rollback, lock, dados existentes e impacto operacional.

Seu papel é impedir que o agente trate mudança de schema como detalhe mecânico, ignorando risco de lock, perda de dados, incompatibilidade entre versões da aplicação, custo de índice, rollback frágil ou impacto em produção.

Esta skill não substitui `efcore-migrations-safety`.  
A skill de EF Core olha a mudança pelo lado da aplicação e do ORM.  
Esta skill olha pelo lado do PostgreSQL real: schema, storage, locks, constraints, planner, dados existentes e operação.

---

## Quando usar

Use esta skill quando a task tocar:

- criação de tabela;
- remoção de tabela;
- criação, remoção ou alteração de coluna;
- alteração de tipo;
- alteração de nulabilidade;
- default value;
- índice;
- unique constraint;
- foreign key;
- check constraint;
- enum;
- migration;
- seed data;
- backfill;
- rename;
- rollback;
- alteração em schema usado por endpoint, job, query ou relatório;
- mudança com possível impacto em produção.

---

## Quando não usar

Não use esta skill quando:

- não houver alteração de schema;
- a task for puramente de query sem mudança estrutural;
- a mudança for apenas documental;
- o risco já tiver sido analisado por skill equivalente e não houver nova informação;
- a análise seria especulativa sem objeto concreto.

---

## Tese central

Schema é contrato persistente.

Código pode mudar rápido.  
Banco guarda estado real, dados reais, locks reais e consequências que podem sobreviver ao deploy.

Toda mudança de schema deve responder:

- o que acontece com dados existentes?
- a aplicação antiga continua funcionando?
- a aplicação nova funciona durante rollout?
- a migration pode bloquear escrita/leitura?
- há rollback realista?
- há risco de perda de dado?
- há risco de custo operacional?

---

## Método

### 1. Identificar alteração de schema

Classificar a mudança como:

- tabela nova;
- coluna nova;
- coluna removida;
- rename;
- tipo alterado;
- nulabilidade alterada;
- default alterado;
- índice novo/removido;
- constraint nova/removida;
- relacionamento novo/removido;
- backfill;
- seed;
- enum alterado.

---

### 2. Avaliar dados existentes

Perguntar:

- a tabela já tem dados?
- a coluna nova aceita `NULL`?
- há default?
- o default reescreve tabela ou é metadata-only na versão usada?
- mudança de tipo pode falhar?
- rename foi detectado como rename ou drop/create?
- remoção de coluna perde dado?
- constraint nova falha em dados existentes?
- backfill precisa ser feito?

---

### 3. Avaliar compatibilidade de deploy

Verificar:

- aplicação antiga funciona com schema novo?
- aplicação nova funciona com schema antigo?
- há janela de deploy com duas versões?
- a mudança exige deploy em fases?
- há necessidade de expand/contract migration?
- há endpoint/job usando o campo alterado?

Mudanças incompatíveis devem ser tratadas como risco maior.

---

### 4. Avaliar locks e impacto operacional

Perguntar:

- a operação toma lock forte?
- pode bloquear escrita?
- pode bloquear leitura?
- índice será criado em tabela grande?
- é necessário `CREATE INDEX CONCURRENTLY`?
- constraint pode ser validada em duas fases?
- backfill pode ser batelado?
- transação da migration pode ficar longa?
- há risco de timeout em deploy?

---

### 5. Avaliar índices

Para índice novo:

- qual query justifica?
- qual seletividade esperada?
- qual cardinalidade?
- qual custo em escrita?
- índice composto está na ordem certa?
- índice parcial faz sentido?
- índice único protege regra real?
- índice duplica outro existente?

Para índice removido:

- quem usa?
- há query ou constraint dependendo dele?
- o planner pode degradar?

---

### 6. Avaliar constraints

Constraints devem proteger invariantes reais.

Verificar:

- `NOT NULL`;
- `UNIQUE`;
- `FOREIGN KEY`;
- `CHECK`;
- exclusão;
- cascade behavior;
- delete/update behavior.

Perguntar:

- a constraint representa regra de domínio?
- a aplicação já garante isso ou o banco também deve garantir?
- há dados existentes violando a constraint?
- o erro gerado será tratado?

---

### 7. Avaliar rollback

Perguntar:

- `Down` é possível?
- rollback perde dado?
- rollback é apenas sintático ou operacionalmente seguro?
- se migration for aplicada em produção, como reverter?
- rollback de app e rollback de schema são compatíveis?

Nem toda migration tem rollback seguro.  
Quando não tiver, registrar explicitamente.

---

### 8. Definir validação

Validações possíveis:

- revisar SQL gerado;
- rodar migration em banco local;
- testar `Up` e `Down`;
- rodar testes de integração;
- inspecionar locks esperados;
- usar `EXPLAIN` para queries afetadas;
- validar constraints contra dados de amostra;
- revisar plano de deploy.

Sempre respeitar authority commands locais.

---

## Output esperado

```md
# PostgreSQL Schema Change Safety Review

## Alteração analisada
<tabela, coluna, índice, constraint, relacionamento ou migration>

## Tipo de mudança
<create | alter | drop | rename | index | constraint | backfill | seed | outro>

## Dados existentes
<risco baixo | moderado | alto | incerto>

## Compatibilidade de deploy
<compatível | exige fases | incompatível | incerta>

## Locks e impacto operacional
<análise curta>

## Índices/constraints
<justificativa e riscos>

## Rollback
<seguro | parcial | destrutivo | incerto>

## Validação recomendada
- <validação 1>
- <validação 2>

## Veredito
<suficiente | ajustar | medir | escalar>

## Risco residual
<risco que permanece>
```

---

## Checklist de qualidade

Antes de aceitar a mudança, verificar:

- dados existentes foram considerados?
- mudança destrutiva foi identificada?
- rename não virou drop/create por acidente?
- nulabilidade/default fazem sentido?
- constraint nova é compatível com dados existentes?
- índice novo tem query justificadora?
- índice não duplica outro?
- custo de escrita foi considerado?
- locks foram considerados?
- compatibilidade entre app antiga/nova foi avaliada?
- rollback foi descrito honestamente?
- validação foi definida?

---

## Critérios de escalonamento

Escalar quando:

- houver produção ou dados reais;
- a migration for destrutiva;
- houver alteração de tipo arriscada;
- houver remoção de coluna/tabela;
- houver backfill relevante;
- índice em tabela grande puder bloquear ou custar caro;
- constraint puder falhar em dados existentes;
- deploy exigir duas fases;
- rollback for destrutivo ou incerto;
- houver trade-off entre integridade, disponibilidade e simplicidade.

---

## Anti-patterns

Evitar:

- aceitar migration sem revisar SQL;
- dropar coluna sem plano de dados;
- alterar tipo sem verificar conversão;
- criar índice “por via das dúvidas”;
- ignorar custo de índice em escrita;
- criar FK/cascade sem entender impacto;
- adicionar `NOT NULL` em tabela com dados sem default/backfill;
- fazer backfill enorme em uma transação cega;
- aplicar migration em produção sem plano;
- tratar rollback como formalidade.

---

## Relação com outras skills

Use junto com:

- `efcore-migrations-safety`, se a mudança vier de EF Core;
- `postgres-query-review`, se a alteração for motivada por query;
- `database-load-and-query-shape-review`, para análise transversal de carga;
- `iac-security-review`, se schema estiver ligado a provisionamento;
- `delivery-wrapup`, para registrar validações e lacunas;
- `project-state-maintainer`, se a decisão de schema for durável.

---

## Declaração operacional curta

Schema PostgreSQL é contrato persistente.  
Mudança segura considera dados existentes, locks, compatibilidade, rollback e operação real.