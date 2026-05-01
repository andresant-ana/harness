# Skill — Docker Container Baseline

## Finalidade

Esta skill orienta a revisão e criação de Dockerfiles, containers, imagens e execução local/CI baseada em container.

Seu papel é impedir que o agente trate Docker apenas como “funciona na minha máquina”, ignorando build context, camadas, usuário, secrets, portas, health checks, tamanho de imagem, segurança e runtime.

---

## Quando usar

Use esta skill quando a task envolver:

- Dockerfile;
- docker-compose;
- build de imagem;
- execução de container;
- container em CI;
- container em cloud;
- multi-stage build;
- imagem base;
- portas;
- volumes;
- variáveis de ambiente;
- health check;
- runtime resource;
- permissões dentro do container.

---

## Quando não usar

Não use esta skill quando:

- não houver container;
- a mudança for puramente documental;
- o projeto já tiver authority source clara e a task não alterar container;
- a análise adicionaria ruído em comando trivial.

---

## Tese central

Container não é só empacotamento.

Container define:

- runtime;
- dependências;
- isolamento;
- superfície de segurança;
- comportamento operacional;
- consumo de recurso;
- e portabilidade.

---

## Método

### 1. Identificar finalidade do container

Perguntar:

- é desenvolvimento local?
- CI?
- produção?
- teste?
- worker?
- aplicação web?
- banco local?

A finalidade muda os critérios.

---

### 2. Revisar imagem base

Verificar:

- imagem é adequada?
- versão está pinada?
- é leve o suficiente?
- é mantida?
- possui vulnerabilidades conhecidas?
- usa variante runtime em produção, não SDK desnecessariamente?

---

### 3. Revisar build context

Verificar:

- `.dockerignore`;
- arquivos copiados;
- segredos acidentais;
- cache de camadas;
- dependências restauradas antes do copy total quando aplicável;
- imagem final sem artefatos de build desnecessários.

---

### 4. Revisar runtime

Perguntar:

- roda como root?
- porta exposta é correta?
- env vars são necessárias?
- há health check?
- working directory está claro?
- entrypoint/cmd faz sentido?
- logs vão para stdout/stderr?

---

### 5. Revisar segurança

Verificar:

- segredo não está no Dockerfile;
- segredo não entra em build arg inseguro;
- usuário não-root quando possível;
- permissões mínimas;
- imagem base confiável;
- sem pacotes desnecessários.

---

### 6. Revisar operação

Perguntar:

- há limite de memória/CPU no runtime alvo?
- app lida com SIGTERM?
- readiness/liveness são coerentes?
- storage local é efêmero?
- volume é realmente necessário?

---

## Output esperado

```md
# Docker Container Baseline Review

## Finalidade
<dev | test | CI | produção | worker | outro>

## Arquivos analisados
- <Dockerfile>
- <compose>
- <dockerignore>

## Imagem base
<análise curta>

## Build context
<análise curta>

## Runtime
<porta, user, env, entrypoint, logs, health>

## Segurança
<root, secrets, packages, imagem base>

## Operação
<resource, signal, storage, health>

## Veredito
<suficiente | ajustar | escalar>

## Risco residual
<risco que permanece>
```

---

## Checklist de qualidade

Antes de aceitar, verificar:

- `.dockerignore` existe ou foi considerado?
- imagem base é adequada?
- versão está controlada?
- multi-stage faz sentido?
- segredo não entra na imagem?
- container não roda como root sem necessidade?
- porta/entrypoint estão corretos?
- logs vão para stdout/stderr?
- health check é coerente?
- storage local efêmero foi considerado?

---

## Critérios de escalonamento

Escalar quando:

- container for produção;
- houver segredo no build/runtime;
- imagem base tiver risco alto;
- container exigir privilégio elevado;
- health check puder derrubar serviço;
- resource limits forem críticos;
- decisão envolver runtime cloud.

---

## Anti-patterns

Evitar:

- usar imagem SDK em produção sem necessidade;
- copiar repo inteiro sem `.dockerignore`;
- colocar secret no Dockerfile;
- rodar como root por padrão;
- instalar pacote sem necessidade;
- health check ornamental;
- volume para estado crítico sem decisão;
- assumir filesystem persistente em container;
- tratar container como VM.

---

## Declaração operacional curta

Container bom é pequeno, explícito, seguro e operável.  
Docker que só funciona localmente ainda não é baseline de produção.