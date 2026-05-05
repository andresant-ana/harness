# Project Context

## Finalidade

Este documento descreve o contexto geral do projeto.

Ele deve ajudar humano, Core Architect e agentes a entenderem o produto, o domínio, os objetivos, o público, as restrições e a direção técnica do sistema.

Este documento não é backlog, changelog nem plano de sprint.

---

## Identidade

### Nome do projeto

`<nome>`

### Descrição curta

`<descrição em 1 ou 2 frases>`

### Problema que resolve

`<qual problema real o projeto resolve>`

### Público/usuário-alvo

`<quem usa ou consome o sistema>`

### Valor principal

`<qual valor o sistema entrega>`

---

## Objetivos

### Objetivos atuais

- `<objetivo 1>`;
- `<objetivo 2>`;
- `<objetivo 3>`.

### Objetivos fora do escopo agora

- `<fora de escopo 1>`;
- `<fora de escopo 2>`;
- `<fora de escopo 3>`.

### Objetivos futuros possíveis

- `<futuro 1>`;
- `<futuro 2>`.

---

## Estágio do projeto

```text
Estágio: <ideação | MVP | piloto | produção inicial | produção madura | estudo | portfolio>
Maturidade técnica: <baixa | média | alta>
Maturidade de produto: <baixa | média | alta>
Usuários reais: <sim | não | incerto>
Produção real: <sim | não | incerto>
```

---

## Stack

```text
Backend:
Frontend:
Banco:
Cloud:
Infra/IaC:
CI/CD:
Observabilidade:
Auth:
Outros:
```

---

## Arquitetura em alto nível

```text
<descrever arquitetura macro>
```

Exemplo de dimensões relevantes:

- tipo de aplicação;
- módulos principais;
- boundaries de domínio;
- integrações;
- banco;
- runtime;
- deploy;
- comunicação síncrona/assíncrona.

---

## Domínio

### Conceitos principais

| Conceito | Significado |
|---------|-------------|
| `<conceito>` | `<descrição>` |

### Linguagem ubíqua

| Termo | Uso correto | Observações |
|------|-------------|-------------|
| `<termo>` | `<significado>` | `<observação>` |

### Regras importantes

- `<regra 1>`;
- `<regra 2>`;
- `<regra 3>`.

---

## Restrições

### Técnicas

- `<restrição técnica 1>`;
- `<restrição técnica 2>`.

### Produto/negócio

- `<restrição de produto 1>`;
- `<restrição de negócio 2>`.

### Operacionais

- `<restrição operacional 1>`;
- `<restrição operacional 2>`.

### Segurança/compliance

- `<restrição de segurança 1>`;
- `<restrição de compliance 2>`.

---

## Princípios locais

Este projeto deve priorizar:

- simplicidade proporcional;
- arquitetura por dor real;
- produção desde o início;
- segurança básica;
- observabilidade suficiente;
- testes proporcionais;
- ausência de over-engineering;
- clareza para humanos e agentes.

Adicionar princípios específicos:

- `<princípio local 1>`;
- `<princípio local 2>`.

---

## Decisões arquiteturais relevantes

| Decisão | Status | Referência |
|--------|--------|------------|
| `<decisão>` | `<ativa | em revisão | substituída>` | `<ADR/PROJECT_STATE/link>` |

Detalhes devem viver em ADR ou `PROJECT_STATE.md`, não aqui.

---

## Integrações

| Integração | Tipo | Finalidade | Risco |
|-----------|------|------------|-------|
| `<integração>` | `<API | banco | fila | cloud | auth | outro>` | `<finalidade>` | `<baixo | médio | alto>` |

---

## Ambientes

```text
Local:
Dev:
Staging:
Produção:
```

Detalhes operacionais devem viver em `OPERATIONAL_REALITY.md`.

---

## Relação com board/issues

```text
Board:
Repositório:
Milestones:
Issue pattern:
```

O board organiza trabalho.  
Este documento descreve contexto de projeto.

---

## Critérios de sucesso

O projeto será considerado bem encaminhado quando:

- `<critério 1>`;
- `<critério 2>`;
- `<critério 3>`.

---

## O que agentes devem evitar neste projeto

- `<anti-pattern local 1>`;
- `<anti-pattern local 2>`;
- `<anti-pattern local 3>`.

Exemplos comuns:

- criar microserviços sem dor real;
- adicionar mensageria sem justificativa;
- criar abstração para variação hipotética;
- ignorar comandos locais;
- tratar frontend como fonte de autorização;
- alterar schema sem considerar dados reais.

---

## Última atualização

```text
Data:
Autor:
Motivo:
```