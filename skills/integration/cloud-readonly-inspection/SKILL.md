# Skill — Cloud Read-Only Inspection

## Finalidade

Esta skill orienta inspeção read-only de recursos cloud, configurações, metadata, runtime, rede, permissões e ambiente.

Seu papel é permitir diagnóstico e entendimento operacional sem criar, alterar, deletar, publicar, reiniciar ou modificar recursos.

---

## Quando usar

Use esta skill quando a task precisar consultar:

- recursos cloud;
- App Service;
- Container Apps;
- Functions;
- AKS;
- storage;
- database;
- networking;
- identities;
- app settings sem revelar valores;
- regiões;
- planos;
- métricas básicas;
- estado de deploy;
- configuração operacional.

---

## Quando não usar

Não use esta skill quando:

- a informação está no IaC local;
- a consulta não tem pergunta operacional clara;
- o acesso envolver produção sem necessidade;
- a operação exigiria escrita;
- o agente não consegue garantir modo read-only;
- a consulta poderia expor segredo.

---

## Tese central

Cloud read-only serve para entender o ambiente.  
Não serve para corrigir ambiente diretamente.

Ambiente cloud pode conter produção, dados reais, segredos, custo e blast radius.  
Mesmo leitura deve ser feita com escopo e cuidado.

---

## Método

### 1. Definir pergunta operacional

Declarar:

- que recurso será inspecionado;
- qual ambiente;
- que dúvida precisa ser respondida;
- como a resposta afetará plan, review ou diagnóstico.

---

### 2. Confirmar modo read-only

Permitido:

- listar recurso;
- ler metadata;
- consultar status;
- ler configuração não sensível;
- inspecionar topologia;
- consultar health/status;
- verificar região/plano/runtime.

Proibido:

- criar;
- atualizar;
- deletar;
- reiniciar;
- escalar;
- aplicar deploy;
- alterar config;
- alterar secret;
- alterar IAM/RBAC;
- alterar network/firewall.

---

### 3. Evitar segredo

Não reproduzir:

- connection string;
- app secret;
- key;
- token;
- certificate;
- password;
- private endpoint secret;
- header sensível.

Se necessário, registrar apenas presença ou referência mascarada.

---

### 4. Separar IaC e estado real

Comparar quando útil:

- IaC esperado;
- estado real;
- drift;
- divergência;
- lacuna.

Não corrigir drift sem processo de IaC.

---

### 5. Registrar achados

Achados devem ser factuais:

- recurso existe/não existe;
- configuração presente/ausente;
- ambiente;
- status;
- região;
- runtime;
- divergência;
- risco.

---

## Output esperado

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
<como isso orienta a decisão>

## Veredito
<suficiente | investigar mais | escalar>
```

---

## Checklist de qualidade

Antes de concluir, verificar:

- ambiente foi identificado?
- operação foi read-only?
- recurso certo foi consultado?
- nenhum segredo foi reproduzido?
- produção foi tratada com cautela?
- IaC e estado real foram diferenciados?
- achado foi registrado como fato, não suposição?
- próxima ação não exige escrita sem autorização?

---

## Critérios de escalonamento

Escalar quando:

- ambiente for produção;
- houver segredo;
- houver IAM/RBAC;
- houver rede/firewall;
- houver drift significativo;
- houver dado real;
- houver necessidade de restart, scale, deploy ou config change;
- a inspeção revelar risco operacional alto.

---

## Anti-patterns

Evitar:

- “só ajustar rapidinho” no cloud;
- copiar secrets para artifact;
- listar recursos sem pergunta;
- confundir portal/cloud atual com IaC desejado;
- corrigir drift manualmente;
- tocar produção em modo diagnóstico;
- alterar config para testar hipótese;
- usar cloud como fonte única ignorando repositório.

---

## Declaração operacional curta

Cloud read-only observa ambiente com cautela.  
Se a próxima ação altera recurso, não é mais inspeção: é escalonamento.