# OpenCode MCP — Cloud Read-Only Inspection

## Finalidade

Este arquivo orienta o uso de MCP para inspeção cloud read-only no OpenCode.

A inspeção cloud serve para entender ambiente, recursos, metadata e configuração não sensível.

Ela não serve para corrigir ambiente diretamente.

---

## Modo permitido

```text
read-only
```

Operações permitidas:

```text
listar recursos
ler metadata
ler status
consultar runtime
consultar região
consultar plano/SKU
consultar health/status
consultar configuração não sensível
inspecionar topologia
consultar identidade sem segredo
```

Operações proibidas sem autorização explícita:

```text
criar recurso
alterar recurso
deletar recurso
reiniciar recurso
escalar recurso
aplicar deploy
alterar app settings
alterar secret
alterar IAM/RBAC
alterar firewall/rede
alterar storage
executar migration
rodar comando em produção
```

---

## Agente responsável

```text
adapters/opencode/agents/mcp-observer.md
```

Skills relacionadas:

```text
skills/integration/cloud-readonly-inspection/SKILL.md
skills/security/secrets-and-config-hygiene/SKILL.md
skills/stack/azure/azure-delivery-reviewer/SKILL.md
skills/stack/azure/azure-execution-model-review/SKILL.md
```

---

## Quando usar

Use quando a task precisar verificar:

- se um recurso existe;
- em qual ambiente está;
- qual runtime usa;
- qual região/plano;
- status operacional;
- metadata de deploy;
- configuração não sensível;
- identidade/managed identity sem segredos;
- possível drift entre IaC e cloud;
- topologia cloud em modo leitura.

---

## Quando não usar

Não use quando:

- a informação está no IaC local;
- a pergunta operacional não está clara;
- o ambiente pode ser produção sem necessidade;
- a consulta pode expor segredo;
- a próxima ação seria alteração de recurso;
- o agente não consegue garantir read-only.

---

## Pergunta obrigatória antes da consulta

Antes de inspecionar cloud, declarar:

```text
Qual recurso será consultado?
Qual ambiente?
Que dúvida operacional queremos responder?
Como a resposta afeta a task?
```

Ambiente incerto é risco.

---

## Proteção de produção

Se o ambiente for ou puder ser produção:

- limitar escopo;
- evitar qualquer mutação;
- não rodar comandos operacionais;
- não revelar segredos;
- registrar limitação;
- escalar se a próxima ação exigir alteração.

---

## Proteção de segredo

Não reproduzir:

```text
connection string
app secret
key
token
certificate
password
private endpoint secret
header sensível
valor de variável sensível
```

Permitido registrar:

```text
secret existe
secret ausente
config sensível presente
valor mascarado
```

Exemplo:

```text
DATABASE_URL: <secret-present-not-shown>
```

---

## IaC vs realidade

Quando houver IaC no repositório, diferenciar:

```text
estado declarado
estado real
drift possível
lacuna de validação
```

Não corrigir drift manualmente via MCP sem processo e autorização.

---

## Processo

### 1. Identificar ambiente

Registrar:

```text
local
dev
staging
prod
incerto
```

### 2. Identificar recurso

Registrar:

```text
resource group
subscription, se seguro e necessário
tipo de recurso
nome lógico
região
runtime
```

Não reproduzir identificadores sensíveis se houver risco.

### 3. Ler metadata mínima

Consultar apenas o necessário para responder a pergunta.

### 4. Comparar com authority sources

Comparar com:

```text
OPERATIONAL_REALITY.md
infra/IaC
README
PROJECT_STATE.md
pipeline
```

### 5. Registrar achados

Achados devem ser factuais e limitados.

---

## Output recomendado

```md
# Cloud Read-Only Inspection Note

## Pergunta operacional
<o que precisava ser verificado>

## Ambiente
<dev | staging | prod | incerto>

## Recursos consultados
- <recurso 1>
- <recurso 2>

## Achados
- <achado 1>
- <achado 2>

## Possível drift IaC/realidade
<nenhum | descrito | incerto>

## Dados sensíveis
<não acessados | mascarados | risco identificado>

## Implicação para a task
<como isso orienta plan, review, deploy ou escalonamento>

## Veredito
<suficiente | investigar mais | escalar>
```

---

## Escalonamento

Escalar quando:

- ambiente for produção;
- houver segredo;
- houver IAM/RBAC;
- houver firewall/rede;
- houver drift relevante;
- houver dado real;
- houver necessidade de restart, scale, deploy ou config change;
- inspeção revelar risco operacional alto.

---

## Anti-patterns

Evitar:

- “só ajustar rapidinho” no cloud;
- copiar secret para artifact;
- listar recursos sem pergunta;
- corrigir drift manualmente;
- tocar produção em diagnóstico;
- alterar config para testar hipótese;
- usar cloud real como laboratório;
- ignorar IaC local.

---

## Declaração operacional curta

Cloud read-only observa ambiente.  
Se a próxima ação altera recurso, já não é inspeção: é escalonamento.