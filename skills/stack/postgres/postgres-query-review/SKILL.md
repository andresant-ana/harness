# Skill — PostgreSQL Query Review

## Finalidade

Esta skill orienta revisão de queries PostgreSQL, incluindo shape, filtros, joins, índices, cardinalidade, paginação, transações, isolamento, N+1, agregações, ordenação e custo de leitura/escrita.

Seu papel é impedir que o agente escreva ou aprove queries que parecem corretas em banco pequeno, mas degradam com volume real, usam índice errado, fazem scan desnecessário, bloqueiam recursos ou criam custo operacional invisível.

Esta skill complementa `database-load-and-query-shape-review`.  
A skill transversal olha banco de forma geral.  
Esta skill foca comportamento específico de PostgreSQL.

---

## Quando usar

Use esta skill quando a task tocar:

- `SELECT`;
- `INSERT`;
- `UPDATE`;
- `DELETE`;
- `UPSERT`;
- `JOIN`;
- `WHERE`;
- `ORDER BY`;
- `GROUP BY`;
- agregação;
- busca textual;
- paginação;
- filtros;
- relatórios;
- dashboards;
- queries geradas por ORM;
- stored SQL;
- migrations com DML;
- transações;
- locks;
- endpoint que consulta banco;
- job com leitura/escrita em lote;
- suspeita de lentidão;
- N+1.

---

## Quando não usar

Não use esta skill quando:

- não houver query ou banco envolvido;
- a query for trivial, pequena e já coberta por padrão local;
- a task for apenas schema sem query;
- a análise duplicaria review já feito sem novo risco;
- não houver cardinalidade, performance ou consistência relevante.

---

## Tese central

Query correta não é apenas a que retorna o resultado certo.

Query correta em sistema real precisa respeitar:

- cardinalidade;
- seletividade;
- índice;
- paginação;
- projeção;
- custo de join;
- transação;
- locks;
- concorrência;
- volume esperado;
- comportamento sob dados reais.

Banco vazio mente.  
Banco real cobra.

---

## Método

### 1. Identificar query shape

Registrar:

- tabelas envolvidas;
- filtros;
- joins;
- ordenação;
- agregações;
- paginação;
- projeção;
- escrita;
- transação;
- origem da query;
- frequência esperada.

Se a query vier de ORM, considerar SQL gerado, não apenas LINQ/código fonte.

---

### 2. Avaliar cardinalidade

Perguntar:

- quantas linhas existem hoje?
- quantas podem existir?
- quantas serão filtradas?
- quantas serão retornadas?
- a query roda por request?
- roda em job?
- roda em relatório?
- pode ser chamada muitas vezes?
- há limite ou paginação?

Quando cardinalidade for desconhecida e potencialmente alta, registrar risco.

---

### 3. Avaliar filtros e seletividade

Verificar:

- filtros usam colunas indexáveis?
- filtro é seletivo?
- filtro com função impede uso de índice?
- `ILIKE '%term%'` pode causar scan?
- cast em coluna prejudica índice?
- filtro por data usa range eficiente?
- filtro por tenant/owner aparece cedo?

---

### 4. Avaliar joins

Perguntar:

- joins são necessários?
- cardinalidade entre tabelas está clara?
- join pode multiplicar linhas?
- há risco de join explosivo?
- FK/índice sustentam join?
- seria melhor projetar dados mínimos?
- há relação opcional gerando `LEFT JOIN` pesado?

---

### 5. Avaliar projeção

Verificar:

- query retorna apenas colunas necessárias?
- evita `SELECT *` em fluxo relevante?
- evita carregar payload grande?
- evita carregar entidade completa quando DTO bastaria?
- evita agregação no app após carregar dados demais?

---

### 6. Avaliar paginação e ordenação

Perguntar:

- há `LIMIT`?
- há paginação?
- `OFFSET` é aceitável para volume esperado?
- keyset pagination faria mais sentido?
- `ORDER BY` usa índice?
- ordenação é determinística?
- há tie-breaker, como `id`?

Paginação sem ordenação estável pode gerar resultado inconsistente.

---

### 7. Avaliar índices

Para cada query relevante:

- qual índice sustentaria filtro?
- índice composto está na ordem certa?
- índice parcial faria sentido?
- índice cobre ordenação?
- índice duplica outro?
- custo de escrita compensa?
- índice é necessário agora ou prematuro?

