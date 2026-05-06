# OpenCode Plugins

## Finalidade

Este diretório documenta a política de plugins do OpenCode dentro do harness.

Plugins são extensões opcionais do runtime.  
Eles não são fundamento da engenharia.

O harness deve funcionar conceitualmente sem depender de plugin específico.

---

## Regra central

Plugin é conveniência operacional, não doutrina.

Se uma regra for essencial para o comportamento do harness, ela deve viver no núcleo canônico:

```text
core/
skills/
agents/
templates/
```

Se uma regra depende da forma como o OpenCode carrega, executa ou expõe plugins, ela pertence ao adapter:

```text
adapters/opencode/plugins/
```

---

## Fonte canônica

Fontes principais:

```text
core/policies/04-tool-and-runtime-boundaries.md
core/policies/07-trusted-integrations-policy.md
core/governance/02-experimental-registry.md
core/governance/03-trusted-integrations-registry.md
core/governance/00-maturity-model.md
```

Fontes relacionadas:

```text
adapters/opencode/README.md
adapters/opencode/AGENTS.md
adapters/opencode/permissions/
```

---

## Status atual

```text
Status: reservado
Maturidade: experimental
Plugins oficiais ativos: nenhum
```

Nesta versão inicial do harness, plugins não são necessários para a operação canônica.

---

## Quando considerar um plugin

Um plugin só deve ser considerado quando resolver uma dor real e recorrente.

Exemplos de dores possíveis:

- reduzir repetição operacional frequente;
- integrar ferramenta read-only de forma mais segura;
- expor comando de validação com menor risco;
- melhorar observabilidade do fluxo;
- padronizar handoff;
- reduzir erro humano em operação repetitiva de baixo risco.

---

## Quando não considerar um plugin

Não adotar plugin quando:

- a motivação for hype;
- a função puder ser resolvida por command/documentação simples;
- o plugin exigir permissão ampla;
- o plugin misturar leitura e escrita sem boundary;
- o plugin depender de segredo sem governança;
- o plugin criar acoplamento forte ao runtime;
- o plugin for necessário apenas para uma task pontual;
- o plugin aumentar mais entropia do que reduz.

---

## Critérios para avaliação

Antes de adicionar plugin, responder:

```text
Qual problema real o plugin resolve?
Esse problema é recorrente?
Que permissões o plugin exige?
O plugin lê dados? Quais?
O plugin escreve dados? Onde?
Qual é o blast radius?
Qual agente pode usá-lo?
Qual artifact registra seu uso?
Como o plugin falha?
Como desativar ou remover?
Existe alternativa mais simples?
```

---

## Modo padrão

Todo plugin novo começa como:

```text
experimental
read-only quando possível
sem produção
sem segredo
sem escrita externa
sem automação irreversível
```

Promoção de maturidade exige evidência.

---

## Registro obrigatório

Plugins relevantes devem ser registrados em:

```text
core/governance/02-experimental-registry.md
```

Se forem promovidos para uso confiável, também devem aparecer em:

```text
core/governance/03-trusted-integrations-registry.md
```

---

## Permissões

Plugins devem seguir menor privilégio.

Por padrão, plugins não devem poder:

- tocar produção;
- manipular secrets;
- alterar cloud config;
- mover board items;
- fechar issues;
- comentar em PRs;
- disparar deploy;
- alterar permissões;
- executar comandos destrutivos.

Qualquer exceção exige:

- finalidade clara;
- autorização explícita;
- registro em governance;
- matriz de permissão;
- plano de rollback ou mitigação;
- revisão humana.

---

## Relação com agents

Um plugin não deve ser acessível por todos os agentes por padrão.

Exemplo de separação:

```text
planner
→ pode consultar plugin read-only de contexto se necessário.

researcher
→ pode usar plugin read-only de docs/repo.

mcp-observer
→ pode usar plugin read-only externo.

implementer
→ só deve usar plugin que ajude execução local controlada.

reviewer
→ pode usar plugin de leitura para evidência.

architect-critic
→ pode usar plugin read-only para contexto arquitetural.

delivery-prep
→ pode usar plugin de leitura para handoff/state.
```

---

## Relação com commands

Se um plugin existir, commands devem chamá-lo apenas quando fizer sentido.

Plugins não devem substituir:

- `plan`;
- `investigate`;
- `implement`;
- `review`;
- `handoff`;
- `project-state`.

Eles podem apoiar esses fluxos, mas não redefini-los.

---

## Segurança

Antes de usar plugin, verificar:

- permissões;
- leitura de dados sensíveis;
- escrita externa;
- logs;
- credenciais;
- supply chain;
- versionamento;
- origem;
- manutenção;
- desinstalação.

Plugins que executam código externo exigem cautela adicional.

---

## Evidência

Uso relevante de plugin deve ser registrado quando impactar decisão.

Registrar:

```text
plugin usado
versão, se aplicável
operação executada
modo
resultado
limitação
impacto na task
```

---

## Critérios de promoção

Um plugin pode sair de experimental quando:

- uso recorrente foi comprovado;
- risco foi entendido;
- permissões são mínimas;
- falhas são previsíveis;
- outputs são úteis;
- não há alternativa mais simples;
- há registro em governance;
- há aceitação humana.

---

## Critérios de remoção

Remover ou desativar plugin quando:

- não for mais usado;
- ampliar risco desnecessariamente;
- quebrar com frequência;
- exigir permissões excessivas;
- duplicar capacidade existente;
- dificultar portabilidade;
- produzir outputs não confiáveis;
- induzir comportamento fora do harness.

---

## Anti-patterns

Evitar:

- plugin como atalho para falta de processo;
- plugin como substituto de policy;
- plugin que vira fonte única de verdade;
- plugin com permissão ampla por comodidade;
- plugin que mistura leitura e escrita sem separação;
- plugin adotado porque “parece legal”;
- plugin essencial sem alternativa documentada;
- plugin sem registro de maturidade.

---

## Declaração operacional curta

Plugins podem melhorar ergonomia, mas não governam a engenharia.  
O harness deve sobreviver sem eles.