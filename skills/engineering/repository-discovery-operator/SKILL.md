# Skill — Repository Discovery Operator

## Finalidade

Esta skill orienta o discovery de repositório antes de mutação, planejamento ou review.

Seu papel é ajudar o agente a entender a topologia local, authority sources, comandos reais, padrões existentes e áreas de impacto sem inflar contexto desnecessariamente.

---

## Quando usar

Use esta skill quando:

- iniciar task em repositório desconhecido;
- precisar produzir Execution Plan;
- houver dúvida sobre estrutura local;
- a task tocar múltiplos arquivos;
- houver risco de editar área errada;
- houver necessidade de localizar authority commands;
- o agente precisar entender convenções antes de agir;
- houver divergência entre documentação e código.

---

## Quando não usar

Não use esta skill quando:

- a task for trivial e arquivo-alvo já estiver claro;
- o workspace já tiver sido descoberto recentemente;
- o uso da skill só repetiria leitura já feita;
- a pergunta for puramente externa e não depender do repo.

---

## Tese central

Discovery não é ler tudo.

Discovery é construir mapa suficiente para agir com precisão.

O agente deve ler com intenção, não com ansiedade.

---

## Método

### 1. Definir pergunta de discovery

Antes de abrir arquivos, declarar:

- o que precisamos descobrir?
- por que isso importa?
- como essa informação mudará o plano?
- que risco existe se não descobrirmos?

---

### 2. Mapear estrutura superficial

Observar:

- diretórios principais;
- arquivos de solução/projeto;
- package/config files;
- README;
- docs;
- scripts;
- CI/CD;
- arquivos de harness/workspace;
- testes.

---

### 3. Localizar authority sources

Procurar:

- `README.md`;
- `PROJECT_STATE.md`;
- `WORKSPACE_GUIDE.md`;
- `AUTHORITY_SOURCES.md`;
- `LOCAL_COMMANDS.md`;
- `DONE_CRITERIA.md`;
- `OPERATIONAL_REALITY.md`;
- ADRs;
- configs reais;
- pipeline definitions.

---

### 4. Localizar authority commands

Identificar comandos reais para:

- restore/install;
- build;
- test;
- lint;
- format;
- typecheck;
- run local;
- migrations;
- docker;
- CI.

Não inventar comando se o projeto define outro.

---

### 5. Identificar área candidata de impacto

Localizar:

- módulo;
- feature;
- endpoint;
- componente;
- query;
- migration;
- teste;
- config;
- documentação relacionada.

---

### 6. Ler por proximidade causal

Depois de localizar a área provável, ler:

- arquivo alvo;
- vizinhos diretos;
- testes relacionados;
- contratos;
- config associada;
- documentação local.

Evitar abrir arquivos distantes sem hipótese.

---

### 7. Registrar lacunas

Se algo importante não for encontrado, registrar:

- comando ausente;
- documentação ausente;
- state ausente;
- teste ausente;
- arquitetura incerta;
- risco de suposição.

---

## Output esperado

A saída pode ser incorporada ao Execution Plan ou virar Investigation Note.

Formato recomendado:

```md
# Repository Discovery Summary

## Pergunta de discovery
<o que precisava ser descoberto>

## Estrutura relevante
- <item 1>
- <item 2>

## Authority sources encontradas
- <fonte 1>
- <fonte 2>

## Authority commands encontrados
- <comando 1>
- <comando 2>

## Área candidata de impacto
- <área 1>
- <área 2>

## Convenções observadas
- <convenção 1>
- <convenção 2>

## Lacunas
- <lacuna 1>
- <lacuna 2>

## Implicação para o plano
<como o discovery muda ou sustenta o próximo passo>
```

---

## Checklist de qualidade

Antes de encerrar discovery, confirmar:

- a pergunta inicial foi respondida?
- authority sources foram procuradas?
- comandos reais foram identificados?
- área de impacto está delimitada?
- convenções locais foram observadas?
- lacunas foram declaradas?
- o contexto foi suficiente sem leitura massiva?
- o próximo passo ficou mais claro?

---

## Critérios de escalonamento

Escalar ou pausar quando:

- authority sources contradizem o código;
- comandos reais não existem ou não funcionam;
- a área de impacto é maior que o esperado;
- há risco R3/R4;
- a documentação local está obsoleta;
- o projeto está inconsistente demais para planejar com segurança.

---

## Anti-patterns

Evitar:

- abrir o repositório inteiro sem pergunta;
- confiar só no nome dos arquivos;
- ignorar README e state;
- inventar comandos;
- seguir padrão genérico da stack contra convenção local;
- ler muito e decidir pouco;
- usar discovery para adiar execução indefinidamente.

---

## Declaração operacional curta

Discovery bom reduz incerteza.  
Ele lê o suficiente para agir com precisão, não o bastante para soterrar a task.