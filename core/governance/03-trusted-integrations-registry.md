# Registro de Integrações Confiáveis

## Finalidade

Este documento registra integrações consideradas confiáveis, experimentais ou restritas dentro da engenharia de harness.

Seu papel é implementar, em forma de registro, a política de integrações confiáveis.

Integração confiável não é a que apenas funciona.  
É a que possui finalidade, permissões, limites, risco e status conhecidos.

---

## Tese central

Nenhuma integração deve ser usada com confiança operacional sem registro.

O harness precisa saber:
- o que a integração acessa;
- o que ela pode alterar;
- quem pode usá-la;
- com qual nível de permissão;
- qual risco ela introduz;
- e em que status de maturidade ela está.

---

## Níveis de confiança

### `experimental`

Integração em avaliação. Uso restrito.

### `read-only-trusted`

Integração confiável para leitura controlada.

### `restricted-operational`

Integração autorizada para ações limitadas e não sensíveis.

### `sensitive`

Integração toca produção, segredo, deploy, dados reais ou efeitos externos relevantes.

### `deprecated`

Integração não deve ser usada em novos fluxos.

---

## Campos obrigatórios por integração

Cada integração deve registrar:

1. nome;
2. tipo;
3. status;
4. finalidade;
5. modo permitido;
6. operações permitidas;
7. operações proibidas;
8. permissões necessárias;
9. agentes autorizados;
10. riscos;
11. evidência produzida;
12. revisão futura.

---

## Template de integração

```md
## <nome da integração>

### Tipo
<MCP | GitHub | cloud | observability | docs | CI/CD | plugin | CLI | outro>

### Status
<experimental | read-only-trusted | restricted-operational | sensitive | deprecated>

### Finalidade
<por que esta integração existe>

### Modo permitido
<read-only | restricted-write | sensitive-write | outro>

### Operações permitidas
- <operação 1>
- <operação 2>

### Operações proibidas
- <operação 1>
- <operação 2>

### Permissões necessárias
- <permissão 1>
- <permissão 2>

### Agentes autorizados
- <agent 1>
- <agent 2>

### Artifacts relacionados
- <artifact 1>
- <artifact 2>

### Riscos
- <risco 1>
- <risco 2>

### Evidência produzida
<que tipo de evidência esta integração pode fornecer>

### Condições de uso
<quando usar e quando evitar>

### Próxima revisão
<data, milestone ou condição>

### Observações
<notas adicionais>
```

---

## Integrações previstas inicialmente

### GitHub Repository Read-Only

#### Tipo
GitHub

#### Status
read-only-trusted

#### Finalidade
Permitir leitura de arquivos, estrutura de repositório, histórico básico e estado público/privado autorizado para revisão, auditoria e inspeção.

#### Modo permitido
read-only

#### Operações permitidas
- ler arquivos;
- listar repositório;
- consultar metadados;
- consultar branches;
- consultar conteúdo versionado;
- apoiar review factual.

#### Operações proibidas
- escrever arquivos;
- abrir ou fechar PR;
- merge;
- push;
- alterar settings;
- alterar permissões;
- modificar branch protection.

#### Agentes autorizados
- `researcher`;
- `reviewer`;
- `mcp-observer`;
- `delivery-prep`, quando necessário para handoff.

#### Riscos
- tratar repositório remoto como mais atual que workspace local sem verificar;
- ignorar branch correta;
- supervalorizar estado remoto desatualizado.

---

### GitHub Projects Read-Only

#### Tipo
GitHub Projects / MCP

#### Status
experimental

#### Finalidade
Ler estado de trabalho, backlog, status de issues, prioridades e dependências organizacionais.

#### Modo permitido
read-only

#### Operações permitidas
- consultar board;
- consultar cards/items;
- consultar issue associada;
- ler status;
- ler prioridade;
- apoiar sequencing de tasks.

#### Operações proibidas
- mover card;
- fechar issue;
- criar item;
- alterar status;
- alterar prioridade;
- escrever comentário;
- automatizar board sem política write.

#### Agentes autorizados
- `mcp-observer`;
- `researcher`, se via contexto read-only;
- `delivery-prep`, apenas para sugerir atualização.

#### Riscos
- confundir board com estado técnico;
- tratar título de issue como especificação completa;
- depender de board para entender arquitetura.

---

### Documentation Research

#### Tipo
Docs externas

#### Status
read-only-trusted

#### Finalidade
Consultar documentação oficial ou confiável quando conhecimento do modelo puder estar desatualizado ou incompleto.

#### Modo permitido
read-only

#### Operações permitidas
- ler documentação oficial;
- verificar API, SDK, CLI ou comportamento de versão;
- apoiar Investigation Note ou Execution Plan.

#### Operações proibidas
- aceitar fonte fraca sem crítica;
- substituir authority source local;
- despejar documentação longa no contexto sem necessidade.

#### Agentes autorizados
- `researcher`;
- `mcp-observer`;
- `planner`, quando usar achados documentados.

#### Riscos
- documentação de versão errada;
- excesso de contexto;
- fonte externa contradizer realidade local.

---

### Cloud Metadata Read-Only

#### Tipo
Cloud

#### Status
experimental

#### Finalidade
Consultar metadata de ambiente cloud sem mutação, quando necessário para diagnóstico, arquitetura ou execução orientada a produção.

#### Modo permitido
read-only

#### Operações permitidas
- ler configuração;
- checar recurso;
- entender runtime;
- confirmar região, plano ou topologia;
- apoiar diagnóstico.

#### Operações proibidas
- criar recurso;
- alterar config;
- deletar recurso;
- executar deploy;
- alterar segredo;
- modificar IAM.

#### Agentes autorizados
- `mcp-observer`;
- `researcher`, quando permitido;
- `reviewer`, para auditoria read-only.

#### Riscos
- tocar produção;
- vazar metadata sensível;
- interpretar config sem contexto.

---

### Observability Read-Only

#### Tipo
Observability

#### Status
experimental

#### Finalidade
Consultar logs, métricas, traces ou health signals em modo read-only para apoiar investigação e diagnóstico.

#### Modo permitido
read-only

#### Operações permitidas
- ler métricas;
- ler traces;
- ler logs filtrados;
- confirmar sintomas;
- apoiar Investigation Note.

#### Operações proibidas
- alterar alertas;
- silenciar alertas;
- modificar dashboard;
- expor dados sensíveis;
- despejar logs extensos em artifacts.

#### Agentes autorizados
- `mcp-observer`;
- `researcher`;
- `reviewer`, quando necessário.

#### Riscos
- vazamento de dados;
- interpretação errada de sinais;
- contexto excessivo;
- uso de logs sem hipótese clara.

---

## Processo de promoção

Uma integração pode ser promovida quando:

- foi usada em piloto;
- seus riscos são conhecidos;
- seus outputs são úteis;
- seu modo de permissão está claro;
- não houve mau uso recorrente;
- há valor operacional real;
- há compatibilidade com policies.

---

## Processo de rebaixamento

Rebaixar ou depreciar quando:

- permissões mudarem;
- riscos aumentarem;
- uso real for baixo;
- outputs forem pouco confiáveis;
- integração gerar ruído;
- integração induzir decisões ruins.

---

## Declaração operacional curta

Este registro define em quem o harness confia, para quê e com quais limites.  
Integração sem registro não deve ser tratada como confiável.