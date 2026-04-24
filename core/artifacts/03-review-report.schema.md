# Schema — Review Report

## Finalidade

O Review Report é o artefato canônico de revisão crítica da mudança, do plan ou do encerramento da task.

Seu papel é registrar, com clareza, se a entrega:
- está aderente ao problema;
- respeitou o plan;
- mantém qualidade suficiente;
- introduziu risco ou slop;
- ou precisa ser bloqueada, reavaliada ou completada.

---

## Quando deve ser usado

Deve ser usado quando houver:
- revisão de plan;
- revisão de implementação;
- revisão de completion packet;
- revisão de mudança sensível;
- revisão conservadora antes de merge ou fechamento humano.

---

## Papel no fluxo

No fluxo canônico, o Review Report:
1. protege o sistema de autoconfiança do executor;
2. força leitura crítica da mudança;
3. explicita bloqueios, lacunas e riscos;
4. preserva honestidade do processo;
5. ajuda o humano a decidir com melhor base.

---

## Campos obrigatórios

### 1. Objeto do review
Indicar se o review incide sobre:
- Execution Plan;
- implementação;
- Completion Packet;
- ou combinação desses.

### 2. Escopo revisado
Que parte da mudança ou do artefato foi efetivamente analisada.

### 3. Leitura geral
Síntese curta da qualidade percebida.

### 4. Aderência ao plan
Se a mudança seguiu, distorceu ou ignorou o plan.

### 5. Pontos fortes
O que foi bem resolvido.

### 6. Pontos de atenção
O que ainda exige cuidado ou acompanhamento.

### 7. Bloqueios
Problemas suficientemente sérios para impedir aprovação.

### 8. Lacunas de evidência
O que não foi sustentado com evidência suficiente.

### 9. Risco residual
Riscos que permanecem mesmo que a mudança seja aceita.

### 10. Veredito
Faixa final do review.

Valores recomendados:
- aprovado;
- aprovado com ressalvas;
- reavaliar;
- bloquear.

---

## Campos recomendados

### 11. Coerência arquitetural
Se a mudança preserva ou degrada a coerência do sistema.

### 12. Risco de slop ou entropia
Se há duplicação, abstração prematura, espalhamento excessivo ou degradação estrutural.

### 13. Pressões reais observadas
Se a mudança tocou ou ignorou:
- concorrência;
- escala;
- falha parcial;
- observabilidade;
- runtime;
- segurança;
- custo de complexidade.

### 14. Recomendações objetivas
Ações concretas para melhorar a qualidade da entrega.

---

## O que o Review Report não deve ser

Não deve ser:
- parecer decorativo;
- reforço emocional do executor;
- texto ambíguo que evita tomar posição;
- dump de observações sem hierarquia;
- lista infinita de detalhes menores sem veredito claro.

---

## Qualidade esperada

Um bom Review Report deve ser:
- conservador o suficiente para proteger o sistema;
- claro o suficiente para orientar decisão;
- honesto sobre o que foi ou não revisado;
- objetivo no veredito;
- útil para follow-up.

Um review ruim:
- comenta muito e decide pouco;
- é elegante demais e preciso de menos;
- não diferencia ressalva de bloqueio;
- não conecta problema a impacto.

---

## Template canônico

```md
# Review Report

## Objeto do review
<execution plan | implementação | completion packet | combinação>

## Escopo revisado
<o que foi efetivamente revisado>

## Leitura geral
<leitura sintética da qualidade>

## Aderência ao plan
<alta | parcial | baixa | não aplicável>

## Pontos fortes
- <ponto 1>
- <ponto 2>

## Pontos de atenção
- <ponto 1>
- <ponto 2>

## Bloqueios
- <bloqueio 1>
- <bloqueio 2>

## Lacunas de evidência
- <lacuna 1>
- <lacuna 2>

## Coerência arquitetural
<avaliacão curta>

## Risco de slop ou entropia
<avaliacão curta>

## Pressões reais observadas
- <pressão 1>
- <pressão 2>

## Risco residual
- <risco 1>
- <risco 2>

## Recomendações objetivas
- <ação 1>
- <ação 2>

## Veredito
<aprovado | aprovado com ressalvas | reavaliar | bloquear>
```

---

## Declaração operacional curta
O Review Report existe para proteger a qualidade do sistema.
Ele não serve para validar ego nem para comentar sem decidir.
