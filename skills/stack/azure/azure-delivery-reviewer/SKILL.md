# Skill — Azure Delivery Reviewer

## Finalidade

Esta skill orienta a revisão de entrega, configuração e publicação de workloads na Azure.

Seu papel é impedir que o agente trate deploy como simples etapa final, ignorando ambiente, app settings, secrets, managed identity, pipeline, observabilidade, rollback, configuração por ambiente e risco de publicação.

Esta skill não substitui `cloud-runtime-choice-review`, `iac-security-review`, `terraform-or-bicep-delivery` ou `ci-cd-pipeline-review`.  
Ela foca a entrega em Azure como superfície específica da stack principal.

---

## Quando usar

Use esta skill quando a task tocar:

- deploy na Azure;
- Azure App Service;
- Azure Container Apps;
- Azure Functions;
- AKS;
- Azure Static Web Apps;
- app settings;
- connection strings;
- managed identity;
- Key Vault;
- deployment slots;
- pipeline de publicação;
- environment variables;
- observabilidade no Azure Monitor/Application Insights;
- configuração de ambiente;
- publicação de frontend/backend;
- runtime config;
- rollback;
- risco de ambiente.

---

## Quando não usar

Não use esta skill quando:

- a task não envolve Azure;
- a alteração é puramente local;
- a task é apenas escolha de runtime, sem entrega;
- a revisão já está coberta por IaC/pipeline/security sem especificidade Azure;
- a análise seria especulativa sem recurso ou ambiente concreto.

---

## Tese central

Entrega em cloud é parte da engenharia, não etapa operacional menor.

Uma aplicação bem implementada pode falhar por:

- app setting errado;
- segredo mal configurado;
- identity sem permissão;
- ambiente confundido;
- pipeline publicando artefato errado;
- health check ruim;
- observabilidade ausente;
- rollback impossível;
- configuração local divergente de produção.

Na Azure, a entrega precisa conectar código, configuração, identidade, runtime, pipeline e observabilidade.

---

## Método

### 1. Identificar workload e ambiente

Registrar:

- aplicação;
- tipo de recurso Azure;
- ambiente;
- região;
- subscription/resource group, se conhecido;
- pipeline ou método de deploy;
- se há produção ou dado real.

Ambiente incerto é risco.

---

### 2. Revisar artefato de entrega

Perguntar:

- o que será publicado?
- build output está correto?
- imagem/container está correto?
- artifact é versionado?
- pipeline usa branch/tag correta?
- há diferença entre build local e build CI?
- frontend e backend usam configurações corretas?

---

### 3. Revisar app settings e configuração

Verificar:

- configurações por ambiente;
- connection strings;
- feature flags;
- endpoints externos;
- CORS;
- URLs públicas;
- variáveis obrigatórias;
- defaults perigosos;
- fallback para produção;
- valores sensíveis.

Não reproduzir valores de segredo.

---

### 4. Revisar identidade e acesso

Avaliar:

- managed identity;
- service principal;
- RBAC;
- acesso a Key Vault;
- acesso a Storage;
- acesso a banco;
- acesso a filas;
- permissões mínimas;
- credenciais estáticas.

Preferir identidade gerenciada quando apropriado.

---

### 5. Revisar observabilidade

Verificar:

- Application Insights;
- Azure Monitor;
- logs estruturados;
- health checks;
- métricas de erro/latência;
- correlation id;
- alerts, se aplicável;
- diagnóstico pós-deploy.

Entrega sem sinal operacional é frágil.

---

### 6. Revisar estratégia de publicação

Perguntar:

- há slot?
- há blue/green ou canary?
- deploy é direto?
- há rollback?
- há migração de banco acoplada?
- há downtime esperado?
- deploy pode ser reexecutado?
- pipeline tem aprovação para ambiente sensível?

---

### 7. Revisar segurança de entrega

Verificar:

- secrets não aparecem em logs;
- pipeline não imprime app settings sensíveis;
- permissões de deploy são mínimas;
- ambiente de produção tem gate;
- artefato não contém segredo;
- recurso não fica público por acidente.

---

### 8. Validar pós-deploy

Definir validações proporcionais:

- health endpoint;
- smoke test;
- logs de startup;
- métricas iniciais;
- endpoint crítico;
- frontend carregando config correta;
- conexão com banco/fila;
- ausência de erro 5xx.

---

## Output esperado

```md
# Azure Delivery Review

## Workload
<API | frontend | worker | function | container | outro>

## Recurso Azure
<App Service | Container Apps | Functions | AKS | Static Web Apps | outro>

## Ambiente
<dev | staging | prod | incerto>

## Artefato de entrega
<build output, container image, package, artifact ou pipeline>

## Configuração
<app settings, env vars, endpoints, CORS, feature flags, lacunas>

## Identidade e acesso
<managed identity, RBAC, Key Vault, banco, storage, filas>

## Observabilidade
<logs, metrics, Application Insights, health, lacunas>

## Estratégia de deploy/rollback
<direto | slot | staged | rollback | incerto>

## Riscos
- <risco 1>
- <risco 2>

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

Antes de aceitar entrega Azure, verificar:

- ambiente está claro?
- recurso Azure está identificado?
- artefato correto será publicado?
- pipeline/branch/tag estão corretos?
- app settings obrigatórios foram considerados?
- secrets não serão expostos?
- managed identity/RBAC seguem menor privilégio?
- Key Vault foi considerado quando há segredo?
- observabilidade existe?
- health check faz sentido?
- há rollback ou mitigação?
- validação pós-deploy está definida?
- produção exige autorização explícita?

---

## Critérios de escalonamento

Escalar quando:

- ambiente for produção;
- houver segredo real;
- houver mudança de RBAC/identity;
- houver mudança de pipeline de deploy;
- houver alteração em app settings sensíveis;
- deploy puder causar indisponibilidade;
- rollback for incerto;
- houver migration de banco junto com deploy;
- observabilidade mínima estiver ausente;
- recurso público ou CORS estiverem em discussão.

---

## Anti-patterns

Evitar:

- deploy direto em produção sem gate;
- app setting sensível em log;
- confundir config local com config cloud;
- service principal amplo por conveniência;
- publicar artefato de branch errada;
- usar fallback para produção;
- ausência de health check;
- rollback tratado como “é só publicar de novo”;
- pipeline com permissão maior que o necessário;
- validar deploy apenas abrindo home page.

---

## Relação com outras skills

Use junto com:

- `cloud-runtime-choice-review`, se o runtime ainda estiver em decisão;
- `azure-execution-model-review`, se o modelo Azure estiver em discussão;
- `iac-security-review`, se houver infraestrutura/config como código;
- `terraform-or-bicep-delivery`, se a entrega envolver IaC;
- `ci-cd-pipeline-review`, se houver pipeline;
- `secrets-and-config-hygiene`, se houver app settings sensíveis;
- `observability-first`, se a entrega alterar sinal operacional.

---

## Declaração operacional curta

Entrega Azure segura conecta artefato, ambiente, configuração, identidade, observabilidade e rollback.  
Deploy sem revisão operacional é chute em cloud.