# Política de MCP

## Finalidade

Esta policy define como o harness deve usar MCP para leitura, consulta, contexto externo e, em casos excepcionais, ações além do repositório local.

Seu papel é impedir:
- integração por entusiasmo;
- ampliação prematura de autoridade;
- dependência excessiva de contexto externo;
- escrita sensível sem governança;
- e confusão entre conveniência e necessidade.

---

## Tese central

MCP é instrumento de ampliação controlada de contexto e capacidade.  
Não é licença para expandir autonomia sem limites.

A engenharia adota MCP com postura:
- conservadora;
- proporcional;
- rastreável;
- e guiada por necessidade real.

---

## Regra operacional principal

MCP deve entrar primeiro como **leitura confiável de estado externo**.

A política padrão da engenharia é:
1. leitura antes de escrita;
2. redução de incerteza antes de automação;
3. governança antes de expansão de autoridade.

---

## Usos legítimos de MCP no caminho padrão

São usos legítimos no início da engenharia:

- leitura de issues e PRs;
- leitura de board e GitHub Projects;
- leitura de documentação externa confiável;
- leitura de observabilidade;
- leitura de cloud metadata;
- leitura de estado organizacional ou operacional relevante para a task.

Esses usos são legítimos porque reduzem incerteza sem ampliar risco de mutação.

---

## Usos não legítimos por padrão

Não pertencem ao caminho padrão:

- escrita sensível em plataformas externas;
- mutação de produção;
- alteração de segredo;
- operação destrutiva;
- fechamento automático de fluxos com impacto real;
- automação write por conveniência.

Esses usos podem existir no futuro, mas exigem governança e maturidade maiores.

---

## Princípio read-only first

Toda nova integração MCP deve ser tratada, por padrão, como candidata a modo read-only.

A promoção para qualquer forma de escrita exige:
- necessidade real;
- caso de uso claro;
- matriz de permissão definida;
- risco entendido;
- trusted integration registrada;
- e validação humana explícita.

---

## Trusted integrations

Nenhuma integração MCP relevante deve ser tratada como confiável apenas porque “funciona”.

Para ser trusted integration, a integração precisa ter:
- dono claro;
- superfície conhecida;
- modo permitido definido;
- risco classificado;
- agentes autorizados definidos;
- valor operacional comprovado;
- registro em governance.

---

## Relação com GitHub Projects e board

GitHub Projects é uso legítimo de MCP em modo read-only para:
- saber o que ainda falta;
- saber o que já foi feito;
- ler ordem de trabalho;
- ler estado organizacional da task;
- conectar task com backlog e priorização.

Mas board não substitui:
- `PROJECT_STATE.md`;
- authority sources do projeto;
- ou entendimento técnico do repositório.

Board informa estado de trabalho.  
Workspace informa estado técnico.

---

## Relação com classes de risco

### R0
Leitura via MCP é amplamente compatível.

### R1
Leitura externa pode enriquecer contexto sem grande atrito.

### R2
MCP pode ser importante para reduzir incerteza factual, desde que não substitua discovery local.

### R3
Leitura externa ainda é útil, mas qualquer escrita já exige forte cautela.

### R4
MCP write sensível continua fora do fluxo padrão.

---

## Relação com evidência

Leitura via MCP pode gerar evidência factual quando:
- a fonte é confiável;
- a consulta é relevante;
- a interpretação é cuidadosa;
- o resultado é usado para reduzir incerteza real.

MCP não deve ser usado para empilhar contexto irrelevante só porque está disponível.

---

## Relação com contexto

MCP não substitui authority source local.  
Ele complementa.

O sistema deve evitar a tentação de:
- consultar tudo;
- importar contexto demais;
- tratar fonte externa como se fosse mais importante que a verdade do projeto.

---

## Condições para escrita futura

Escrita via MCP só pode ser promovida quando houver:

1. caso de uso recorrente;
2. valor operacional claro;
3. blast radius compreendido;
4. limites de permissão por agente;
5. política formal escrita;
6. confiança suficiente na integração;
7. aprovação explícita do humano.

Sem isso, o caminho correto continua sendo leitura.

---

## Sinais de mau uso de MCP

O uso está ruim quando:
- a integração entrou só por hype;
- o agente consulta contexto externo sem propósito claro;
- o board começa a substituir entendimento técnico do projeto;
- MCP vira desculpa para não manter state local;
- escrita é proposta cedo demais;
- a superfície externa fica maior do que o problema justifica.

---

## Declaração operacional curta

MCP amplia poder.  
Poder sem governança vira risco.  
O harness usa MCP primeiro para enxergar melhor, não para agir mais cedo.