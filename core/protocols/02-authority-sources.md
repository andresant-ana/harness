# Authority Sources

## Finalidade

Este protocolo define como o harness deve identificar, priorizar e respeitar as fontes de verdade local do projeto.

Seu papel é impedir que o runtime invente fluxo operacional, arquitetura local, comandos de validação ou convenções do repositório com base em suposição genérica.

---

## Tese central

Quando houver conflito entre:
- suposição do modelo,
- heurística do agente,
- conhecimento genérico de framework

e
- fonte de verdade local do projeto,

vence a fonte de verdade local documentada.

---

## O que são authority sources

Authority sources são os artefatos que descrevem como o projeto realmente funciona.

Eles se dividem em duas categorias:

### 1. Authority files
Arquivos que codificam a verdade local.

### 2. Authority commands
Comandos reais que definem como buildar, testar, validar, rodar e operar localmente.

---

## Exemplos de authority files

Podem incluir:

- `AGENTS.md`
- `opencode.json`
- `README.md` do projeto
- `WORKSPACE_GUIDE.md`
- `PROJECT_CONTEXT.md`
- `PROJECT_STATE.md`
- documentação local em `docs/`
- arquivos de solution/workspace
- manifests de dependência
- configs de test/lint/build
- pipeline definitions
- configs de runtime
- arquivos de infraestrutura local
- documentação de módulos e boundaries

Nem todo projeto terá os mesmos, mas todo projeto maduro precisa ter algum conjunto mínimo de authority files.

---

## Exemplos de authority commands

Podem incluir comandos reais para:

- build;
- test;
- lint;
- format;
- bootstrap de ambiente;
- run local;
- migrations;
- validação de contratos;
- profiling;
- observabilidade local;
- checagens de segurança.

Esses comandos precisam ser tratados como verdade local do projeto, não como detalhe opcional.

---

## Regra de prioridade

O sistema deve seguir esta ordem de confiança:

1. authority files e authority commands do projeto;
2. convenções explícitas do workspace;
3. documentação local coerente com o repositório;
4. padrões reconhecidos do framework;
5. conhecimento genérico do modelo.

Ou seja:
**o conhecimento genérico sempre perde para a verdade local documentada**.

---

## O que fazer no início da task

Antes de produzir Execution Plan, o agente deve tentar responder:

- quais são os authority files desta task;
- quais comandos reais regem o ciclo de validação;
- se a task altera alguma dessas fontes;
- se há conflito entre documentação e realidade observada.

---

## Quando authority source está faltando

Se o projeto não tiver authority source suficiente, o agente não deve fingir certeza.

As respostas corretas nesse caso são:
- explicitar ausência;
- trabalhar com mais cautela;
- marcar risco aumentado;
- sugerir formalização futura;
- evitar decisões que dependam de certeza inexistente.

---

## Quando authority source está desatualizada

Quando houver indício de conflito entre:
- documentação local;
- comandos documentados;
- estrutura real do projeto;
- comportamento observado

o agente deve:
1. registrar o conflito;
2. não tratar a fonte como plenamente confiável;
3. considerar atualização futura da documentação local;
4. escalar se a decisão depender fortemente disso.

---

## Relação com PROJECT_STATE

`PROJECT_STATE.md` é uma authority source de estado durável do projeto.

Ele não substitui:
- board,
- código,
- configuração,
- comando real.

Mas ajuda a preservar:
- estado técnico atual;
- o que já foi feito;
- limitações conhecidas;
- pontos frágeis;
- próximos passos;
- implicações locais relevantes.

---

## Relação com GitHub Projects e board

Board e issue tracker não são authority sources arquiteturais ou operacionais do repositório.

Eles são authority sources de:
- estado de trabalho;
- backlog;
- priorização;
- sequência de tasks;
- dependências organizacionais.

O sistema deve usar ambos sem confundir suas funções.

---

## Como registrar authority sources no workspace

Todo workspace deveria registrar explicitamente:

- arquivos de autoridade;
- comandos de autoridade;
- observações de confiabilidade;
- lacunas conhecidas;
- pontos onde documentação e realidade podem divergir.

Isso reduz custo de discovery e melhora a qualidade do plan.

---

## Sinal de boa maturidade de projeto

Projeto maduro para uso com agent costuma ter:
- authority files fáceis de localizar;
- authority commands claros;
- documentação curta, mas verdadeira;
- pouca necessidade de inferência do modelo.

---

## Declaração operacional curta

Não assuma o projeto.  
Pergunte ao projeto como ele funciona.  
Authority sources existem para impedir que o runtime confunda familiaridade com conhecimento real.