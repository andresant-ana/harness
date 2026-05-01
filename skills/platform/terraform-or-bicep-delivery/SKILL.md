# Skill — Terraform or Bicep Delivery

## Finalidade

Esta skill orienta a entrega segura e revisável de infraestrutura como código usando Terraform, Bicep ou modelos equivalentes.

Seu papel é garantir que mudanças em infraestrutura sejam planejadas, revisadas e validadas antes de qualquer aplicação, respeitando ambiente, state, secrets, permissões e blast radius.

---

## Quando usar

Use esta skill quando a task envolver:

- Terraform;
- Bicep;
- ARM templates;
- IaC modules;
- plan;
- apply;
- destroy;
- state;
- resource group;
- Azure resources;
- variáveis de ambiente;
- secrets;
- outputs;
- drift de infraestrutura;
- pipeline de IaC.

---

## Quando não usar

Não use esta skill quando:

- não houver IaC;
- a task for apenas leitura documental;
- a mudança estiver coberta por IaC security review sem entrega;
- a execução de IaC não estiver no escopo.

---

## Tese central

IaC deve ser tratada como mudança de sistema real.

Ação de infraestrutura precisa de:

- plano;
- diff;
- ambiente confirmado;
- revisão;
- validação;
- rollback ou mitigação;
- autorização quando houver risco.

---

## Método

### 1. Identificar ambiente e escopo

Registrar:

- dev, staging ou prod;
- subscription/tenant/resource group;
- módulo;
- recursos afetados;
- se há dados reais;
- se há custo real;
- se há produção.

---

### 2. Revisar alteração

Verificar:

- recursos criados;
- recursos alterados;
- recursos removidos;
- mudanças de rede;
- mudanças de permissão;
- mudanças de segredo;
- outputs;
- tags;
- nomes;
- região.

---

### 3. Gerar plano antes de aplicar

Para Terraform, preferir:

```bash
terraform fmt -check
terraform validate
terraform plan
```

Para Bicep, quando aplicável:

```bash
az bicep build --file <file>
az deployment group what-if ...
```

Nunca tratar `apply`/deploy como validação inicial.

---

### 4. Avaliar state

Em Terraform, considerar:

- backend remoto;
- lock;
- workspace correto;
- state sensível;
- drift;
- import;
- risco de `destroy`.

---

### 5. Avaliar segurança

Verificar:

- secret hardcoded;
- output sensível;
- IAM/RBAC;
- exposição pública;
- firewall;
- storage;
- managed identity;
- credencial estática.

---

### 6. Definir aprovação

Antes de aplicar mudança sensível:

- confirmar ambiente;
- revisar plan/what-if;
- confirmar risco;
- ter autorização humana;
- registrar rollback ou mitigação.

---

## Output esperado

```md
# Terraform/Bicep Delivery Review

## Ferramenta
<Terraform | Bicep | ARM | outro>

## Ambiente
<dev | staging | prod | incerto>

## Escopo
<recursos ou módulo afetado>

## Plano/What-if
<executado | não executado | não aplicável>

## Mudanças relevantes
- <mudança 1>
- <mudança 2>

## State/outputs/secrets
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

- ambiente está confirmado?
- plan/what-if foi considerado?
- há risco de destroy?
- state está seguro?
- outputs não expõem secret?
- permissões são mínimas?
- rede pública é intencional?
- custo foi considerado?
- tags/naming fazem sentido?
- apply/deploy tem autorização?

---

## Critérios de escalonamento

Escalar quando:

- ambiente for produção;
- houver `destroy`;
- houver IAM/RBAC;
- houver segredo;
- houver rede pública;
- houver banco/storage com dados reais;
- houver mudança de state;
- houver apply/deploy real;
- plan indicar alteração inesperada.

---

## Anti-patterns

Evitar:

- aplicar sem plan;
- confundir validate com segurança;
- usar workspace errado;
- ignorar state sensível;
- output de secret;
- permissão ampla por conveniência;
- abrir rede para todos;
- rodar destroy sem autorização;
- misturar dev e prod.

---

## Declaração operacional curta

IaC delivery exige plano antes de ação.  
Infraestrutura muda mundo real; o harness precisa ver o diff antes de tocar no ambiente.