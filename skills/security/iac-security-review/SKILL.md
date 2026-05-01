# Skill — IaC Security Review

## Finalidade

Esta skill orienta a revisão de segurança em infraestrutura como código, cloud configuration, permissões, redes, secrets, storage, identidade gerenciada e blast radius.

Seu papel é impedir que o agente crie ou altere infraestrutura com permissões amplas, exposição pública indevida, segredos inseguros ou configuração operacional frágil.

---

## Quando usar

Use esta skill quando a task tocar:

- Terraform;
- Bicep;
- ARM templates;
- GitHub Actions;
- Azure resources;
- cloud config;
- IAM/RBAC;
- managed identity;
- service principal;
- storage;
- network rules;
- firewall;
- secret store;
- container registry;
- app settings;
- database config;
- public endpoint;
- CI/CD permissions.

---

## Quando não usar

Não use esta skill quando:

- não houver IaC, cloud ou config operacional;
- a task for puramente local;
- a análise já estiver coberta por policy mais específica;
- a mudança não alterar superfície de infraestrutura.

---

## Tese central

Infraestrutura define blast radius.

Um erro em IaC pode expor dados, ampliar privilégio, abrir rede, vazar segredo ou gerar custo real.

Cloud config deve ser tratada como código sensível.

---

## Método

### 1. Identificar recurso e ambiente

Registrar:

- recurso criado/alterado;
- ambiente;
- região;
- escopo;
- subscription/project;
- runtime;
- quem consome;
- se há produção ou staging sensível.

---

### 2. Avaliar exposição de rede

Perguntar:

- recurso é público?
- deveria ser público?
- há firewall?
- há private endpoint?
- há allowlist?
- há CORS?
- há porta aberta?
- há acesso administrativo exposto?

---

### 3. Avaliar identidade e permissão

Verificar:

- princípio do menor privilégio;
- managed identity;
- roles atribuídas;
- escopo da role;
- permissões wildcard;
- service principal;
- credencial estática;
- acesso de CI/CD.

---

### 4. Avaliar segredos e configuração

Perguntar:

- segredo está em IaC?
- valor sensível está em state?
- app setting contém secret?
- secret store é usado?
- outputs expõem segredo?
- logs/pipeline imprimem valor?

---

### 5. Avaliar dados e storage

Verificar:

- storage público;
- encryption;
- backup;
- retention;
- deletion protection;
- acesso anônimo;
- connection string;
- firewall;
- dados sensíveis.

---

### 6. Avaliar operação

Perguntar:

- há observabilidade?
- há tags?
- há custo esperado?
- há autoscaling?
- há health checks?
- há rollback?
- há drift?
- há diferença entre local/staging/prod?

---

### 7. Definir validação

Recomendar:

- plan/diff de IaC;
- policy check;
- secret scan;
- revisão de permissões;
- revisão de outputs;
- revisão de network exposure;
- validação manual antes de apply/deploy.

---

## Output esperado

```md
# IaC Security Review

## Recurso/alteração analisada
<recurso, módulo IaC, pipeline ou config>

## Ambiente
<local | dev | staging | prod | incerto>

## Exposição de rede
<privado | público | restrito | incerto>

## Identidade e permissões
<análise de menor privilégio>

## Segredos/configuração
<análise sem revelar valores>

## Dados/storage
<análise curta>

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

Antes de aceitar, verificar:

- ambiente está claro?
- recurso público é realmente necessário?
- permissões seguem menor privilégio?
- não há wildcard perigoso?
- segredo não está hardcoded?
- outputs não expõem segredo?
- state não contém valor sensível sem controle?
- storage não está público por acidente?
- CI/CD tem permissão mínima?
- apply/deploy não será feito sem autorização?

---

## Critérios de escalonamento

Escalar quando:

- tocar produção;
- tocar segredo;
- tocar IAM/RBAC;
- abrir recurso publicamente;
- alterar firewall/rede;
- alterar banco/storage com dados reais;
- executar apply/deploy;
- houver risco de custo ou indisponibilidade;
- houver dúvida sobre blast radius.

---

## Anti-patterns

Evitar:

- `Owner`/`Contributor` amplo por conveniência;
- storage público sem justificativa;
- segredo em variável de pipeline impressa;
- output de secret;
- firewall aberto para `0.0.0.0/0`;
- apply automático sem revisão;
- usar credencial estática quando managed identity basta;
- misturar prod e dev;
- ignorar state sensível.

---

## Declaração operacional curta

IaC é código com impacto real.  
Toda mudança de infraestrutura precisa considerar permissão, exposição, segredo, ambiente e blast radius.