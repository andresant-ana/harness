# Padrão de Evidência

## Finalidade

Este protocolo define o que conta como evidência aceitável dentro do harness.

Seu papel é impedir que o sistema trate:
- confiança verbal,
- inferência vaga,
- ou plausibilidade superficial

como substitutos de verificação real.

---

## Tese central

Toda saída relevante do sistema deve ser sustentada por evidência proporcional ao risco.

A pergunta correta não é apenas:
“isso parece certo?”

A pergunta correta é:
“o que foi efetivamente observado, executado, lido, validado ou demonstrado para sustentar isso?”

---

## O que conta como evidência

Evidência pode incluir:

- leitura factual de arquivo;
- resultado de comando executado;
- saída de build, test, lint ou format;
- resultado de busca estruturada;
- confirmação de authority source local;
- diff revisado;
- comportamento observado;
- lacuna explicitamente reconhecida;
- log, métrica ou artefato concreto;
- validação funcional proporcional.

Evidência não precisa ser sempre automática, mas precisa ser rastreável.

---

## O que não conta como evidência

Não conta como evidência:

- “provavelmente”;
- “deve estar funcionando”;
- “parece coerente”;
- “segui o padrão”;
- “o código parece correto”;
- “essa abordagem costuma funcionar”;
- qualquer linguagem confiante sem base factual correspondente.

---

## Regra de proporcionalidade

Quanto maior o risco:
- maior a exigência de evidência;
- maior a exigência de clareza sobre o que foi ou não validado;
- menor a tolerância a conclusão baseada em plausibilidade.

### R0
Pode aceitar evidência baseada em leitura factual e síntese clara.

### R1
Exige ao menos validação local proporcional e explicitação de limites.

### R2
Exige validação mais forte, Completion Packet robusto e review mais atento.

### R3
Exige evidência mais severa e, muitas vezes, validação estratégica antes de seguir.

### R4
Exige autorização explícita e tratamento fora do fluxo comum.

---

## Evidência por tipo de saída

### Execution Plan
Deve ser sustentado por:
- discovery suficiente;
- authority sources relevantes;
- leitura factual da topologia;
- hipótese operacional justificada.

### Completion Packet
Deve ser sustentado por:
- comandos executados;
- validações realizadas;
- leitura de diff;
- checagens efetivas;
- explicitação do que ficou sem validação.

### Review Report
Deve ser sustentado por:
- comparação com plan;
- leitura de mudança;
- risco identificado com base clara;
- pontos de bloqueio bem justificados.

### Escalation Note
Deve ser sustentada por:
- motivo real da escalada;
- impacto provável;
- opções percebidas;
- contexto factual suficiente para decisão.

---

## Regra da honestidade

A evidência não precisa ser perfeita.  
Mas a ausência dela precisa ser explicitada.

Uma saída honesta com lacunas declaradas é melhor do que uma saída “forte” construída sobre suposição silenciosa.

---

## Fórmula mínima de evidência

Toda entrega relevante deve conseguir responder:

1. o que foi verificado;
2. como foi verificado;
3. o que não foi verificado;
4. por que não foi verificado;
5. que risco isso deixa aberto.

Se uma entrega não consegue responder isso, ela está fraca.

---

## Relação com validação

Validação é um dos meios de produzir evidência, mas não o único.

Leitura factual, authority source, diff review e raciocínio causal documentado também podem produzir evidência, desde que não sejam usados para mascarar a falta de teste ou verificação quando estes seriam necessários.

---

## Relação com review

Review não deve aceitar linguagem elegante em vez de base factual.

O reviewer deve perguntar:
- isso foi realmente validado?
- ou isso só foi explicado de forma convincente?

---

## Relação com segurança e operação

Sempre que a task tocar:
- segurança,
- confiabilidade,
- execução em cloud,
- mudança de persistência,
- superfície operacional,

o padrão de evidência precisa subir.

Não basta “funcionar”.  
É preciso deixar claro o que foi realmente checado nessas dimensões.

---

## Declaração operacional curta

Evidência é tudo aquilo que permite confiar com base factual.  
O resto é retórica.  
O harness trabalha com evidência, não com retórica.