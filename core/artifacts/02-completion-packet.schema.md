# Schema — Completion Packet

## Finalidade

O Completion Packet é o artefato canônico de encerramento da task.

Seu papel é preservar continuidade, honestidade e rastreabilidade ao final da execução, registrando:
- o que foi feito;
- o que foi validado;
- o que não foi validado;
- que risco permanece;
- e o que ainda depende de continuidade.

---

## Quando deve ser usado

Deve ser usado ao final de toda task relevante que tenha passado por:
- plan;
- execução;
- validação;
- ou review.

Em tasks muito pequenas, ele pode ser mais enxuto.  
Em tasks moderadas ou sensíveis, ele deve ser explícito.

---

## Papel no fluxo

No fluxo canônico, o Completion Packet:
1. sucede execução e validação;
2. resume a mudança de forma objetiva;
3. prepara review final e continuidade;
4. impede encerramento verbal vazio;
5. registra verdade factual do estado final da task.

---

## Campos obrigatórios

### 1. Resumo da entrega
Síntese objetiva do que foi entregue ou alterado.

### 2. O que foi feito
Lista factual das mudanças relevantes.

### 3. O que não foi feito
Tudo que ficou explicitamente fora da entrega real, mesmo que estivesse no horizonte inicial.

### 4. Arquivos ou áreas tocadas
Resumo das regiões alteradas no repositório.

### 5. Validações realizadas
Tudo que foi efetivamente rodado, lido, verificado ou comparado.

### 6. Validações não realizadas
O que não foi verificado e por quê.

### 7. Riscos remanescentes
Risco técnico, operacional, de segurança, de regressão ou de continuidade que ainda permanece.

### 8. Divergências em relação ao plan
Quais partes saíram do plan e por que.

### 9. Impacto em documentação e state
Se a task:
- exigiu atualização de state;
- alterou authority source;
- mudou operational reality;
- ou deixou follow-up documental.

### 10. Próximo passo recomendado
Qual é a continuação natural mais provável após a task.

---

## Campos recomendados

### 11. Classe de risco encerrada
Classe final com que a task efetivamente terminou.

### 12. Pressões reais tocadas
Indicar se a task tocou:
- concorrência;
- escala;
- falha parcial;
- observabilidade;
- runtime;
- execution model;
- dependência externa;
- segurança;
- custo de complexidade.

### 13. Estado do review
Se a task:
- já foi revisada;
- precisa de review;
- foi aprovada com ressalvas;
- ou precisa de reavaliação.

### 14. Necessidade de escalonamento posterior
Se a execução resolveu a task, mas deixou uma decisão estrutural pendente.

---

## O que o Completion Packet não deve ser

Não deve ser:
- narrativa triunfal;
- texto persuasivo;
- lista vaga de “ajustes realizados”;
- release note genérica;
- tentativa de esconder ausência de validação.

---

## Qualidade esperada

Um bom Completion Packet deve ser:
- factual;
- honesto;
- legível;
- curto o suficiente para ser útil;
- denso o suficiente para preservar continuidade.

Um packet ruim:
- não explicita o que ficou aberto;
- não registra lacunas;
- usa linguagem bonita para esconder incerteza;
- não conecta mudança a validação.

---

## Template canônico

```md
# Completion Packet

## Resumo da entrega
<resumo objetivo da mudança>

## O que foi feito
- <item 1>
- <item 2>

## O que não foi feito
- <item 1>
- <item 2>

## Arquivos ou áreas tocadas
- <área ou arquivo 1>
- <área ou arquivo 2>

## Validações realizadas
- <validação 1>
- <validação 2>

## Validações não realizadas
- <lacuna 1>
- <lacuna 2>

## Riscos remanescentes
- <risco 1>
- <risco 2>

## Divergências em relação ao plan
- <divergência 1>
- <divergência 2>

## Impacto em documentação e state
- <impacto 1>
- <impacto 2>

## Pressões reais tocadas
- <pressão 1>
- <pressão 2>

## Estado do review
<pendente | revisado | aprovado com ressalvas | outro>

## Próximo passo recomendado
<próxima ação mais natural>
```

---

## Declaração operacional curta
O Completion Packet encerra a execução sem apagar a verdade.
Ele existe para impedir que a task “termine” sem deixar memória útil e honesta.