# Checklist — Project Bootstrap

## Finalidade

Este checklist orienta a preparação inicial de um projeto/workspace para uso com o harness.

Ele deve ser usado quando um novo projeto passa a operar com a engenharia de harness, garantindo que as fontes locais de autoridade, comandos, estado técnico, riscos e realidade operacional estejam minimamente definidos.

---

## Identificação

```text
Projeto:
Repositório:
Responsável:
Data:
Status: <não iniciado | em andamento | concluído | bloqueado>
```

---

## 1. Estrutura mínima do workspace

Verificar se existem ou serão criados:

- [ ] `WORKSPACE_GUIDE.md`;
- [ ] `PROJECT_CONTEXT.md`;
- [ ] `AUTHORITY_SOURCES.md`;
- [ ] `LOCAL_COMMANDS.md`;
- [ ] `PROJECT_STATE.md`;
- [ ] `WORKTREE_POLICY.md`;
- [ ] `RISK_SURFACES.md`;
- [ ] `DONE_CRITERIA.md`;
- [ ] `OPERATIONAL_REALITY.md`;
- [ ] `GITHUB_PROJECTS_CONTEXT.md`, se houver board.

Observações:

```text
<lacunas ou adaptações locais>
```

---

## 2. Contexto do projeto

Confirmar que `PROJECT_CONTEXT.md` responde:

- [ ] o que o projeto faz;
- [ ] qual problema resolve;
- [ ] quem usa;
- [ ] qual é a stack;
- [ ] qual é o estágio do projeto;
- [ ] quais objetivos estão dentro e fora do escopo;
- [ ] quais conceitos de domínio importam;
- [ ] quais restrições técnicas, operacionais e de produto existem.

Lacunas:

```text
<lacunas>
```

---

## 3. Fontes de autoridade

Confirmar que `AUTHORITY_SOURCES.md` lista:

- [ ] código/configs principais;
- [ ] README/docs relevantes;
- [ ] comandos de autoridade;
- [ ] ADRs;
- [ ] `PROJECT_STATE.md`;
- [ ] pipeline/CI;
- [ ] arquivos de infraestrutura;
- [ ] board/issues, se aplicável;
- [ ] fontes externas confiáveis, se necessário.

Pergunta crítica:

```text
O agente saberá onde procurar a verdade local antes de agir?
```

---

## 4. Comandos locais

Confirmar que `LOCAL_COMMANDS.md` define, quando aplicável:

- [ ] setup;
- [ ] restore/install;
- [ ] build;
- [ ] test;
- [ ] lint;
- [ ] format;
- [ ] typecheck;
- [ ] run local;
- [ ] Docker;
- [ ] banco/migrations;
- [ ] CI local;
- [ ] IaC validate/plan;
- [ ] comandos sensíveis/proibidos.

Não deixar comando crítico apenas em memória conversacional.

---

## 5. PROJECT_STATE inicial

Confirmar que `PROJECT_STATE.md` registra:

- [ ] snapshot técnico atual;
- [ ] decisões ativas;
- [ ] boundaries importantes;
- [ ] estado operacional conhecido;
- [ ] riscos conhecidos;
- [ ] limitações conhecidas;
- [ ] dívidas conscientes;
- [ ] follow-ups estruturais relevantes.

Não transformar o arquivo em changelog ou backlog.

---

## 6. Política de branch/worktree

Confirmar que `WORKTREE_POLICY.md` define:

- [ ] branch principal;
- [ ] padrão de branch;
- [ ] quando usar worktree;
- [ ] quando abrir PR;
- [ ] comandos pré-commit;
- [ ] operações Git sensíveis;
- [ ] como resolver conflitos;
- [ ] relação com issues/board.

---

## 7. Superfícies de risco

Confirmar que `RISK_SURFACES.md` mapeia riscos em:

- [ ] auth;
- [ ] dados sensíveis;
- [ ] API/input externo;
- [ ] banco/schema;
- [ ] cloud/infra;
- [ ] CI/CD;
- [ ] secrets/config;
- [ ] frontend;
- [ ] dependências;
- [ ] arquitetura;
- [ ] observabilidade;
- [ ] produção.

---

## 8. Critérios de pronto

Confirmar que `DONE_CRITERIA.md` define:

- [ ] critérios mínimos para qualquer task;
- [ ] critérios por classe de risco;
- [ ] validações técnicas;
- [ ] critérios documentais;
- [ ] handoff;
- [ ] motivos aceitáveis para lacunas;
- [ ] motivos de bloqueio.

---

## 9. Realidade operacional

Confirmar que `OPERATIONAL_REALITY.md` registra:

- [ ] ambientes;
- [ ] runtime;
- [ ] execução local;
- [ ] configuração;
- [ ] secrets sem valores reais;
- [ ] banco;
- [ ] deploy;
- [ ] CI/CD;
- [ ] observabilidade;
- [ ] integrações externas;
- [ ] gaps operacionais;
- [ ] runbook mínimo.

---

## 10. GitHub Projects / board

Se houver board, confirmar que `GITHUB_PROJECTS_CONTEXT.md` define:

- [ ] board principal;
- [ ] repo;
- [ ] campos;
- [ ] status workflow;
- [ ] labels importantes;
- [ ] uso read-only;
- [ ] limites de MCP;
- [ ] relação entre issue, execução e `PROJECT_STATE.md`.

Board organiza trabalho.  
`PROJECT_STATE.md` preserva verdade técnica.

---

## 11. Primeira validação do workspace

Rodar ou registrar comandos seguros:

```bash
git status
find . -maxdepth 2 -type f | sort
```

Validações específicas:

```bash
<comando de build/test/lint se já existir>
```

Resultado:

```text
<resultado>
```

---

## 12. Critério de conclusão do bootstrap

Bootstrap concluído quando:

- [ ] os documentos locais mínimos existem;
- [ ] comandos principais estão documentados;
- [ ] fontes de autoridade estão claras;
- [ ] estado técnico inicial está registrado;
- [ ] riscos principais estão visíveis;
- [ ] critérios de pronto estão definidos;
- [ ] agentes conseguem iniciar discovery sem depender de conversa antiga.

---

## Lacunas aceitas

| Lacuna | Motivo | Critério de resolução |
|-------|--------|-----------------------|
| `<lacuna>` | `<motivo>` | `<critério>` |

---

## Próximo passo

```text
<primeira task real | completar docs locais | validar comandos | criar board | outro>
```