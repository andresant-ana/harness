# Authority Sources

## Finalidade

Este documento lista as fontes locais de autoridade do projeto.

Authority source é qualquer arquivo, comando, documento, configuração ou convenção que deve prevalecer sobre suposição genérica do agente.

O objetivo é evitar que o agente invente estrutura, comando, arquitetura, validação ou comportamento.

---

## Regra central

A verdade local vence conhecimento genérico.

Quando houver conflito entre:

- documentação global do harness;
- memória conversacional;
- conhecimento do modelo;
- tutorial externo;
- arquivo local;
- comando local;

o agente deve priorizar a fonte local mais específica, salvo se ela estiver claramente obsoleta.

---

## Ordem de autoridade

Adaptar conforme o projeto.

```text
1. Código real e testes existentes
2. Configurações reais do projeto
3. PROJECT_STATE.md
4. ADRs
5. LOCAL_COMMANDS.md
6. OPERATIONAL_REALITY.md
7. README.md / documentação local
8. Issues/PRs vinculadas
9. Board/GitHub Projects
10. Documentação externa oficial
```

---

## Arquivos de autoridade

| Arquivo | Função | Status | Observações |
|--------|--------|--------|-------------|
| `README.md` | `<função>` | `<ativo | parcial | obsoleto | incerto>` | `<observação>` |
| `PROJECT_STATE.md` | Memória técnica viva | `<ativo | parcial | obsoleto | incerto>` | `<observação>` |
| `LOCAL_COMMANDS.md` | Comandos reais | `<ativo | parcial | obsoleto | incerto>` | `<observação>` |
| `OPERATIONAL_REALITY.md` | Realidade operacional | `<ativo | parcial | obsoleto | incerto>` | `<observação>` |
| `DONE_CRITERIA.md` | Critérios locais de pronto | `<ativo | parcial | obsoleto | incerto>` | `<observação>` |

Adicionar outros:

| Arquivo | Função | Status | Observações |
|--------|--------|--------|-------------|
| `<arquivo>` | `<função>` | `<status>` | `<observação>` |

---

## Configurações de autoridade

| Arquivo/config | O que define | Observações |
|---------------|--------------|-------------|
| `<arquivo>.sln` | `<ex: solution principal>` | `<observação>` |
| `<arquivo>.csproj` | `<ex: target framework/dependências>` | `<observação>` |
| `package.json` | `<ex: scripts frontend>` | `<observação>` |
| `docker-compose.yml` | `<ex: ambiente local>` | `<observação>` |
| `.github/workflows/...` | `<ex: CI/CD>` | `<observação>` |
| `infra/...` | `<ex: IaC>` | `<observação>` |

---

## Comandos de autoridade

Comandos devem ser definidos em `LOCAL_COMMANDS.md`.

Este documento apenas aponta para eles.

```text
Build:
Test:
Lint:
Format:
Run:
Migrations:
Docker:
CI:
```

---

## ADRs

| ADR | Decisão | Status |
|-----|---------|--------|
| `<ADR-0001>` | `<decisão>` | `<ativo | substituído | em revisão>` |

---

## Documentação de módulo

| Documento | Módulo/área | Função |
|----------|-------------|--------|
| `<doc>` | `<módulo>` | `<função>` |

---

## Board e issues

### Board

```text
URL:
Uso:
Limite:
```

O board é autoridade para gestão de trabalho, não para verdade técnica.

### Issues

Issues podem ser usadas como:

- entrada de task;
- critério de aceite;
- histórico de discussão;
- referência de prioridade.

Issues não substituem:

- código;
- ADR;
- PROJECT_STATE;
- documentation local.

---

## Fontes externas confiáveis

| Fonte | Uso permitido | Observações |
|------|---------------|-------------|
| `<docs oficiais>` | `<quando usar>` | `<observação>` |
| `<repo oficial>` | `<quando usar>` | `<observação>` |

Evitar fonte externa fraca quando houver fonte oficial.

---

## Como agir em conflito

Quando fontes entrarem em conflito:

1. identificar as fontes conflitantes;
2. declarar o conflito;
3. verificar qual é mais específica e atual;
4. procurar evidência no código/config;
5. não escolher no chute;
6. escalar se houver impacto relevante.

---

## Sinais de authority source obsoleta

- comando documentado não roda;
- arquitetura descrita não existe no código;
- README contradiz pipeline;
- PROJECT_STATE contradiz implementação;
- ADR ativa contradiz decisão posterior;
- board indica status incompatível com repo.

---

## Última atualização

```text
Data:
Autor:
Motivo:
```