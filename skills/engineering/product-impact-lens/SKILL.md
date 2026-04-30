# Skill — Product Impact Lens

## Finalidade

Esta skill orienta a leitura de impacto de produto em decisões técnicas.

Seu papel é impedir que o agente trate toda task como problema puramente técnico, ignorando valor para usuário, negócio, fluxo, prioridade, custo de oportunidade e critério de aceite real.

A skill conecta engenharia com propósito.

---

## Quando usar

Use esta skill quando a task envolver:

- feature nova;
- alteração de fluxo de usuário;
- decisão entre escopos;
- dúvida sobre MVP;
- trade-off entre qualidade e entrega;
- priorização;
- UX ou frontend;
- API que serve caso de uso real;
- complexidade que precisa ser justificada por valor;
- definição de pronto.

---

## Quando não usar

Não use esta skill quando:

- a task for puramente interna e mecânica;
- não houver impacto de produto;
- o critério de aceite já estiver claro e fechado;
- o uso da skill só adicionaria discussão abstrata.

---

## Tese central

Boa engenharia entrega valor real com custo proporcional.

Nem toda melhoria técnica melhora o produto agora.  
Nem toda entrega rápida é engenharia responsável.

A lente de produto pergunta:

“isso ajuda o usuário, o negócio ou a evolução do sistema de forma proporcional ao custo?”

---

## Método

### 1. Identificar usuário ou consumidor

Perguntar:

- quem se beneficia da mudança?
- usuário final?
- operador?
- desenvolvedor futuro?
- sistema externo?
- negócio?
- suporte?

---

### 2. Identificar problema de produto

Declarar:

- qual dor do usuário ou negócio está sendo resolvida;
- qual comportamento precisa mudar;
- qual resultado esperado;
- qual métrica, sinal ou feedback indicaria sucesso.

---

### 3. Separar necessário de desejável

Classificar itens como:

- necessário para aceite;
- desejável;
- follow-up;
- fora de escopo;
- over-engineering.

---

### 4. Avaliar custo de oportunidade

Perguntar:

- esta complexidade vale agora?
- existe solução menor que entrega valor suficiente?
- o ganho justifica atrasar outras frentes?
- estamos otimizando algo que ainda não dói?

---

### 5. Conectar com critério de aceite

Garantir que implementação e validação conversem com resultado real.

Critério técnico sem critério de produto pode virar entrega sem valor.

---

### 6. Recomendar escopo

Sugerir:

- escopo mínimo responsável;
- o que deixar para depois;
- que risco aceitar;
- que follow-up registrar.

---

## Output esperado

```md
# Product Impact Lens

## Consumidor da mudança
<usuário, operador, dev, sistema externo ou negócio>

## Dor ou objetivo de produto
<problema que a mudança resolve>

## Resultado esperado
<como saber que gerou valor>

## Necessário para aceite
- <item 1>
- <item 2>

## Desejável / follow-up
- <item 1>
- <item 2>

## Fora de escopo
- <item 1>
- <item 2>

## Custo de oportunidade
<leitura curta>

## Recomendação de escopo
<escopo recomendado>
```

---

## Checklist de qualidade

Antes de seguir, verificar:

- o consumidor da mudança está claro?
- a dor é real?
- o critério de aceite representa valor?
- há itens desejáveis disfarçados de obrigatórios?
- há over-engineering técnico sem ganho de produto?
- o escopo mínimo responsável foi identificado?
- o follow-up foi separado do agora?

---

## Critérios de escalonamento

Escalar quando:

- a decisão depender de prioridade de negócio;
- houver conflito entre qualidade técnica e prazo;
- o escopo estiver ambíguo;
- o critério de aceite for fraco;
- a task técnica parecer desconectada de valor;
- o agente estiver prestes a implementar suposição de produto.

---

## Anti-patterns

Evitar:

- construir feature sem usuário claro;
- confundir melhoria técnica com valor imediato;
- expandir escopo para “ficar completo”;
- implementar edge cases sem evidência;
- resolver problema de produto com arquitetura pesada;
- ignorar operação e suporte como consumidores reais;
- aceitar ticket vago como especificação suficiente.

---

## Declaração operacional curta

Produto dá direção para a técnica.  
A solução boa entrega valor real sem complexidade desproporcional.