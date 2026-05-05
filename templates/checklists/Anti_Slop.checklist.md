# Checklist — Anti-Slop

## Finalidade

Este checklist detecta sinais de AI slop, abstraction bloat, drift, over-engineering, saída superficial e degradação de qualidade causada por agente.

Ele deve ser usado em planos, diffs, handoffs e reviews quando houver risco de o agente parecer produtivo enquanto aumenta entropia.

---

## Identificação

```text
Projeto:
Task/Issue:
Objeto avaliado: <plan | diff | completion | docs | arquitetura | outro>
Avaliador:
Data:
```

---

## 1. Escopo e causalidade

Verificar:

- [ ] cada mudança responde ao objetivo;
- [ ] não há “já que estou aqui”;
- [ ] não há refactor lateral;
- [ ] não há arquivos novos sem função clara;
- [ ] não há mudança cosmética misturada com feature;
- [ ] não há solução maior que o problema.

Sinais de slop:

```text
<sinais>
```

---

## 2. Evidência

Verificar:

- [ ] conclusões têm evidência;
- [ ] validações foram executadas ou lacunas declaradas;
- [ ] não há “parece funcionar” sem base;
- [ ] fontes foram registradas;
- [ ] hipóteses não foram tratadas como fatos;
- [ ] handoff não esconde incerteza.

---

## 3. Arquitetura por dor real

Verificar:

- [ ] abstrações novas têm dor real;
- [ ] interfaces novas têm justificativa;
- [ ] camadas novas reduzem risco real;
- [ ] mensageria/CQRS/event sourcing/microserviço não aparecem por hype;
- [ ] alternativa simples foi considerada;
- [ ] custo de contexto foi considerado.

Pergunta crítica:

```text
Essa complexidade paga aluguel agora?
```

---

## 4. Drift arquitetural

Verificar:

- [ ] boundaries foram respeitados;
- [ ] imports indevidos não apareceram;
- [ ] regra de domínio não foi duplicada;
- [ ] infra não vazou para domínio sem motivo;
- [ ] frontend não virou fonte de verdade indevida;
- [ ] documentação não contradiz código.

---

## 5. Contexto e navegação

Verificar:

- [ ] solução não espalha feature simples por arquivos demais;
- [ ] nomes são coerentes;
- [ ] estrutura segue padrão local;
- [ ] novo padrão não compete com padrão existente;
- [ ] agente não ignorou authority sources;
- [ ] contexto usado era necessário para decisão.

---

## 6. Dependências

Verificar:

- [ ] nenhuma dependência foi adicionada por conveniência;
- [ ] alternativa nativa/local foi considerada;
- [ ] supply chain/licença/manutenção foram consideradas;
- [ ] package não duplica capacidade existente;
- [ ] lockfile não contém ruído inexplicado.

---

## 7. Segurança

Verificar:

- [ ] input externo não foi confiado;
- [ ] auth não foi tratada superficialmente;
- [ ] secrets não aparecem;
- [ ] logs não vazam dados;
- [ ] frontend não é única barreira;
- [ ] dependência/IaC/cloud não abriu risco oculto.

---

## 8. Produção

Verificar:

- [ ] solução não é apenas de localhost;
- [ ] erro/falha parcial foi considerado;
- [ ] observabilidade mínima foi considerada;
- [ ] deploy/config/runtime foram considerados quando aplicável;
- [ ] banco real/cardinalidade real foram considerados;
- [ ] autoscaling não foi usado como argumento vazio.

---

## 9. Documentação e state

Verificar:

- [ ] docs foram atualizadas quando realidade mudou;
- [ ] docs não foram infladas sem necessidade;
- [ ] `PROJECT_STATE.md` não virou changelog;
- [ ] board não virou verdade técnica;
- [ ] ADR foi considerado para decisão arquitetural;
- [ ] handoff é útil para próxima sessão.

---

## 10. Linguagem suspeita

Sinais de alerta em texto do agente:

- [ ] “melhores práticas” sem contexto;
- [ ] “escalável” sem carga ou workload;
- [ ] “robusto” sem falhas consideradas;
- [ ] “simples” com muitos arquivos/camadas;
- [ ] “pronto para produção” sem observabilidade/validação;
- [ ] “testado” sem comando/evidência;
- [ ] “necessário” sem trade-off.

---

## 11. Veredito anti-slop

Escolher:

- [ ] limpo;
- [ ] aceitável com ressalvas;
- [ ] slop moderado — ajustar;
- [ ] slop alto — bloquear/replanejar.

Motivo:

```text
<motivo>
```

Ações obrigatórias:

- `<ação 1>`;
- `<ação 2>`.

Ações recomendadas:

- `<ação 1>`;
- `<ação 2>`.