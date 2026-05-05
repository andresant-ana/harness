# Local Commands

## Finalidade

Este documento registra os comandos reais deste projeto.

Agentes devem consultar este arquivo antes de inventar comandos genéricos da stack.

Se um comando não existir aqui, o agente pode sugerir um comando padrão com ressalva, mas não deve tratá-lo como autoridade.

---

## Ambiente esperado

```text
Sistema operacional:
Shell:
Runtime backend:
Runtime frontend:
Banco local:
Docker:
Cloud CLI:
Outros:
```

---

## Preparação inicial

```bash
# exemplo
<comando de setup>
```

Observações:

- `<observação 1>`;
- `<observação 2>`.

---

## Instalação/restauração de dependências

### Backend

```bash
<comando>
```

### Frontend

```bash
<comando>
```

### Infra/Tools

```bash
<comando>
```

---

## Build

### Build completo

```bash
<comando>
```

### Build backend

```bash
<comando>
```

### Build frontend

```bash
<comando>
```

---

## Testes

### Todos os testes

```bash
<comando>
```

### Testes backend

```bash
<comando>
```

### Testes frontend

```bash
<comando>
```

### Testes de integração

```bash
<comando>
```

### Testes específicos

```bash
<comando>
```

Observações:

- `<como rodar subset>`;
- `<dependências necessárias>`.

---

## Lint

```bash
<comando>
```

---

## Format

```bash
<comando>
```

---

## Typecheck

```bash
<comando>
```

---

## Execução local

### Backend

```bash
<comando>
```

### Frontend

```bash
<comando>
```

### Fullstack

```bash
<comando>
```

---

## Docker

### Subir ambiente local

```bash
<comando>
```

### Derrubar ambiente local

```bash
<comando>
```

### Logs

```bash
<comando>
```

### Rebuild

```bash
<comando>
```

---

## Banco de dados

### Criar/resetar banco local

```bash
<comando>
```

### Rodar migrations

```bash
<comando>
```

### Criar migration

```bash
<comando>
```

### Reverter migration

```bash
<comando>
```

### Seed

```bash
<comando>
```

Observações:

- não rodar comandos destrutivos sem confirmar ambiente;
- nunca aplicar migration em produção sem autorização explícita.

---

## CI/CD local

Comandos que aproximam o pipeline:

```bash
<comando>
```

---

## Infra/IaC

### Validate

```bash
<comando>
```

### Plan / What-if

```bash
<comando>
```

### Apply / Deploy

```bash
<comando>
```

Aplicação real exige autorização quando houver risco externo.

---

## Git

### Checagem pré-commit

```bash
git status
git diff --check
```

Comandos adicionais do projeto:

```bash
<comando>
```

---

## Comandos proibidos ou sensíveis

Não executar sem autorização explícita:

```bash
rm -rf <path>
git reset --hard
git clean -fd
terraform apply
terraform destroy
az deployment ...
dotnet ef database update <produção>
docker volume rm ...
```

Adicionar comandos sensíveis locais:

```bash
<comando sensível>
```

---

## Variáveis de ambiente necessárias

Não registrar valores reais.

| Nome | Obrigatória? | Ambiente | Observação |
|-----|--------------|----------|------------|
| `<VAR>` | `<sim | não>` | `<local | dev | prod>` | `<sem valor real>` |

---

## Troubleshooting comum

### Problema

`<descrição>`

### Sintoma

```text
<erro ou sintoma>
```

### Solução segura

```bash
<comando>
```

---

## Última atualização

```text
Data:
Autor:
Motivo:
```