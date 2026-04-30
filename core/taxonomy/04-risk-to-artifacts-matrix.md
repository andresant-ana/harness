# Matriz de Risco para Artefatos

## Finalidade

Este documento conecta classes de risco aos artifacts, níveis de review, evidência, autonomia e escalonamento esperados.

Seu papel é tornar operacional a taxonomia de risco do harness.

---

## Tese central

Risco muda comportamento.

Uma task R0 não deve carregar a mesma cerimônia de uma task R3.  
Uma task R3 não pode ser tratada com a leveza de uma R1.

A matriz existe para calibrar profundidade, não para burocratizar.

---

## Classes de risco

| Classe | Natureza | Autonomia padrão |
|--------|----------|------------------|
| R0 | Leitura, inspeção, pesquisa e síntese sem mutação | Alta |
| R1 | Mudança local, pequena e reversível | Moderada |
| R2 | Mudança funcional relevante | Controlada |
| R3 | Mudança estrutural, sensível ou sistêmica | Baixa |
| R4 | Produção, segredos, irreversibilidade ou alto risco | Fora da autonomia padrão |

---

## Matriz resumida

| Risco | Artifact de entrada | Artifact de execução | Artifact de saída | Review | Escalonamento |
|------|----------------------|----------------------|-------------------|--------|---------------|
| R0 | Pergunta / contexto | Investigation Note | Investigation Note | Leve | Raro |
| R1 | Implementation Packet enxuto | Execution Plan simples | Completion Packet enxuto | Proporcional | Se risco subir |
| R2 | Implementation Packet completo | Execution Plan completo | Completion Packet + Review Report | Explícito | Possível |
| R3 | Implementation Packet completo | Escalation Note antes de mutação relevante | Review Report / Completion Packet | Forte | Provável |
| R4 | Solicitação excepcional | Autorização explícita | Artifact excepcional | Forte/humano | Obrigatório |

---

## R0 — Investigação e leitura

### Natureza

R0 é read-only.

Exemplos:
- entender parte do repositório;
- consultar docs;
- ler issue;
- investigar bug sem mutação;
- sintetizar contexto;
- consultar MCP read-only.

### Artifacts esperados

Obrigatório ou recomendado:
- Investigation Note.

Opcional:
- Escalation Note, se a investigação revelar risco estrutural.

### Evidência esperada

- fontes consultadas;
- achados factuais;
- hipóteses separadas;
- lacunas explícitas.

### Review

Leve, focado em:
- factualidade;
- fonte;
- separação entre fato e hipótese.

---

## R1 — Mudança local de baixo risco

### Natureza

R1 envolve mudança pequena, local e reversível.

Exemplos:
- ajuste simples;
- correção localizada;
- documentação pequena;
- refino sem impacto estrutural.

### Artifacts esperados

Recomendado:
- Implementation Packet enxuto;
- Execution Plan simples;
- Completion Packet enxuto.

Opcional:
- Review Report leve.

### Evidência esperada

- validação local proporcional;
- diff revisado;
- lacunas declaradas.

### Review

Proporcional, focado em:
- escopo;
- causalidade;
- ausência de expansão silenciosa.

---

## R2 — Mudança funcional relevante

### Natureza

R2 envolve impacto funcional moderado ou relevante.

Exemplos:
- nova feature;
- alteração em fluxo;
- mudança em múltiplos arquivos;
- mudança em banco ou integração com risco controlado;
- refactor moderado.

### Artifacts esperados

Obrigatório:
- Implementation Packet;
- Execution Plan;
- Completion Packet.

Recomendado:
- Review Report.

Opcional:
- Project State Entry, se houver mudança durável.

### Evidência esperada

- discovery;
- authority sources;
- build/test/lint quando aplicável;
- validação funcional;
- risco residual;
- lacunas explícitas.

### Review

Explícito, cobrindo:
- aderência ao plan;
- segurança;
- operação;
- entropia;
- evidência.

---

## R3 — Mudança estrutural ou sensível

### Natureza

R3 envolve alteração com impacto sistêmico, arquitetural, operacional ou de segurança relevante.

Exemplos:
- mudança de boundary;
- nova integração externa relevante;
- mensageria;
- mudança de execution model;
- migration sensível;
- alteração estrutural de módulos;
- introdução de abstração importante.

### Artifacts esperados

Obrigatório:
- Implementation Packet;
- Execution Plan ou Escalation Note antes da mutação;
- Review Report;
- Completion Packet, se houver entrega.

Frequentemente necessário:
- Escalation Note;
- ADR;
- Project State Entry.

### Evidência esperada

- trade-off explícito;
- análise de risco;
- validação forte;
- decisão estratégica;
- lacunas claras;
- impacto operacional e arquitetural.

### Review

Forte, conservador e possivelmente com Core Architect.

---

## R4 — Produção, segredos e irreversibilidade

### Natureza

R4 está fora da autonomia padrão.

Exemplos:
- produção;
- segredo;
- dado real;
- operação destrutiva;
- IAM;
- deploy sensível;
- migration real;
- ação externa irreversível.

### Artifacts esperados

Obrigatório:
- autorização explícita;
- Escalation Note ou documento excepcional;
- registro de decisão;
- evidência e rollback quando aplicável.

### Evidência esperada

- máxima clareza;
- comando ou ação exata;
- ambiente confirmado;
- risco entendido;
- plano de mitigação;
- aprovação humana.

### Review

Humano e conservador.

---

## Regras transversais

### Quando a classe subir

Se a task começar como R1 e revelar risco R2/R3, o sistema deve:
- parar;
- reclassificar;
- atualizar plan;
- escalar se necessário.

### Quando a classe descer

Uma task pode ser rebaixada se discovery mostrar que o risco era menor.  
Mas isso deve ser explicitado.

### Quando houver dúvida

Escolher a classe mais conservadora até haver evidência para rebaixar.

---

## Relação com Project State Entry

Project State Entry deve ser considerado quando:

- R2 altera estado durável;
- R3 envolve decisão ou arquitetura;
- R0 descobre fato durável;
- R4 gera consequência ou decisão crítica.

---

## Relação com Core Architect

Acionar Core Architect quando:

- R3;
- trade-off relevante;
- over-engineering provável;
- decisão arquitetural;
- conflito entre simplicidade e sofisticação;
- risco estrutural.

---

## Declaração operacional curta

Risco define peso do fluxo.  
O harness usa artifacts para calibrar rigor, preservar evidência e impedir autonomia indevida.