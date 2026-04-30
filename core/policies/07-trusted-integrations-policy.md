# Política de Integrações Confiáveis

## Finalidade

Esta policy define os critérios para uma integração ser considerada confiável dentro da engenharia de harness.

Seu papel é impedir que ferramentas, APIs, MCP servers, plugins, CLIs, dashboards ou serviços externos sejam usados como se fossem seguros apenas porque estão disponíveis ou funcionam tecnicamente.

---

## Tese central

Integração funcional não é integração confiável.

Uma integração só deve ser tratada como confiável quando sua superfície, permissões, riscos, finalidade, outputs e limites forem conhecidos e registrados.

---

## Regra operacional principal

Nenhuma integração deve receber confiança operacional sem responder:

1. qual problema ela resolve;
2. que dados ela lê;
3. que dados ela escreve;
4. que permissões possui;
5. qual é seu blast radius;
6. que agente ou fluxo pode usá-la;
7. que tipo de evidência ela produz;
8. quais são seus limites;
9. como falha;
10. quando deve ser evitada.

---

## O que pode ser integração

Podem ser integrações:

- MCP servers;
- GitHub;
- GitHub Projects;
- cloud providers;
- observability platforms;
- CI/CD systems;
- package registries;
- documentation sources;
- issue trackers;
- plugins do runtime;
- CLIs externas;
- bancos, filas ou storage acessados por tooling.

---

## Níveis de confiança

### 1. Experimental
Integração ainda em avaliação.

Características:
- uso limitado;
- sem dependência crítica;
- sem write sensível;
- precisa de supervisão humana.

### 2. Read-only confiável
Integração aprovada para leitura controlada.

Características:
- fonte útil;
- permissões limitadas;
- escopo claro;
- sem mutação.

### 3. Operacional restrita
Integração pode executar ações limitadas e não sensíveis.

Características:
- outputs previsíveis;
- blast radius baixo;
- autorização definida;
- logs ou rastreabilidade.

### 4. Sensível
Integração toca produção, segredos, deploy, permissões, dados reais ou efeitos externos relevantes.

Características:
- exige governança forte;
- não pertence à autonomia padrão;
- precisa de aprovação explícita.

---

## Critérios para confiança

Uma integração pode ser considerada confiável quando:

- tem finalidade clara;
- possui documentação suficiente;
- opera com menor privilégio;
- tem modo read-only quando possível;
- seus outputs são compreensíveis;
- seus efeitos são rastreáveis;
- seus riscos são conhecidos;
- há política de uso;
- há registro em governance;
- há limites por agente ou contexto.

---

## Critérios de rejeição

Uma integração não deve ser confiada quando:

- exige permissão ampla demais;
- não há clareza sobre efeitos;
- mistura leitura e escrita sem separação;
- produz outputs opacos;
- não tem valor recorrente;
- amplia risco mais do que reduz incerteza;
- depende de credenciais mal geridas;
- não há dono ou documentação.

---

## Registro obrigatório

Integrações confiáveis devem ser registradas em `core/governance/03-trusted-integrations-registry.md`.

O registro deve conter:

- nome da integração;
- finalidade;
- nível de confiança;
- permissões;
- agentes autorizados;
- operações permitidas;
- operações proibidas;
- riscos;
- observações;
- status.

---

## Relação com MCP

Todo MCP server relevante é uma integração.

Por padrão, MCP deve começar como:
- experimental;
- read-only;
- restrito;
- e sem escrita sensível.

Promoção para escrita depende de política, registro e autorização.

---

## Relação com agentes

Nem todo agente deve poder usar toda integração.

Exemplo:
- `mcp-observer` pode ler board;
- `implementer` pode não precisar acessar board diretamente;
- `reviewer` pode ler PRs;
- nenhum agente deve escrever em produção por padrão.

Permissão deve seguir função.

---

## Relação com evidência

Integrações podem produzir evidência, mas o harness deve avaliar:

- a fonte é confiável?
- o dado está atualizado?
- o output é interpretável?
- há risco de contexto incompleto?
- a fonte externa contradiz authority source local?

Integração não substitui julgamento.

---

## Relação com segurança

Integrações ampliam surface area.

Por isso, toda integração confiável deve ser analisada quanto a:
- permissões;
- segredo;
- escopo;
- logs;
- dados sensíveis;
- risco de write;
- risco de impersonação;
- risco de supply chain.

---

## Revisão periódica

Integrações confiáveis devem ser revisadas periodicamente.

Perguntas:
- ainda são necessárias?
- ainda estão seguras?
- permissões continuam adequadas?
- o uso real corresponde ao registro?
- houve mudança no provedor, API ou risco?

---

## Sinais de mau uso

Sinais de mau uso de integração:

- ferramenta externa usada por conveniência sem pergunta clara;
- integração virando fonte primária de verdade local;
- permissões amplas demais;
- automação write sem maturidade;
- agente usando integração fora do papel;
- outputs aceitos sem validação.

---

## Declaração operacional curta

Integração confiável não é a que apenas funciona.  
É a que tem finalidade, limite, permissão, risco e governança conhecidos.