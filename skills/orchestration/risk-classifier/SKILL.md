# Skill — Risk Classifier

## Finalidade

Esta skill orienta a classificação de risco de uma task usando as classes R0 a R4.

Seu papel é calibrar autonomia, profundidade de discovery, artifacts exigidos, validação, review e escalonamento.

Risco não é etiqueta burocrática.  
Risco define o comportamento do harness.

---

## Quando usar

Use esta skill quando:

- uma task estiver começando;
- a classe de risco estiver incerta;
- o discovery revelar impacto maior ou menor que o previsto;
- o agente precisar decidir peso de plan, review e validação;
- houver dúvida sobre autonomia;
- a task tocar código, dados, arquitetura, segurança, runtime, cloud, dependência ou produção.

---

## Quando não usar

Não use esta skill quando:

- a classe de risco já estiver clara e documentada;
- a task for leitura trivial sem consequência;
- o fluxo já tiver sido classificado e nada mudou;
- a classificação estiver sendo usada para justificar excesso de cerimônia.

---

## Classes de risco

### R0 — Leitura, pesquisa ou investigação

Use quando:

- não há mutação;
- a task é read-only;
- o objetivo é entender, resumir, investigar ou consultar;
- a saída natural é Investigation Note.

Exemplos:

- ler documentação;
- investigar estrutura do repo;
- consultar board em modo read-only;
- analisar logs sem alterar nada.

### R1 — Mudança local pequena e reversível

Use quando:

- há mutação pequena;
- o impacto é localizado;
- o diff é simples;
- não há risco estrutural;
- a validação é leve.

Exemplos:

- ajuste simples de documentação;
- correção pequena em arquivo isolado;
- refino local sem impacto sistêmico.

### R2 — Mudança funcional relevante

Use quando:

- a task altera comportamento real;
- toca múltiplos arquivos;
- exige validação funcional;
- pode afetar usuário, API, banco, integração ou fluxo;
- ainda está dentro de autonomia controlada.

Exemplos:

- nova feature;
- alteração de endpoint;
- mudança em query;
- ajuste em fluxo de frontend;
- mudança moderada em persistência.

### R3 — Mudança estrutural, sensível ou sistêmica

Use quando:

- há impacto arquitetural;
- há alteração de boundary;
- há integração relevante;
- há nova dependência importante;
- há risco operacional ou de segurança elevado;
- há mudança de execution model;
- há refactor estrutural.

Exemplos:

- introduzir mensageria;
- alterar estrutura modular;
- mudar estratégia de autenticação;
- criar abstração importante;
- alterar pipeline ou cloud runtime.

### R4 — Produção, segredo, irreversibilidade ou alto risco

Use quando:

- toca produção;
- toca segredo real;
- envolve dado real;
- pode causar dano externo;
- envolve operação destrutiva;
- altera IAM, deploy, banco real ou recurso cloud sensível.

R4 fica fora da autonomia padrão.

---

## Método

### 1. Identificar natureza da ação

Perguntar:

- é leitura ou mutação?
- altera código?
- altera estado externo?
- altera documentação durável?
- altera runtime, cloud, banco, auth ou dependência?
- pode afetar produção?

### 2. Identificar superfície tocada

Classificar superfícies:

- código;
- testes;
- docs;
- banco;
- API;
- frontend;
- auth;
- segredo;
- config;
- cloud;
- CI/CD;
- observabilidade;
- board;
- produção.

### 3. Avaliar reversibilidade

Perguntar:

- é fácil desfazer?
- o efeito é local?
- a alteração pode gerar dado persistido?
- há impacto fora do repositório?
- exige rollback?

Quanto menor a reversibilidade, maior o risco.

### 4. Avaliar blast radius

Perguntar:

- quantos módulos podem ser afetados?
- quantos fluxos dependem disso?
- há impacto em usuário?
- há impacto operacional?
- há impacto de segurança?

### 5. Avaliar incerteza

Perguntar:

- entendemos o problema?
- há authority source suficiente?
- há comportamento desconhecido?
- a task depende de suposição?
- há lacuna de validação?

Incerteza relevante aumenta a classe ou exige Investigation Note.

### 6. Escolher classe conservadora

Quando houver dúvida, escolher a classe mais conservadora até haver evidência para rebaixar.

### 7. Registrar justificativa

A classificação deve vir com rationale curto.

---

## Saída esperada

A saída deve conter:

- classe de risco;
- justificativa;
- artifacts esperados;
- validação esperada;
- necessidade de review;
- sinais de escalonamento.

---

## Artifacts por risco

### R0

Esperado:

- Investigation Note.

### R1

Esperado:

- Execution Plan simples, se houver mutação;
- Completion Packet enxuto.

### R2

Esperado:

- Implementation Packet;
- Execution Plan;
- Completion Packet;
- Review Report recomendado.

### R3

Esperado:

- Implementation Packet completo;
- Execution Plan forte ou Escalation Note;
- Review Report;
- Project State Entry quando durável;
- possível ADR.

### R4

Esperado:

- autorização humana explícita;
- Escalation Note ou artifact excepcional;
- rollback ou mitigação;
- review humano conservador.

---

## Checklist rápido

Antes de fechar a classe, perguntar:

- há mutação?
- há impacto funcional?
- há impacto estrutural?
- há impacto em segurança?
- há impacto operacional?
- há dependência nova?
- há produção ou segredo?
- há irreversibilidade?
- há incerteza alta?
- há necessidade de Core Architect?

---

## Anti-patterns

Evitar:

- classificar tudo como R1 para acelerar;
- classificar tudo como R3 por medo;
- ignorar aumento de risco durante execução;
- tratar documentação durável como se fosse irrelevante;
- tratar dependência nova como detalhe;
- tratar produção ou segredo como fluxo normal;
- esconder incerteza para manter autonomia.

---

## Declaração operacional curta

Classe de risco define o peso do harness.  
Risco bem classificado evita tanto negligência quanto burocracia.