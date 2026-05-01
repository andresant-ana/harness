# Skill — EF Core Migrations Safety

## Finalidade

Esta skill orienta alterações em entidades persistidas, DbContext, mappings, migrations e schema changes usando Entity Framework Core.

Seu papel é impedir que o agente trate migration como detalhe mecânico, ignorando risco de dados, locks, rollback, compatibilidade, cardinalidade, queries e impacto em produção.

---

## Quando usar

Use esta skill quando a task tocar:

- entidade persistida;
- `DbContext`;
- `DbSet`;
- Fluent API;
- migrations EF Core;
- relacionamento;
- coluna;
- índice;
- constraint;
- seed;
- tracking;
- query LINQ relevante;
- mudança de schema;
- alteração que impacta PostgreSQL ou banco relacional.

---

## Quando não usar

Não use esta skill quando:

- não houver persistência envolvida;
- a alteração for puramente em memória;
- a migration já foi criada e revisada em outra etapa;
- a task é apenas leitura e não altera schema/query.

---

## Tese central

Migration é mudança de dados e contrato persistente.

Código pode ser revertido rapidamente.  
Mudança de banco pode deixar dado, lock, incompatibilidade ou perda.

Toda alteração persistida precisa considerar:

- schema;
- dado existente;
- compatibilidade;
- rollback;
- performance;
- validação;
- produção.

---

## Método

### 1. Identificar mudança persistida

Classificar:

- nova tabela;
- nova coluna;
- remoção de coluna;
- alteração de tipo;
- alteração de nulabilidade;
- novo índice;
- nova constraint;
- relacionamento;
- seed;
- rename;
- migration corretiva;
- query sem schema change.

---

### 2. Avaliar dado existente

Perguntar:

- já há dados na tabela?
- coluna nova é nullable ou tem default?
- alteração pode quebrar registros existentes?
- mudança de tipo pode perder dado?
- rename será detectado como drop/create?
- há necessidade de backfill?
- há compatibilidade com versão anterior da aplicação?

---

### 3. Avaliar migration gerada

Ao gerar migration, revisar:

- `Up`;
- `Down`;
- operações destrutivas;
- drops;
- renames;
- defaults;
- constraints;
- índices;
- nomes gerados;
- SQL implícito;
- impacto em lock.

Migration gerada automaticamente não é automaticamente correta.

---

### 4. Avaliar query/tracking

Se a task toca queries, verificar:

- tracking desnecessário;
- `AsNoTracking` em leitura;
- includes excessivos;
- N+1;
- projeção;
- paginação;
- filtros;
- transações;
- concorrência.

---

### 5. Avaliar índice e constraint

Perguntar:

- filtro frequente precisa de índice?
- índice novo custa escrita?
- constraint protege regra real?
- unique constraint substitui validação frágil?
- índice pode ser criado com segurança em produção?

---

### 6. Avaliar deploy e compatibilidade

Perguntar:

- aplicação antiga funciona com schema novo?
- aplicação nova funciona com schema antigo durante deploy?
- migration é backward-compatible?
- precisa de deploy em duas fases?
- há risco de downtime?

---

### 7. Validar

Possíveis validações:

```bash
dotnet ef migrations list
dotnet ef migrations add <Name>
dotnet ef database update
dotnet test
```

Mas comandos devem seguir authority source local.

Quando não aplicar em banco real, registrar lacuna.

---

## Output esperado

```md
# EF Core Migrations Safety Review

## Mudança persistida
<tabela, entidade, coluna, relacionamento, índice ou query>

## Tipo de alteração
<add | remove | rename | alter | index | constraint | seed | query>

## Risco de dados existentes
<baixo | moderado | alto | incerto>

## Migration
<gerada | não gerada | não aplicável>

## Pontos de atenção na migration
- <drop/rename/default/backfill/lock/etc>

## Query/tracking
<análise se aplicável>

## Compatibilidade de deploy
<compatível | exige cuidado | incerta>

## Validação recomendada
- <validação 1>
- <validação 2>

## Veredito
<suficiente | ajustar | escalar>

## Risco residual
<risco que permanece>
```

---

## Checklist de qualidade

Antes de aceitar, verificar:

- há schema change?
- dado existente foi considerado?
- migration foi revisada manualmente?
- há operação destrutiva?
- rename virou drop/create?
- nulabilidade/default fazem sentido?
- índice/constraint são justificados?
- query evita N+1?
- tracking está adequado?
- deploy compatibility foi considerada?
- rollback/Down foi avaliado?
- validação foi registrada?

---

## Critérios de escalonamento

Escalar quando:

- migration for destrutiva;
- houver produção ou dado real;
- alteração exigir backfill;
- houver mudança de tipo arriscada;
- índice puder gerar lock relevante;
- deploy precisar de duas fases;
- relação entre entidades alterar boundary;
- query crítica tiver risco de performance;
- não houver ambiente seguro para validar.

---

## Anti-patterns

Evitar:

- aceitar migration auto-gerada sem ler;
- dropar coluna sem plano;
- alterar nulabilidade sem considerar dados;
- usar migration para corrigir dado sem estratégia;
- carregar entidade inteira para projection simples;
- lazy loading invisível;
- include para tudo;
- query dentro de loop;
- transação com API externa;
- aplicar migration real sem autorização.

---

## Declaração operacional curta

EF Core facilita mudar schema, mas não remove risco.  
Toda migration precisa ser lida como mudança real de dados, compatibilidade e operação.