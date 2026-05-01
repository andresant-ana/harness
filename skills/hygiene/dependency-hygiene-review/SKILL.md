# Skill — Dependency Hygiene Review

## Finalidade

Esta skill orienta a revisão de higiene de dependências já existentes no projeto.

Seu papel é identificar dependências não usadas, redundantes, arriscadas, desatualizadas, mal justificadas ou que poderiam ser substituídas por capacidades já presentes no projeto.

Esta skill é diferente de `dependency-and-supply-chain-review`: aquela avalia entrada ou alteração de dependência; esta avalia saúde e necessidade do conjunto existente.

---

## Quando usar

Use esta skill quando houver:

- suspeita de dependência não usada;
- dependência duplicando outra;
- pacote antigo sem manutenção;
- dependência adicionada por tentativa;
- lockfile grande ou confuso;
- alerta de vulnerabilidade;
- bundle/runtime inflado;
- build lento por tooling desnecessário;
- dependência transitiva problemática;
- mudança que revela que pacote não é mais necessário.

---

## Quando não usar

Não use esta skill quando:

- a task não envolve dependências;
- a revisão viraria auditoria ampla sem motivo;
- a dependência acabou de ser analisada por supply chain review;
- não houver evidência de ruído, risco ou custo.

---

## Tese central

Dependência que não paga aluguel vira entropia.

Mesmo dependências legítimas em algum momento podem perder utilidade, ficar inseguras, duplicar capacidades ou aumentar custo de manutenção.

---

## Método

### 1. Definir escopo da revisão

Escolher se a revisão cobre:

- uma dependência específica;
- uma família de dependências;
- dependências de runtime;
- dev dependencies;
- lockfile;
- package manager;
- container base;
- CI tooling.

Evitar auditoria ampla sem pergunta.

---

### 2. Identificar uso real

Verificar:

- imports;
- chamadas;
- configs;
- scripts;
- build pipeline;
- runtime;
- testes;
- documentação;
- lockfile.

Diferenciar “não encontrei uso rápido” de “não é usada”.

---

### 3. Avaliar redundância

Perguntar:

- outra dependência já faz isso?
- recurso nativo da stack já faz isso?
- o projeto tem helper próprio?
- há duas bibliotecas para mesma função?
- uma dependência existe apenas por legado?

---

### 4. Avaliar risco

Considerar:

- manutenção;
- vulnerabilidades;
- licença;
- permissões;
- scripts;
- transitive dependencies;
- impacto em bundle;
- impacto em cold start;
- impacto em build/deploy.

---

### 5. Avaliar remoção

Antes de remover, perguntar:

- há cobertura de teste?
- a remoção quebra build?
- há uso dinâmico?
- há uso em config?
- há uso em CI?
- há documentação que precisa mudar?
- há lockfile a atualizar?

---

### 6. Recomendar ação

Ações possíveis:

- manter;
- atualizar;
- remover;
- substituir;
- investigar mais;
- registrar follow-up;
- escalar por risco.

---

## Output esperado

```md
# Dependency Hygiene Review

## Escopo
<dependência, grupo, runtime/dev, lockfile ou tooling>

## Uso encontrado
- <uso 1>
- <uso 2>

## Redundância
<sim | não | incerto>

## Riscos
- <risco 1>
- <risco 2>

## Ação recomendada
<manter | atualizar | remover | substituir | investigar | escalar>

## Validação necessária
- <build>
- <test>
- <lockfile review>
- <runtime check>

## Risco residual
<risco que permanece>
```

---

## Checklist de qualidade

Antes de recomendar remoção ou alteração, verificar:

- o escopo está claro?
- uso real foi procurado?
- uso dinâmico foi considerado?
- scripts e CI foram considerados?
- lockfile foi considerado?
- alternativa existe?
- risco de supply chain foi avaliado?
- validação pós-mudança está clara?
- a ação cabe no escopo atual?

---

## Critérios de escalonamento

Escalar quando:

- a dependência for crítica;
- houver vulnerabilidade alta;
- houver licença incerta;
- a remoção puder afetar runtime;
- a dependência tocar auth, crypto, dados ou segurança;
- houver dúvida sobre substituição;
- a mudança exigir refactor amplo.

---

## Anti-patterns

Evitar:

- remover dependência só porque não apareceu no primeiro grep;
- atualizar tudo sem changelog;
- ignorar lockfile;
- ignorar dev dependencies;
- tratar dependência transitiva como irrelevante;
- fazer limpeza ampla dentro de feature;
- substituir dependência por helper frágil;
- manter pacote “porque sempre esteve aí”.

---

## Declaração operacional curta

Higiene de dependência pergunta se o pacote ainda paga aluguel.  
Se não paga, deve ser removido, substituído ou registrado como dívida.