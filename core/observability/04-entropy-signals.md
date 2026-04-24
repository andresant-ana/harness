# Sinais de Entropia

## Finalidade

Este documento define sinais de degradação técnica, arquitetural, documental e operacional que o harness deve observar ao longo do tempo.

Seu papel é ajudar humano, Core Architect e agentes a detectar cedo quando o sistema está ficando mais confuso, mais frágil ou mais difícil de governar.

---

## Tese central

Entropia raramente aparece como grande desastre imediato.  
Ela aparece como pequenas degradações acumuladas.

O harness deve reconhecer sinais de:

- AI slop;
- abstraction bloat;
- drift arquitetural;
- documentação vencida;
- skill bloat;
- context bloat;
- dependências desnecessárias;
- perda de fronteira entre camadas;
- perda de coerência entre artifacts.

---

## Categorias de entropia

1. entropia de código;
2. entropia arquitetural;
3. entropia documental;
4. entropia operacional;
5. entropia de contexto;
6. entropia de agentes;
7. entropia de skills;
8. entropia de adapter;
9. entropia de governança.

---

## Entropia de código

### Sinais

- duplicação de lógica;
- helpers redundantes;
- funções genéricas demais;
- nomes inconsistentes;
- tratamento de erro divergente;
- arquivos longos sem responsabilidade clara;
- lógica espalhada por conveniência;
- teste acoplado demais à implementação.

### Pergunta diagnóstica

A mudança tornou o código mais navegável ou apenas adicionou mais superfície?

---

## Entropia arquitetural

### Sinais

- boundaries de módulo quebrados;
- imports indevidos entre contextos;
- camada nova sem dor real;
- interface sem variação concreta;
- DTO, mapper ou adapter ornamental;
- feature simples tocando muitos arquivos;
- microdecisões criando arquitetura paralela;
- padrão usado por prestígio, não por necessidade.

### Pergunta diagnóstica

A arquitetura ficou mais clara, ou mais cerimonial?

---

## Entropia documental

### Sinais

- README desatualizado;
- `PROJECT_STATE.md` contradiz código;
- authority commands não funcionam;
- ADRs não refletem decisão real;
- documentação explica intenção antiga;
- risks conhecidos não estão registrados;
- templates copiados sem adaptação;
- completion packets não deixam continuidade.

### Pergunta diagnóstica

A documentação ainda representa a realidade ou virou decoração?

---

## Entropia operacional

### Sinais

- comandos locais inconsistentes;
- build/test/lint não documentados;
- pipeline divergente do local;
- health checks frágeis;
- observabilidade insuficiente;
- logs ruidosos ou sensíveis;
- deploy depende de conhecimento tribal;
- ambiente local funciona por acaso.

### Pergunta diagnóstica

O sistema pode ser operado por alguém que não estava na conversa original?

---

## Entropia de contexto

### Sinais

- sessões longas demais;
- transcript substituindo artifacts;
- contexto global inchado;
- project state ausente;
- skills demais chamadas por insegurança;
- documentos duplicados em prompt;
- Core Architect recebendo ruído em vez de decisão organizada.

### Pergunta diagnóstica

O contexto está ajudando a decisão atual ou soterrando o problema?

---

## Entropia de agentes

### Sinais

- agentes com papéis sobrepostos;
- implementer decidindo arquitetura;
- reviewer implementando;
- planner sem discovery;
- architect-critic opinando em detalhe tático;
- mcp-observer substituindo discovery local;
- delivery-prep escondendo lacunas.

### Pergunta diagnóstica

Cada agente está fazendo o papel certo?

---

## Entropia de skills

### Sinais

- skill para problema raro;
- skill que só repete protocol;
- skill sem output esperado;
- skill sem gatilho claro;
- skills duplicadas;
- skill teórica demais;
- skill chamada em toda task sem necessidade.

### Pergunta diagnóstica

A skill reduz erro recorrente ou apenas aumenta contexto?

---

## Entropia de adapter

### Sinais

- regra canônica vivendo apenas no OpenCode;
- adapter redefinindo doutrina;
- config de runtime virando fonte de verdade global;
- commands específicos vazando para o núcleo;
- AGENTS.md contradizindo constitution;
- runtime escolhido moldando demais o sistema.

### Pergunta diagnóstica

O adapter está traduzindo o núcleo ou substituindo o núcleo?

---

## Entropia de governança

### Sinais

- mudanças estruturais sem changelog;
- arquivos novos sem motivo claro;
- policies criadas para caso único;
- experimentos não registrados;
- integrações confiáveis sem registro;
- depreciação inexistente;
- backlog sem critério.

### Pergunta diagnóstica

A engenharia está evoluindo com controle ou acumulando decisões soltas?

---

## Sinais vermelhos

Sinais de alerta alto:

- segredo apareceu em diff;
- produção foi tocada sem autorização;
- task R3 executada como R1;
- review aprovou sem evidência;
- agente adicionou dependência por tentativa;
- abstração nova sem dor real;
- board virou documentação técnica;
- `PROJECT_STATE.md` ficou obsoleto;
- adapter contradiz núcleo;
- skill bloat começou a degradar contexto.

---

## Sinais amarelos

Sinais de atenção:

- handoff genérico;
- plan pouco específico;
- discovery superficial;
- lacunas mal descritas;
- documentação local atrasada;
- diff maior que o problema;
- contexto longo demais;
- review sem veredito forte;
- state update esquecido.

---

## Como reagir à entropia

### Entropia leve

Ações possíveis:
- registrar no handoff;
- criar follow-up;
- ajustar documentação;
- melhorar checklist.

### Entropia moderada

Ações possíveis:
- review específico;
- skill de hygiene;
- Project State Entry;
- refactor delimitado;
- atualização de authority source.

### Entropia alta

Ações possíveis:
- bloquear mudança;
- escalar para Core Architect;
- criar ADR;
- rever protocol/policy;
- abrir task de hardening;
- reavaliar adapter ou skill.

---

## Relação com metrics

Sinais de entropia devem alimentar:

- entropy delta;
- documentation drift;
- missed escalation;
- review catch rate;
- context load;
- project state usefulness;
- skill bloat indicator.

---

## Relação com review

Review deve tratar entropia como qualidade real, não como gosto pessoal.

Perguntas mínimas:

- o diff tem causalidade?
- a complexidade paga aluguel?
- a documentação continua verdadeira?
- a mudança respeita boundaries?
- isso ajuda o agente futuro?

---

## Relação com governance

Quando o mesmo sinal de entropia aparece repetidamente, ele deve alimentar governance:

- backlog pós-piloto;
- revisão de skill;
- ajuste de policy;
- depreciação;
- hardening;
- novo replay scenario.

---

## Declaração operacional curta

Entropia é o custo invisível de pequenas permissões ruins.  
O harness deve detectar cedo, reagir proporcionalmente e impedir degradação acumulada.