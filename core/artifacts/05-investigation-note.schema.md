# Schema — Investigation Note

## Finalidade

A Investigation Note é o artefato canônico usado quando a task exige investigação factual, análise de contexto, leitura de repositório, diagnóstico ou pesquisa antes de qualquer implementação.

Seu papel é registrar o que foi descoberto, o que ainda é incerto, quais fontes foram consultadas e qual caminho parece mais adequado depois da investigação.

A Investigation Note existe para impedir que investigação desapareça dentro de conversa, memória volátil ou conclusão vaga.

---

## Quando deve ser usada

A Investigation Note deve ser usada quando a task:

- for R0 ou predominantemente read-only;
- exigir discovery antes de plan;
- envolver diagnóstico de bug, falha ou comportamento estranho;
- envolver leitura de repositório sem mutação;
- envolver consulta a documentação, MCP, board ou fonte externa;
- precisar produzir conhecimento antes de produzir código;
- terminar sem implementação, mas com achados relevantes.

---

## Papel no fluxo

No fluxo canônico, a Investigation Note pode aparecer:

1. antes do Execution Plan;
2. como saída principal de uma task R0;
3. como base para uma Escalation Note;
4. como insumo para Core Architect;
5. como suporte para atualização futura de `PROJECT_STATE.md`.

Ela não substitui o Execution Plan quando houver implementação.  
Ela fornece base factual para decidir se, como e onde implementar.

---

## Campos obrigatórios

### 1. Objetivo da investigação
Descrição direta do que a investigação precisava descobrir.

Pergunta que este campo responde:
- qual dúvida, hipótese ou problema motivou a investigação?

### 2. Contexto
Resumo do cenário que originou a investigação.

Perguntas que este campo responde:
- por que isso está sendo investigado?
- qual é o estado conhecido antes da investigação?
- que evento, dúvida ou sintoma disparou a análise?

### 3. Escopo investigado
Lista do que foi efetivamente analisado.

Pode incluir:
- diretórios;
- arquivos;
- módulos;
- commits;
- issues;
- board items;
- logs;
- documentação;
- integrações;
- comandos;
- fontes externas.

### 4. Fora de escopo
Lista do que não foi analisado ou não deveria ser concluído a partir desta investigação.

### 5. Fontes consultadas
Fontes usadas para sustentar os achados.

Podem incluir:
- authority files;
- authority commands;
- arquivos do repositório;
- documentação local;
- documentação externa;
- MCP read-only;
- GitHub Issues;
- GitHub Projects;
- logs;
- outputs de comandos.

### 6. Achados factuais
Lista objetiva do que foi encontrado.

Achado factual deve ser algo observado, lido, executado ou confirmado, não uma opinião solta.

### 7. Hipóteses
Interpretações plausíveis ainda não plenamente confirmadas.

Hipótese deve ser claramente separada de fato.

### 8. Lacunas e incertezas
O que ainda não foi possível confirmar.

### 9. Riscos percebidos
Riscos técnicos, operacionais, de segurança, arquitetura, escopo ou entropia identificados durante a investigação.

### 10. Recomendação
Direção sugerida com base nos achados.

Pode ser:
- seguir para Execution Plan;
- abrir Escalation Note;
- atualizar documentação;
- criar issue;
- pedir mais contexto;
- não implementar nada por enquanto.

---

## Campos recomendados

### 11. Classe de risco sugerida
Risco mais adequado após a investigação.

### 12. Áreas candidatas de impacto
Regiões do sistema que provavelmente seriam tocadas em uma implementação futura.

### 13. Pressões reais observadas
Indicar se a investigação encontrou pressão de:
- concorrência;
- throughput;
- latência;
- consistência;
- observabilidade;
- estado local;
- execução em cloud;
- segurança;
- custo de complexidade;
- entropia.

### 14. Próximos passos possíveis
Lista de caminhos concretos após a investigação.

### 15. Necessidade de atualização de estado
Indicar se os achados devem virar memória durável em `PROJECT_STATE.md` ou documentação local.

---

## O que a Investigation Note não deve ser

Não deve ser:

- dump de transcript;
- lista desorganizada de observações;
- conclusão sem fonte;
- opinião disfarçada de fato;
- substituto de plan;
- tentativa de implementar enquanto investiga;
- relatório longo sem decisão prática.

---

## Qualidade esperada

Uma boa Investigation Note deve ser:

- factual;
- organizada;
- separando fatos, hipóteses e lacunas;
- útil para decisão;
- curta o suficiente para ser lida;
- densa o suficiente para evitar reinvestigação desnecessária.

Uma Investigation Note ruim:

- mistura achado com opinião;
- não informa fontes;
- não explicita incertezas;
- não gera próximo passo claro;
- deixa a investigação presa à conversa.

---

## Relação com evidência

A Investigation Note deve obedecer ao Padrão de Evidência.

Isso significa que ela deve deixar claro:

- o que foi observado;
- onde foi observado;
- como foi confirmado;
- o que ainda não foi confirmado;
- que conclusão depende de hipótese.

Sem essa separação, a investigação perde valor operacional.

---

## Relação com Execution Plan

Quando a investigação indicar que a task deve virar implementação, a Investigation Note deve servir como insumo para o Execution Plan.

O Execution Plan deve aproveitar:

- achados factuais;
- riscos percebidos;
- áreas candidatas de impacto;
- lacunas;
- critérios de escalonamento.

A Investigation Note não deve virar implementação diretamente.

---

## Relação com Escalation Note

Quando a investigação revelar ambiguidade estrutural, risco acima do envelope ou necessidade de decisão estratégica, a saída correta pode ser uma Escalation Note.

Nesse caso, a Investigation Note fornece a base factual da escalada.

---

## Relação com PROJECT_STATE

Quando os achados forem duráveis para o projeto, a Investigation Note deve indicar atualização de `PROJECT_STATE.md`.

Exemplos de achados duráveis:

- limitação técnica confirmada;
- risco conhecido;
- decisão implícita descoberta;
- comando real confirmado;
- divergência entre documentação e realidade;
- ponto frágil recorrente;
- fato operacional relevante.

---

## Template canônico

```md
# Investigation Note

## Objetivo da investigação
<dúvida, hipótese ou problema investigado>

## Contexto
<cenário que motivou a investigação>

## Escopo investigado
- <item 1>
- <item 2>

## Fora de escopo
- <item 1>
- <item 2>

## Fontes consultadas
- <fonte 1>
- <fonte 2>

## Achados factuais
- <fato 1>
- <fato 2>

## Hipóteses
- <hipótese 1>
- <hipótese 2>

## Lacunas e incertezas
- <lacuna 1>
- <lacuna 2>

## Riscos percebidos
- <risco 1>
- <risco 2>

## Classe de risco sugerida
R0 | R1 | R2 | R3 | R4

## Áreas candidatas de impacto
- <área 1>
- <área 2>

## Pressões reais observadas
- <pressão 1>
- <pressão 2>

## Recomendação
<direção recomendada>

## Próximos passos possíveis
- <passo 1>
- <passo 2>

## Necessidade de atualização de estado
<sim | não | incerto>
```

---

## Declaração operacional curta

A Investigation Note transforma investigação em memória factual.  
Ela existe para que descoberta não vire conversa perdida, achismo ou reinvestigação futura.