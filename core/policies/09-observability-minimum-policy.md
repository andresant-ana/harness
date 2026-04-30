# Política de Observabilidade Mínima

## Finalidade

Esta policy define o nível mínimo de observabilidade esperado para mudanças relevantes em projetos operados pelo harness.

Seu papel é impedir que o sistema entregue funcionalidades invisíveis em produção, difíceis de diagnosticar ou dependentes apenas de reprodução local.

---

## Tese central

Se não é possível observar, não é possível operar com confiança.

Observabilidade não é luxo de sistema grande.  
É condição mínima para entender se uma mudança funciona, falha, degrada ou causa efeito colateral.

---

## Regra operacional principal

Toda mudança relevante deve considerar se altera ou exige:

- logs;
- métricas;
- tracing;
- health checks;
- sinais de erro;
- sinais de degradação;
- visibilidade de dependências;
- diagnóstico de falha.

Nem toda task precisa adicionar instrumentação nova.  
Mas toda task relevante deve avaliar se a observabilidade existente é suficiente.

---

## Dimensões mínimas

### 1. Logs

Logs devem ajudar a entender eventos importantes sem vazar dado sensível.

Bons logs:
- explicam transições relevantes;
- registram falhas com contexto suficiente;
- evitam ruído excessivo;
- não expõem segredos;
- não registram dado pessoal sem necessidade.

### 2. Métricas

Métricas devem ajudar a perceber comportamento agregado.

Podem cobrir:
- latência;
- taxa de erro;
- throughput;
- contagem de eventos;
- saturação;
- retry;
- falha de dependência;
- tempo de processamento.

### 3. Tracing

Tracing é relevante quando há fluxo distribuído, integração externa ou caminho com múltiplas etapas.

Não precisa ser usado em toda task, mas deve ser considerado quando a causalidade atravessa boundaries.

### 4. Health checks

Health checks devem refletir estado útil.

A política deve distinguir:
- liveness;
- readiness;
- dependências necessárias;
- capacidade real de aceitar tráfego.

Health check ruim pode derrubar serviço saudável ou manter serviço incapaz recebendo tráfego.

### 5. Erros acionáveis

Erros devem ser compreensíveis o suficiente para orientar diagnóstico.

Mensagens genéricas, silenciosas ou enganosas reduzem operabilidade.

---

## Quando observabilidade é obrigatória

A observabilidade deve ser tratada com mais rigor quando a task toca:

- integração externa;
- processamento assíncrono;
- fila;
- job;
- autenticação;
- autorização;
- pagamento;
- persistência crítica;
- cloud/runtime;
- fluxo de usuário importante;
- comportamento sob carga;
- operação em produção.

---

## Quando observabilidade nova pode não ser necessária

Pode não ser necessário adicionar observabilidade nova quando:

- a mudança é puramente interna e local;
- já existe instrumentação suficiente;
- a alteração não muda comportamento operacional;
- o custo de instrumentação excede o valor real;
- a task é R1 simples e reversível.

Mas essa decisão deve ser consciente, não por esquecimento.

---

## Relação com segurança

Observabilidade não pode vazar segredo ou dado sensível.

Logs, traces e métricas devem evitar:

- tokens;
- senhas;
- connection strings;
- payloads sensíveis;
- dados pessoais desnecessários;
- headers de autorização;
- detalhes internos que ampliem risco.

---

## Relação com produção

Uma solução production-minded precisa ser observável.

O sistema deve perguntar:

- como saberemos que isso está funcionando?
- como saberemos que está falhando?
- como diferenciaremos erro de usuário, erro de dependência e erro de sistema?
- que sinal apareceria em produção se isso quebrasse?

---

## Relação com Completion Packet

Quando a task tiver impacto operacional, o Completion Packet deve registrar:

- observabilidade considerada;
- observabilidade adicionada ou preservada;
- lacunas conhecidas;
- recomendação de follow-up, se necessário.

---

## Relação com Review

O reviewer deve bloquear ou pedir reavaliação quando:

- fluxo crítico fica invisível;
- erro relevante é engolido;
- log vaza informação sensível;
- mudança operacional não possui diagnóstico plausível;
- health check foi alterado sem compreensão;
- observabilidade foi tratada como detalhe irrelevante.

---

## Observabilidade mínima por risco

### R0
Pode apenas registrar achados sobre ausência ou presença de observabilidade.

### R1
Observabilidade nova raramente é obrigatória, mas não deve ser degradada.

### R2
Impacto operacional deve ser avaliado explicitamente.

### R3
Observabilidade deve ser parte do plan e do review.

### R4
Exige tratamento excepcional e autorização.

---

## Anti-patterns

Evitar:

- logar tudo;
- logar nada;
- logar segredo;
- criar métrica sem uso claro;
- criar trace ornamental;
- tratar health check como ping trivial;
- assumir que teste local substitui sinal de produção.

---

## Declaração operacional curta

Observabilidade mínima é o direito de enxergar o sistema.  
Sem sinal, não há operação confiável.  
O harness não aceita mudança relevante completamente invisível.