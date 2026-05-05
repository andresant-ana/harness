# Operational Reality

## Finalidade

Este documento registra a realidade operacional do projeto.

Ele descreve como o sistema roda, é configurado, validado, observado, entregue e diagnosticado na prática.

Não é arquitetura idealizada.  
É realidade atual.

---

## Regra central

Se o agente não sabe como o sistema roda fora do pensamento abstrato, ele não deve fingir prontidão de produção.

Este documento deve expor:

- ambientes;
- runtime;
- deploy;
- config;
- segredos;
- banco;
- observabilidade;
- limitações;
- gaps operacionais.

---

## Ambientes

| Ambiente | Existe? | Finalidade | Observações |
|----------|---------|------------|-------------|
| Local | `<sim | não | parcial>` | Desenvolvimento | `<observação>` |
| Dev | `<sim | não | parcial>` | Teste remoto | `<observação>` |
| Staging | `<sim | não | parcial>` | Pré-produção | `<observação>` |
| Produção | `<sim | não | parcial>` | Usuários reais | `<observação>` |

---

## Runtime

```text
Tipo de workload:
Runtime local:
Runtime remoto:
Container:
Cloud:
Processo principal:
Workers/jobs:
```

---

## Como rodar localmente

Referência primária: `LOCAL_COMMANDS.md`.

Resumo:

```bash
<comando principal>
```

Dependências locais:

- `<dependência 1>`;
- `<dependência 2>`.

---

## Configuração

### Variáveis necessárias

Não registrar valores reais.

| Variável | Ambiente | Obrigatória? | Observação |
|---------|----------|--------------|------------|
| `<VAR>` | `<local/dev/prod>` | `<sim/não>` | `<observação>` |

### Configs por ambiente

```text
Local:
Dev:
Staging:
Produção:
```

### Defaults perigosos

- `<default perigoso ou nenhum>`.

---

## Segredos

Não registrar valores.

```text
Secret store:
.env local:
CI secrets:
Cloud secrets:
Rotação:
Riscos:
```

Observações:

- `<observação 1>`;
- `<observação 2>`.

---

## Banco de dados

```text
Tipo:
Local:
Remoto:
Migrations:
Seed:
Backup:
Dados reais:
Riscos:
```

Comandos vivem em `LOCAL_COMMANDS.md`.

---

## Deploy

```text
Método atual:
Pipeline:
Manual/automático:
Ambiente alvo:
Rollback:
Gates:
Responsável:
```

---

## CI/CD

```text
Provider:
Workflows:
Checks obrigatórios:
Deploy automático:
Secrets usados:
Gaps conhecidos:
```

---

## Observabilidade

```text
Logs:
Métricas:
Tracing:
Health checks:
Alertas:
Dashboards:
Application Insights/Azure Monitor:
Gaps:
```

Perguntas mínimas:

- sabemos se o sistema subiu?
- sabemos se está falhando?
- sabemos latência/erro de endpoints críticos?
- sabemos diagnosticar startup failure?
- sabemos diferenciar liveness e readiness, se aplicável?

---

## Integrações externas

| Integração | Ambiente | Criticidade | Falha esperada | Observabilidade |
|-----------|----------|-------------|----------------|-----------------|
| `<integração>` | `<ambiente>` | `<baixa/média/alta>` | `<modo de falha>` | `<sinal>` |

---

## Superfícies operacionais sensíveis

- deploy;
- secrets;
- banco;
- migration;
- cloud config;
- fila/job;
- auth;
- observabilidade;
- CORS;
- storage;
- pipeline.

Detalhes:

```text
<detalhes locais>
```

---

## Gaps operacionais conhecidos

| Gap | Impacto | Status | Próxima ação |
|-----|---------|--------|--------------|
| `<gap>` | `<impacto>` | `<ativo | em progresso | aceito>` | `<ação>` |

---

## Runbook mínimo

### Startup falha

```text
Sintomas:
Onde olhar:
Comandos:
Riscos:
```

### Banco indisponível

```text
Sintomas:
Onde olhar:
Comandos:
Riscos:
```

### Deploy falha

```text
Sintomas:
Onde olhar:
Comandos:
Rollback:
```

### Erro 5xx

```text
Sintomas:
Onde olhar:
Correlação:
Próximo passo:
```

---

## O que agentes não devem fazer

- tocar produção sem autorização;
- revelar segredo;
- aplicar migration real sem aprovação;
- alterar cloud config manualmente sem plano;
- tratar deploy como detalhe;
- declarar “pronto para produção” sem evidência;
- usar autoscaling para mascarar código ruim;
- ignorar observabilidade.

---

## Última atualização

```text
Data:
Autor:
Motivo:
```