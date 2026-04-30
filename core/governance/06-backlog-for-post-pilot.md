# Backlog Pós-Piloto

## Finalidade

Este documento registra melhorias, ideias, extensões e endurecimentos que não devem ser implementados agora, mas que podem ser avaliados após o piloto controlado.

Seu papel é evitar dois extremos:

- esquecer boas ideias;
- implementar cedo demais e inflar o harness antes de validar o núcleo.

Backlog pós-piloto é estacionamento estratégico, não lista de desejos sem critério.

---

## Tese central

Nem toda boa ideia deve entrar agora.

O harness deve nascer forte, mas não inchado.

Ideias que parecem úteis, mas ainda não têm evidência suficiente, devem ser registradas para avaliação futura.

---

## Critérios para entrar no backlog

Adicionar item quando:

- a ideia parece útil;
- ainda não há evidência de recorrência;
- a implementação agora aumentaria escopo;
- depende do piloto;
- exige integração ainda não confiável;
- pode virar skill, command, plugin ou policy depois;
- precisa de maturidade antes de entrar.

---

## Critérios para sair do backlog

Promover item quando:

- o piloto mostrar dor real;
- houver repetição;
- o valor operacional ficar claro;
- o risco for compreendido;
- houver escopo delimitado;
- a solução reduzir entropia líquida.

Remover item quando:

- não houve dor real;
- ficou redundante;
- gera risco alto;
- adiciona complexidade sem retorno;
- depende de ferramenta instável;
- deixou de fazer sentido.

---

## Template de item

```md
## <nome do item>

### Categoria
<skill | agent | template | adapter | MCP | plugin | eval | automation | governance | outro>

### Status
<proposto | aguardando piloto | promovido | rejeitado | removido>

### Descrição
<descrição curta>

### Dor ou oportunidade
<qual problema isso resolveria>

### Critério para promover
<que evidência justificaria implementar>

### Risco de implementar cedo demais
<que custo ou entropia isso poderia gerar>

### Dependências
<o que precisa existir antes>

### Observações
<notas adicionais>
```

---

## Backlog inicial

### Dashboard simples de métricas do harness

#### Categoria
observability / tooling

#### Status
aguardando piloto

#### Descrição
Criar forma simples de visualizar métricas de tasks, como evidence strength, handoff continuity, entropy delta e review quality.

#### Dor ou oportunidade
Pode ajudar a enxergar padrões de falha ao longo do tempo.

#### Critério para promover
Promover se o piloto gerar dados suficientes e a análise manual ficar repetitiva.

#### Risco de implementar cedo demais
Criar teatro de métricas antes de saber quais sinais realmente importam.

---

### Replay suite formal

#### Categoria
eval / replay

#### Status
aguardando piloto

#### Descrição
Formalizar conjunto de cenários de replay para comparar versões do harness, modelos e adapters.

#### Dor ou oportunidade
Ajuda a medir regressão comportamental.

#### Critério para promover
Promover quando houver pelo menos alguns cenários reais recorrentes.

#### Risco de implementar cedo demais
Criar suite artificial que mede casos pouco representativos.

---

### MCP write controlado

#### Categoria
MCP / integration

#### Status
aguardando piloto

#### Descrição
Avaliar se alguma escrita via MCP deve ser permitida em escopos muito restritos, como atualização de status não sensível.

#### Dor ou oportunidade
Pode reduzir fricção operacional.

#### Critério para promover
Somente se o piloto mostrar repetição, baixo risco e trusted integration madura.

#### Risco de implementar cedo demais
Ampliar autonomia externa antes de governança suficiente.

---

### Plugin operacional para OpenCode

#### Categoria
adapter / plugin

#### Status
aguardando piloto

#### Descrição
Criar plugin para automatizar parte do carregamento de skills, commands ou artifacts no OpenCode.

#### Dor ou oportunidade
Pode reduzir fricção de uso.

#### Critério para promover
Promover se a operação manual do adapter ficar repetitiva e estável.

#### Risco de implementar cedo demais
Acoplar demais o núcleo ao runtime e cristalizar fluxo ainda instável.

---

### Mais skills específicas de stack

#### Categoria
skill / stack

#### Status
aguardando piloto

#### Descrição
Expandir stack skills além do conjunto inicial, caso surjam dores reais em .NET, React, PostgreSQL ou Azure.

#### Dor ou oportunidade
Pode reduzir erros recorrentes específicos.

#### Critério para promover
Somente quando uma dor aparecer em mais de uma task ou tiver risco alto.

#### Risco de implementar cedo demais
Transformar skills em apostila enciclopédica.

---

### Templates avançados de ADR

#### Categoria
template / architecture

#### Status
aguardando piloto

#### Descrição
Criar variações de ADR para decisões de arquitetura, cloud, integração, dependência e segurança.

#### Dor ou oportunidade
Pode melhorar registro de decisões.

#### Critério para promover
Promover se decisões relevantes estiverem ficando mal registradas.

#### Risco de implementar cedo demais
Gerar burocracia de ADR antes de haver volume real de decisões.

---

### Automação de PROJECT_STATE

#### Categoria
automation / workspace

#### Status
aguardando piloto

#### Descrição
Avaliar command ou workflow para sugerir Project State Entry automaticamente após Completion Packet.

#### Dor ou oportunidade
Pode reduzir esquecimento de atualização de estado.

#### Critério para promover
Promover se o piloto mostrar state updates recorrentes e formato estável.

#### Risco de implementar cedo demais
Inflar PROJECT_STATE com ruído automático.

---

### Adapter alternativo futuro

#### Categoria
adapter

#### Status
aguardando piloto

#### Descrição
Avaliar portabilidade do núcleo para outro runtime futuro, caso surja necessidade.

#### Dor ou oportunidade
Preserva independência do harness.

#### Critério para promover
Somente se houver runtime alternativo real e necessidade prática.

#### Risco de implementar cedo demais
Dividir energia antes de estabilizar OpenCode.

---

### Policy de segurança avançada

#### Categoria
security / policy

#### Status
aguardando piloto

#### Descrição
Criar políticas mais profundas para threat modeling, abuso de API, privacy e secure SDLC.

#### Dor ou oportunidade
Pode aumentar maturidade de segurança.

#### Critério para promover
Promover se tasks reais tocarem segurança de forma recorrente ou sensível.

#### Risco de implementar cedo demais
Transformar toda task em auditoria pesada.

---

### Catálogo de incidentes e falhas do harness

#### Categoria
governance / observability

#### Status
aguardando piloto

#### Descrição
Registrar falhas reais do harness, como missed escalation, slop aprovado ou handoff ruim.

#### Dor ou oportunidade
Ajuda no hardening.

#### Critério para promover
Promover quando houver volume suficiente de falhas reais.

#### Risco de implementar cedo demais
Criar processo pesado antes de existirem dados.

---

## Revisão do backlog

Este backlog deve ser revisado:

- ao final do piloto;
- antes de release candidate;
- quando uma dor se repetir;
- quando uma ideia deixar de fazer sentido;
- quando uma integração amadurecer.

---

## Declaração operacional curta

Backlog pós-piloto protege boas ideias sem inflar o presente.  
O harness registra possibilidades, mas só promove o que a prática justificar.