Índice deve nascer de query e cardinalidade, não de palpite.

---

### 8. Avaliar transações e locks

Perguntar:

- a transação é necessária?
- duração é curta?
- há I/O externo dentro da transação?
- operação atualiza muitas linhas?
- há risco de lock contention?
- isolamento padrão basta?
- `SELECT ... FOR UPDATE` é necessário?
- há risco de deadlock?
- operação é idempotente?

---

### 9. Avaliar escrita

Para `INSERT/UPDATE/DELETE/UPSERT`:

- há constraint protegendo consistência?
- `ON CONFLICT` está correto?
- update tem filtro seletivo?
- delete é seguro?
- operação em massa é batelada?
- retorno é necessário?
- trigger ou cascade pode amplificar custo?

---

### 10. Definir validação

Validações possíveis:

- `EXPLAIN`;
- `EXPLAIN ANALYZE` em ambiente seguro;
- inspecionar SQL gerado por ORM;
- query log;
- teste de integração;
- medição local com dados de amostra;
- revisar índices existentes;
- verificar cardinalidade;
- avaliar plano de execução;
- simular paginação.

Não usar `EXPLAIN ANALYZE` em produção sem autorização e cuidado.

---

## Output esperado

```md
# PostgreSQL Query Review

## Operação analisada
<SELECT | INSERT | UPDATE | DELETE | UPSERT | relatório | endpoint | job>

## Query shape
<tabelas, filtros, joins, ordenação, paginação, projeção>

## Cardinalidade
<volume conhecido, esperado ou incerto>

## Índices relevantes
- <índice existente/proposto/lacuna>

## Riscos identificados
- <full scan>
- <N+1>
- <join explosivo>
- <paginação instável>
- <lock>
- <transação longa>
- <outro>

## Transação/isolamento
<análise curta ou não aplicável>

## Validação recomendada
- <EXPLAIN>
- <SQL gerado>
- <teste>
- <query log>
- <outro>

## Veredito
<suficiente | ajustar | medir | escalar>

## Risco residual
<risco que permanece>
```

---

## Checklist de qualidade

Antes de aceitar uma query relevante, verificar:

- cardinalidade foi considerada?
- há filtro seletivo?
- há paginação onde precisa?
- ordenação é estável?
- há projeção mínima?
- não há `SELECT *` em fluxo relevante?
- não há N+1?
- joins têm cardinalidade entendida?
- índice existente ou necessário foi considerado?
- índice novo é justificado por query real?
- transação é curta?
- não há I/O externo dentro da transação?
- escrita em massa é controlada?
- validação foi definida ou lacuna registrada?

---

## Critérios de escalonamento

Escalar quando:

- query afeta fluxo crítico;
- cardinalidade é desconhecida e potencialmente alta;
- query pode causar full scan em tabela grande;
- índice novo pode afetar produção;
- transação pode bloquear fluxo relevante;
- operação pode gerar deadlock ou lock contention;
- relatório ou busca exige decisão de produto/performance;
- query exige mudança de schema;
- validação adequada não pode ser feita e o risco é alto.

---

## Anti-patterns

Evitar:

- filtrar no backend após carregar dados demais;
- buscar tudo e paginar no frontend;
- `OFFSET` profundo sem considerar custo;
- `ORDER BY` instável;
- `SELECT *` em endpoint relevante;
- `ILIKE '%term%'` em tabela grande sem estratégia;
- função em coluna indexada sem entender impacto;
- query dentro de loop;
- update/delete sem filtro seguro;
- transação envolvendo chamada externa;
- criar índice sem query concreta;
- aceitar performance local com banco vazio.

---

## Relação com outras skills

Use junto com:

- `database-load-and-query-shape-review`, para revisão transversal de carga;
- `postgres-schema-change-safety`, se a query exigir índice/schema;
- `efcore-migrations-safety`, se a query vier de EF Core;
- `dotnet-performance-baseline`, se a query estiver em hot path .NET;
- `performance-and-capacity-review`, se houver impacto sob carga;
- `failure-mode-and-reliability-review`, se houver transação, retry ou falha parcial.

---

## Declaração operacional curta

Query PostgreSQL boa respeita dados reais, índices, cardinalidade e transações.  
Resultado correto em banco pequeno não prova comportamento seguro em produção.