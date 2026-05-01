# Skill — Doc Gardener

## Finalidade

Esta skill orienta a manutenção de documentação viva: README, guides, authority sources, ADRs, templates, state files, comandos e notas operacionais.

Seu papel é impedir que documentação vire decoração, fique desatualizada ou contradiga o código e o fluxo real.

---

## Quando usar

Use esta skill quando:

- uma task alterar comportamento documentado;
- comandos locais mudarem;
- arquitetura mudar;
- boundary mudar;
- dependência ou integração nova entrar;
- `PROJECT_STATE.md` precisar ser atualizado;
- README estiver desatualizado;
- ADR precisar ser criado ou revisado;
- authority source estiver incompleta;
- documentação contradizer o repositório;
- uma lacuna documental atrapalhar execução ou review.

---

## Quando não usar

Não use esta skill quando:

- a task não altera verdade durável;
- documentação não é impactada;
- a atualização geraria ruído;
- a task é pequena e o Completion Packet basta;
- a mudança documental seria apenas ornamental.

---

## Tese central

Documentação boa é parte do sistema.

Ela deve ajudar humano, Core Architect e agente futuro a entenderem a realidade atual sem depender de conversa antiga.

Documentação ruim aumenta entropia.

---

## Método

### 1. Identificar documento impactado

Verificar se a mudança afeta:

- README;
- WORKSPACE_GUIDE;
- PROJECT_CONTEXT;
- AUTHORITY_SOURCES;
- LOCAL_COMMANDS;
- PROJECT_STATE;
- DONE_CRITERIA;
- OPERATIONAL_REALITY;
- ADR;
- templates;
- docs de módulo;
- comments relevantes.

---

### 2. Determinar se a informação é durável

Atualizar documentação apenas se a informação precisar sobreviver à task.

Perguntar:

- isso muda como operar o projeto?
- muda como evoluir?
- muda arquitetura?
- muda comando?
- muda risco?
- evita reinvestigação futura?
- representa decisão?

---

### 3. Escolher forma correta

Nem tudo vai no mesmo lugar.

- decisão arquitetural relevante → ADR;
- estado técnico atual → PROJECT_STATE;
- comandos reais → LOCAL_COMMANDS;
- operational reality → OPERATIONAL_REALITY;
- guia de onboarding → README/WORKSPACE_GUIDE;
- critério de pronto → DONE_CRITERIA;
- fonte de autoridade → AUTHORITY_SOURCES.

---

### 4. Evitar duplicação

Antes de escrever, verificar:

- já existe documento para isso?
- a informação deve ser linkada em vez de duplicada?
- a duplicação criaria drift futuro?
- há fonte canônica mais apropriada?

---

### 5. Atualizar de forma mínima e causal

A documentação deve mudar na medida da task.

Evitar reescrever documento inteiro sem necessidade.

---

### 6. Verificar coerência

Depois de atualizar, verificar:

- a documentação não contradiz código;
- não contradiz outro documento;
- não registra intenção antiga como realidade;
- não mistura backlog com estado técnico;
- não usa linguagem vaga.

---

## Output esperado

```md
# Documentation Maintenance Note

## Mudança que motivou atualização
<o que mudou ou foi descoberto>

## Documentos impactados
- <documento 1>
- <documento 2>

## Informação durável
<sim | não | incerto>

## Local recomendado
<README | PROJECT_STATE | ADR | LOCAL_COMMANDS | outro>

## Atualização proposta
<descrição curta>

## Risco de documentação
<drift, duplicação, lacuna ou obsolescência>

## Veredito
<atualizar agora | criar follow-up | não atualizar | escalar>
```

---

## Checklist de qualidade

Antes de encerrar, verificar:

- a informação precisa sobreviver?
- o documento correto foi escolhido?
- não houve duplicação desnecessária?
- a atualização é factual?
- comandos documentados são reais?
- state não virou changelog?
- board não virou documentação técnica?
- README não virou depósito de detalhes?
- ADR foi considerado quando houve decisão?

---

## Critérios de escalonamento

Escalar quando:

- documentos de autoridade se contradizem;
- a documentação exige decisão arquitetural;
- não está claro onde registrar;
- a atualização pode mudar entendimento do projeto;
- uma decisão precisa de ADR;
- PROJECT_STATE está obsoleto demais;
- a documentação local conflita com código.

---

## Anti-patterns

Evitar:

- documentação ornamental;
- atualizar docs sem mudança real;
- copiar Completion Packet inteiro para PROJECT_STATE;
- colocar backlog em PROJECT_STATE;
- deixar decisão arquitetural em comentário solto;
- registrar intenção futura como estado atual;
- duplicar comando em três lugares;
- README gigante com detalhe que pertence a guide local.

---

## Declaração operacional curta

Doc gardener mantém documentação viva, factual e útil.  
Documento bom reduz contexto futuro; documento ruim aumenta entropia.