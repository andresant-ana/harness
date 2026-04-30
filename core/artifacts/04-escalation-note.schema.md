# Schema — Escalation Note

## Finalidade

A Escalation Note é o artefato canônico usado quando a execução atinge um ponto fora do envelope legítimo do executor.

Seu papel é organizar a dúvida, o risco ou a decisão pendente de forma que o humano operador ou o Core Architect consigam arbitrar com clareza.

Ela existe para impedir dois erros opostos:
- o executor continuar decidindo sozinho quando já deveria ter parado;
- ou o executor “escalar” despejando contexto bruto sem organizar o problema.

---

## Quando deve ser usada

Deve ser usada quando houver:

- ambiguidade estrutural;
- risco acima do esperado;
- conflito entre plan e realidade;
- necessidade de redefinição de escopo;
- decisão arquitetural relevante;
- falta de autoridade para seguir;
- consumo de budget sem convergência;
- necessidade de autorização sensível.

---

## Papel no fluxo

No fluxo canônico, a Escalation Note:
1. interrompe improviso;
2. transforma a dúvida em problema legível;
3. sobe a questão para a camada certa;
4. preserva rastreabilidade;
5. evita que o executor esconda aumento de risco.

---

## Campos obrigatórios

### 1. Contexto da escalada
Resumo do cenário em que a escalada surgiu.

### 2. Motivo da escalada
Explicação objetiva do porquê o executor não deve seguir sozinho.

### 3. Impacto provável
O que está em jogo caso a decisão seja tomada de forma errada ou tardia.

### 4. Opções percebidas
Quais caminhos o executor conseguiu identificar.

### 5. Trade-offs iniciais
O que se ganha e se perde em cada opção relevante.

### 6. Risco percebido
Qual risco principal está dirigindo a escalada.

### 7. Recomendação do executor
Se houver base factual suficiente, o executor pode sugerir uma direção.

### 8. Decisão pendente
Qual é exatamente a pergunta que precisa ser respondida.

---

## Campos recomendados

### 9. Classe de risco atualizada
Se a escalada decorre de aumento ou correção de risco.

### 10. Authority sources consultadas
Quais fontes locais foram usadas antes da escalada.

### 11. Pressões reais tocadas
Se a escalada envolve:
- arquitetura;
- concorrência;
- escala;
- observabilidade;
- execução em cloud;
- segurança;
- custo de complexidade;
- estado local;
- boundary entre módulos.

### 12. Consequência de não decidir agora
O que acontece se a decisão for adiada.

---

## O que a Escalation Note não deve ser

Não deve ser:
- pedido genérico de ajuda;
- texto vago;
- despejo de transcript;
- dramatização;
- abandono passivo da task;
- racionalização elegante de falta de discovery.

---

## Qualidade esperada

Uma boa Escalation Note deve ser:
- curta;
- factual;
- orientada a decisão;
- explícita quanto ao motivo da escalada;
- clara sobre a pergunta pendente.

Uma nota ruim:
- não diz qual decisão precisa ser tomada;
- mistura várias dúvidas diferentes;
- não registra impacto;
- não organiza trade-off.

---

## Template canônico

```md
# Escalation Note

## Contexto da escalada
<situação em que a escalada surgiu>

## Motivo da escalada
<por que o executor não deve seguir sozinho>

## Classe de risco atualizada
R0 | R1 | R2 | R3 | R4

## Authority sources consultadas
- <fonte 1>
- <fonte 2>

## Impacto provável
- <impacto 1>
- <impacto 2>

## Opções percebidas
- <opção 1>
- <opção 2>

## Trade-offs iniciais
- <trade-off 1>
- <trade-off 2>

## Risco percebido
- <risco 1>
- <risco 2>

## Pressões reais tocadas
- <pressão 1>
- <pressão 2>

## Recomendação do executor
<recomendação, se houver base suficiente>

## Decisão pendente
<pergunta exata que precisa de arbitragem>

## Consequência de não decidir agora
<efeito provável do adiamento>
```

---

## Declaração operacional curta
A Escalation Note organiza a dúvida antes de subir.
Ela existe para que escalonamento seja sinal de maturidade, não de improviso.