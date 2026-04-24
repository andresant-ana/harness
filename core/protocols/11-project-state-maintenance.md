# Protocolo de Manutenção do PROJECT_STATE

## Finalidade

Este protocolo define como o harness deve manter o `PROJECT_STATE.md` no workspace de cada projeto.

Seu papel é garantir que o estado técnico e operacional durável do projeto sobreviva a sessões, agentes, tasks e mudanças de contexto.

---

## Tese central

Board organiza trabalho.  
`PROJECT_STATE.md` preserva realidade técnica.

O estado do projeto não pode depender de memória conversacional, transcript bruto ou lembrança do agente.

Sempre que uma task alterar a realidade durável do projeto, o `PROJECT_STATE.md` deve ser considerado para atualização.

---

## O que é PROJECT_STATE

`PROJECT_STATE.md` é uma authority source local do workspace.

Ele deve registrar:
- estado técnico atual;
- decisões duráveis;
- riscos conhecidos;
- limitações;
- dívidas conscientes;
- comandos relevantes;
- mudanças de arquitetura;
- operational reality;
- próximos passos técnicos importantes.

Ele não é changelog, board, diário ou relatório de cada task.

---

## Quando atualizar

Atualizar quando houver:

- mudança arquitetural;
- alteração de boundary;
- mudança de execution model;
- alteração em comandos locais;
- nova integração;
- risco novo conhecido;
- limitação técnica descoberta;
- dívida técnica assumida;
- decisão que precisa sobreviver;
- divergência entre documentação e realidade;
- mudança operacional relevante.

---

## Quando não atualizar

Não atualizar quando:

- a mudança é trivial e sem impacto durável;
- o Completion Packet já basta;
- a informação é efêmera;
- o detalhe pertence apenas ao diff;
- a entrada aumentaria ruído sem ajudar decisão futura.

A regra não é registrar tudo.  
A regra é registrar o que muda entendimento futuro do projeto.

---

## Processo de atualização

### 1. Identificar mudança durável

Ao final da task, verificar:
- algo mudou na forma de entender o projeto?
- algo precisa ser lembrado em uma futura sessão?
- algo evita reinvestigação?
- algo altera operação, arquitetura ou risco?

### 2. Escolher tipo de entrada

Classificar como:
- estado técnico;
- decisão;
- risco;
- limitação;
- dívida técnica;
- comando;
- integração;
- arquitetura;
- operação;
- segurança;
- follow-up.

### 3. Escrever Project State Entry

Usar o schema canônico de `Project State Entry`.

### 4. Atualizar ou consolidar

Decidir se:
- cria nova entrada;
- atualiza entrada existente;
- marca entrada antiga como resolvida, substituída ou obsoleta.

### 5. Referenciar origem

Ligar a entrada a:
- issue;
- PR;
- commit;
- artifact;
- ADR;
- investigação;
- decisão humana;
- Core Architect.

---

## Estrutura esperada do PROJECT_STATE

Cada projeto pode adaptar a organização, mas a estrutura deve permitir localizar rapidamente:

- visão atual do estado técnico;
- decisões ativas;
- riscos e limitações;
- dívidas conscientes;
- comandos ou operational reality;
- histórico relevante recente;
- follow-ups estruturais.

---

## Relação com Completion Packet

O Completion Packet pode indicar necessidade de state update.

Mas o Completion Packet não deve ser copiado inteiro para o `PROJECT_STATE.md`.

O estado deve absorver apenas o que for durável.

---

## Relação com Investigation Note

Investigações podem gerar entradas quando descobrirem:

- fato estrutural;
- limitação;
- risco;
- conflito entre documentação e realidade;
- comando real;
- comportamento operacional relevante.

---

## Relação com Review Report

Review pode exigir atualização quando encontrar:

- risco não registrado;
- dívida não documentada;
- slop aceito temporariamente;
- decisão implícita;
- necessidade de follow-up.

---

## Relação com board

O board informa a gestão do trabalho.

`PROJECT_STATE.md` informa a verdade técnica.

Exemplo:
- board diz “implementar autenticação”;
- `PROJECT_STATE.md` diz “auth usa JWT com refresh token, risco X em observação, comando Y valida fluxo local”.

Eles são complementares, não substitutos.

---

## Papel do executor

O executor deve:
- detectar necessidade de atualização;
- propor Project State Entry;
- não inflar o state com ruído;
- registrar lacunas quando não puder atualizar;
- escalar se a atualização depender de decisão estratégica.

---

## Papel do Core Architect

O Core Architect deve:
- validar entradas estratégicas;
- impedir ruído;
- garantir que decisões e trade-offs relevantes sobrevivam;
- revisar se o state reflete a realidade arquitetural do projeto.

---

## Sinais de PROJECT_STATE ruim

O state está ruim quando:

- virou changelog;
- está desatualizado;
- repete issues;
- não registra decisões importantes;
- não mostra riscos;
- ninguém consegue usá-lo para retomar contexto;
- contradiz o repositório.

---

## Critério de qualidade

Um bom `PROJECT_STATE.md` deve ser:

- curto o suficiente para ser lido;
- denso o suficiente para orientar;
- atualizado apenas com memória durável;
- factual;
- útil para humano e agente;
- fácil de revisar.

---

## Declaração operacional curta

`PROJECT_STATE.md` não registra tudo.  
Registra o que precisa sobreviver.  
Ele é a memória técnica viva do projeto.