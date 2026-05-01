# Skill — Docs Research Operator

## Finalidade

Esta skill orienta pesquisa em documentação oficial ou fontes técnicas confiáveis quando o conhecimento local ou do modelo puder estar incompleto, desatualizado ou ambíguo.

Seu papel é permitir que o agente consulte documentação externa sem despejar ruído no contexto, sem aceitar fonte fraca e sem contrariar a realidade do workspace.

---

## Quando usar

Use esta skill quando a task envolver:

- API, SDK, CLI ou framework com comportamento específico;
- versão recente;
- dúvida sobre configuração;
- erro de ferramenta;
- recurso cloud;
- package novo;
- breaking change;
- documentação local insuficiente;
- conhecimento do modelo possivelmente desatualizado.

---

## Quando não usar

Não use esta skill quando:

- a resposta está clara em authority source local;
- a consulta externa não mudará decisão;
- a fonte disponível é fraca;
- o problema é específico do workspace e não da ferramenta;
- a pesquisa viraria navegação genérica.

---

## Tese central

Documentação externa informa possibilidade.  
Workspace local define realidade.

Fonte externa ajuda quando responde pergunta concreta e aplicável à versão/stack em uso.

---

## Método

### 1. Formular pergunta de pesquisa

Antes de pesquisar, declarar:

- qual comportamento precisa ser confirmado;
- qual versão/ferramenta está em jogo;
- por que a dúvida importa;
- que decisão será afetada.

---

### 2. Priorizar fontes

Preferir:

- documentação oficial;
- release notes;
- changelog oficial;
- repositório oficial;
- specs;
- páginas de cloud provider;
- docs de package manager;
- issues oficiais quando docs forem insuficientes.

Evitar:

- blog genérico;
- snippet sem contexto;
- resposta antiga de fórum;
- tutorial sem versão;
- conteúdo de baixa confiança.

---

### 3. Confirmar versão

Verificar:

- versão do projeto;
- versão da lib;
- versão da CLI;
- versão do runtime;
- data da documentação;
- compatibilidade.

---

### 4. Extrair síntese mínima

Registrar apenas:

- achado relevante;
- citação ou referência;
- versão;
- limitação;
- implicação prática.

Não colar documentação longa sem necessidade.

---

### 5. Comparar com workspace

Antes de aplicar:

- verificar config local;
- verificar package/version;
- verificar padrão do projeto;
- verificar comandos locais;
- verificar constraints.

---

### 6. Registrar lacunas

Se a fonte não responder completamente, registrar incerteza em vez de inventar.

---

## Output esperado

```md
# Docs Research Note

## Pergunta
<o que precisava ser confirmado>

## Ferramenta/versão
<framework, SDK, CLI, cloud resource ou lib>

## Fontes consultadas
- <fonte 1>
- <fonte 2>

## Achados
- <achado 1>
- <achado 2>

## Aplicabilidade ao workspace
<como se conecta à versão/config local>

## Lacunas
- <lacuna 1>
- <lacuna 2>

## Implicação para a task
<ação ou decisão recomendada>

## Veredito
<suficiente | investigar mais | escalar>
```

---

## Checklist de qualidade

Antes de concluir, verificar:

- a pergunta estava clara?
- fonte oficial foi priorizada?
- versão foi considerada?
- achado se aplica ao workspace?
- docs não contradizem authority source local?
- síntese é suficiente e não inflada?
- lacunas foram declaradas?
- não houve uso de fonte fraca como certeza?

---

## Critérios de escalonamento

Escalar quando:

- docs forem contraditórias;
- versão local não for clara;
- mudança tiver risco R3/R4;
- comportamento documentado afetar arquitetura;
- fonte externa contrariar prática local;
- decisão envolver segurança, produção ou dados.

---

## Anti-patterns

Evitar:

- pesquisar sem pergunta;
- aceitar primeiro resultado;
- usar tutorial como fonte canônica;
- ignorar versão;
- copiar docs inteiras;
- aplicar exemplo oficial sem adaptar ao projeto;
- usar fonte externa para atropelar authority source local;
- esconder incerteza quando docs não forem conclusivas.

---

## Declaração operacional curta

Pesquisa boa responde pergunta concreta com fonte confiável, versão correta e aplicação clara ao workspace.