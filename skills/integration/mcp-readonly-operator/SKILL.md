# Skill — MCP Read-Only Operator

## Finalidade

Esta skill orienta o uso de MCP em modo read-only.

Seu papel é permitir que o agente consulte fontes externas de contexto sem transformar integração em autonomia perigosa, escrita acidental, alteração de estado remoto ou substituição da verdade local do workspace.

---

## Quando usar

Use esta skill quando a task precisar consultar:

- GitHub;
- GitHub Projects;
- issues;
- PRs;
- documentação externa;
- cloud metadata;
- observabilidade;
- ferramentas conectadas via MCP;
- contexto externo que reduza incerteza.

---

## Quando não usar

Não use esta skill quando:

- a informação já estiver disponível no workspace;
- a consulta externa for curiosidade;
- a fonte não estiver registrada ou confiável;
- a operação exigir escrita;
- a task puder ser resolvida por authority sources locais;
- o uso de MCP aumentaria contexto sem melhorar decisão.

---

## Tese central

MCP read-only observa.  
Não age.

Integração externa deve reduzir incerteza, não ampliar autonomia do agente.

---

## Método

### 1. Definir pergunta externa

Antes de consultar qualquer MCP, declarar:

- que informação precisamos obter;
- por que ela importa;
- que decisão depende dela;
- qual fonte externa é apropriada;
- qual risco existe se a fonte estiver errada.

---

### 2. Confirmar modo read-only

A operação deve ser estritamente de leitura.

Permitido:

- listar;
- buscar;
- abrir;
- ler;
- consultar;
- inspecionar;
- resumir.

Proibido sem autorização explícita:

- criar;
- editar;
- deletar;
- mover;
- fechar;
- comentar;
- aplicar label;
- alterar status;
- disparar workflow;
- fazer deploy;
- modificar recurso externo.

---

### 3. Verificar confiança da integração

Antes de usar, consultar a política e o registro aplicável:

- MCP Policy;
- Trusted Integrations Policy;
- Trusted Integrations Registry.

Se a integração não for confiável, tratar resultado como experimental ou escalar.

---

### 4. Separar fonte externa de autoridade local

MCP pode informar contexto, mas não substitui automaticamente:

- código local;
- commands locais;
- `PROJECT_STATE.md`;
- ADRs;
- workspace guide;
- authority files.

Quando remoto e local divergirem, registrar divergência.

---

### 5. Capturar apenas o necessário

Evitar despejar grandes blocos externos no contexto.

Preferir:

- síntese factual;
- links ou referências;
- achados relevantes;
- lacunas;
- implicação para o plano.

---

### 6. Registrar evidência

Toda consulta MCP relevante deve indicar:

- fonte consultada;
- achado factual;
- limitação;
- impacto no plan, review ou handoff.

---

## Output esperado

```md
# MCP Read-Only Note

## Pergunta externa
<o que precisava ser consultado>

## Integração usada
<MCP/fonte>

## Modo
read-only

## Fontes consultadas
- <fonte 1>
- <fonte 2>

## Achados
- <achado 1>
- <achado 2>

## Limitações
- <limitação 1>
- <limitação 2>

## Implicação para a task
<como isso muda ou confirma o próximo passo>

## Veredito
<suficiente | investigar mais | escalar>
```

---

## Checklist de qualidade

Antes de concluir, verificar:

- a pergunta externa estava clara?
- a operação foi read-only?
- a integração é confiável ou experimental?
- a consulta reduziu incerteza?
- a fonte externa não substituiu verdade local indevidamente?
- achados foram separados de hipóteses?
- dados sensíveis foram evitados?
- o resultado foi registrado em artifact quando relevante?

---

## Critérios de escalonamento

Escalar quando:

- a operação exigiria escrita;
- a integração não for confiável;
- houver risco de produção, segredo ou dado sensível;
- fonte externa contradizer authority source local;
- o agente precisar decidir com base em contexto externo ambíguo;
- a consulta revelar risco R3/R4.

---

## Anti-patterns

Evitar:

- usar MCP para tudo;
- consultar externo antes de ler workspace;
- mover card ou issue sem autorização;
- comentar em PR automaticamente;
- tratar board como especificação técnica completa;
- despejar logs ou issues inteiras no contexto;
- usar integração sem registrar fonte;
- confundir “consigo acessar” com “devo agir”.

---

## Declaração operacional curta

MCP read-only serve para observar contexto externo com segurança.  
Ele informa a execução, mas não substitui autoridade local nem autorização humana.