# Protocolo de Review

## Finalidade

Este protocolo define como o harness deve revisar planos, implementações, artifacts e entregas antes de considerar uma task aceita, encerrada ou pronta para continuidade.

Seu papel é impedir que o sistema confunda:
- código que compila com código bom;
- plano bem escrito com plano correto;
- entrega funcional com entrega segura;
- ausência de erro visível com ausência de risco;
- linguagem confiante com evidência suficiente.

---

## Tese central

Review não é etapa decorativa.  
Review é o mecanismo que protege o sistema contra autoconfiança do executor, slop, over-engineering, regressão, risco operacional e fechamento prematuro.

O reviewer deve ser conservador o suficiente para proteger a qualidade, mas proporcional o suficiente para não transformar toda task simples em auditoria pesada.

---

## Quando o review deve acontecer

O review deve acontecer:

- antes de aprovar Execution Plan relevante;
- depois de implementação com impacto real;
- antes de handoff final;
- quando a task tocar risco R2 ou superior;
- quando houver alteração em arquitetura, segurança, persistência, integração, runtime ou observabilidade;
- quando houver suspeita de slop, drift ou complexidade desnecessária;
- quando a evidência for fraca ou incompleta.

---

## Tipos de review

### 1. Review de plano

Avalia se o Execution Plan é bom o suficiente para execução.

Deve verificar:
- se o problema foi entendido;
- se o discovery foi suficiente;
- se a classe de risco faz sentido;
- se a hipótese operacional é proporcional;
- se o escopo está claro;
- se a validação prevista é suficiente;
- se os critérios de escalonamento existem.

### 2. Review de implementação

Avalia se a mudança implementada respeita o plano e preserva qualidade.

Deve verificar:
- aderência ao escopo;
- coerência com a arquitetura local;
- causalidade do diff;
- segurança;
- evidência;
- efeitos colaterais;
- complexidade introduzida;
- risco operacional.

### 3. Review de handoff

Avalia se a task foi encerrada com memória útil.

Deve verificar:
- Completion Packet;
- lacunas explicitadas;
- riscos remanescentes;
- necessidade de atualização de estado;
- próximos passos;
- alinhamento com artifacts formais.

### 4. Review arquitetural

Avalia se a mudança respeita proporcionalidade arquitetural.

Deve ser usado quando houver:
- nova abstração;
- boundary relevante;
- alteração estrutural;
- integração externa;
- mudança de módulo;
- risco de over-engineering;
- risco de acoplamento ou drift.

### 5. Review operacional

Avalia se a mudança faz sentido como sistema real.

Deve ser usado quando houver impacto em:
- produção;
- cloud/runtime;
- observabilidade;
- falha parcial;
- performance;
- concorrência;
- estado local;
- banco;
- infraestrutura.

---

## Ordem recomendada de review

O review deve seguir uma sequência lógica:

1. confirmar o objeto revisado;
2. confirmar o escopo real da revisão;
3. comparar com Implementation Packet e Execution Plan;
4. analisar evidência;
5. verificar risco e classe real;
6. avaliar coerência arquitetural;
7. avaliar segurança e operação;
8. avaliar entropia e slop;
9. declarar lacunas;
10. emitir veredito.

Essa ordem evita que o review vire comentário solto.

---

## Critérios obrigatórios de review

### 1. Aderência ao problema

O review deve responder:
- a solução resolve o problema certo?
- ou resolveu uma variação inventada durante a execução?

### 2. Aderência ao escopo

O review deve responder:
- a mudança ficou dentro do envelope aprovado?
- houve expansão silenciosa?
- houve melhoria lateral não autorizada?

### 3. Aderência ao plan

O review deve responder:
- a implementação seguiu o plan?
- se desviou, o desvio foi justificado?
- o desvio exigia escalonamento?

### 4. Evidência

O review deve responder:
- o que foi realmente validado?
- o que não foi validado?
- a evidência é proporcional à classe de risco?

### 5. Segurança

O review deve observar:
- entrada não confiável;
- authn/authz;
- segredo;
- configuração;
- dependência;
- superfície de exposição;
- logging sensível;
- abuso plausível.

### 6. Produção e operação

O review deve observar:
- observabilidade;
- falha parcial;
- timeout;
- retry;
- fallback;
- runtime;
- estado local;
- consumo de recurso;
- comportamento sob carga plausível.

### 7. Arquitetura e complexidade

O review deve observar:
- a complexidade paga aluguel?
- há abstração por dor real?
- a solução ficou mais legível ou mais cerimonial?
- houve criação de camada, interface ou padrão sem necessidade clara?

### 8. Entropia e slop

O review deve observar:
- duplicação;
- nomenclatura inconsistente;
- helpers redundantes;
- espalhamento excessivo;
- documentação desatualizada;
- acoplamento novo;
- degradação de navegação.

---

## Vereditos possíveis

### Aprovado

Use quando:
- a entrega resolve o problema;
- a evidência é suficiente;
- o risco residual é aceitável;
- não há bloqueios relevantes.

### Aprovado com ressalvas

Use quando:
- a entrega é aceitável;
- existem lacunas conhecidas;
- o risco residual é tolerável;
- há follow-up recomendado, mas não bloqueante.

### Reavaliar

Use quando:
- há dúvida relevante;
- o plan ou a execução precisa de ajuste;
- a evidência ainda é insuficiente;
- há risco que precisa ser esclarecido antes de aceitar.

### Bloquear

Use quando:
- a mudança está fora do escopo;
- há falha de segurança relevante;
- há risco operacional não tratado;
- há slop significativo;
- há complexidade injustificada;
- há ausência de evidência crítica;
- a solução contraria authority source local.

---

## Uso do Review Report

Quando o review for relevante, ele deve produzir um `Review Report`.

O report deve registrar:
- objeto revisado;
- escopo revisado;
- leitura geral;
- aderência ao plan;
- pontos fortes;
- pontos de atenção;
- bloqueios;
- lacunas de evidência;
- risco residual;
- veredito.

O Review Report deve ser útil para decisão, não apenas uma lista de comentários.

---

## Relação com Core Architect

O Core Architect deve ser acionado quando o review envolver:
- trade-off arquitetural;
- risco de over-engineering;
- decisão estrutural;
- complexidade não justificada;
- tensão entre simplicidade e evolução;
- dúvidas sobre valor real da solução.

O executor pode revisar aspectos táticos.  
O Core Architect revisa julgamento estratégico.

---

## Relação com classes de risco

### R0
Review pode ser leve e focado em factualidade da investigação.

### R1
Review deve verificar escopo, causalidade e validação local.

### R2
Review deve ser explícito e normalmente produzir Review Report.

### R3
Review deve ser conservador, com atenção a arquitetura, segurança, operação e escalonamento.

### R4
Review padrão não basta; exige autorização e tratamento excepcional.

---

## Sinais de review fraco

Um review está fraco quando:

- só diz “parece bom”;
- não compara com o plan;
- não fala de evidência;
- ignora riscos remanescentes;
- não diferencia ressalva de bloqueio;
- não observa slop;
- não declara escopo efetivamente revisado.

---

## Declaração operacional curta

Review protege o sistema.  
Ele deve decidir, não apenas comentar.  
Ele deve se apoiar em evidência, não em confiança verbal.