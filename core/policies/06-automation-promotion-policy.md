# Política de Promoção de Automação

## Finalidade

Esta policy define quando um comportamento recorrente pode ser promovido a automação oficial dentro do harness, seja como command, script, skill, plugin, integração ou rotina operacional.

Seu papel é impedir que a engenharia transforme qualquer repetição percebida em automação prematura, aumentando entropia, risco e custo de manutenção.

---

## Tese central

Automação só deve ser promovida quando o processo manual já está compreendido, estabilizado e justificado por repetição real.

Automação prematura cristaliza erro.  
Automação madura reduz fricção sem reduzir controle.

---

## Regra operacional principal

Nenhum fluxo deve virar automação oficial sem responder:

1. o processo já se repetiu mais de uma vez?
2. os passos são estáveis?
3. o risco é compreendido?
4. o output esperado é claro?
5. a automação reduz erro ou apenas economiza digitação?
6. há rollback ou modo seguro?
7. a automação respeita policies de comando, arquivo, Git, MCP e produção?

Se essas respostas não estiverem claras, o fluxo ainda deve permanecer manual ou semi-manual.

---

## Estágios de maturidade

### 1. Manual exploratório
O operador ou agente executa passos manualmente para entender o problema.

Use quando:
- o fluxo ainda é incerto;
- há descoberta em andamento;
- o risco ainda não é conhecido.

### 2. Checklist
O fluxo vira checklist quando os passos já são compreendidos, mas ainda exigem julgamento humano.

Use quando:
- há repetição;
- ainda há variação;
- o risco depende de contexto.

### 3. Template
O fluxo vira template quando a estrutura se repete, mas o conteúdo muda.

Use para:
- packets;
- reports;
- prompts;
- ADRs;
- state entries.

### 4. Command
O fluxo vira command quando a execução tem sequência relativamente estável e escopo claro.

Use quando:
- o ganho operacional é real;
- o risco é baixo ou controlado;
- o resultado é previsível.

### 5. Skill
O fluxo vira skill quando precisa de método acionável, critérios, anti-patterns e outputs esperados.

Use quando:
- envolve julgamento recorrente;
- exige checklist inteligente;
- precisa ser chamado sob demanda.

### 6. Plugin ou integração
O fluxo vira plugin ou integração quando há necessidade técnica real de conexão com runtime, API ou ferramenta externa.

Use apenas com governança forte.

---

## Critérios para promover

Uma automação pode ser promovida quando atender a maioria dos critérios abaixo:

- recorrência real;
- passos conhecidos;
- risco classificado;
- valor operacional claro;
- escopo delimitado;
- output verificável;
- falhas previsíveis;
- compatibilidade com policies;
- baixo risco de acoplamento indevido;
- manutenção aceitável.

---

## Critérios para não promover

Não promover quando:

- o fluxo ainda está sendo descoberto;
- há muitas exceções;
- a automação depende de julgamento estratégico;
- o risco é alto;
- a superfície externa é sensível;
- o ganho é apenas cosmético;
- a automação mascararia falta de entendimento;
- o processo ainda não possui evidência de recorrência.

---

## Automação não substitui julgamento

Mesmo automações aprovadas devem preservar:

- possibilidade de inspeção;
- logs ou evidência;
- modo de falha compreensível;
- ponto de interrupção;
- escalonamento quando o caso sair do padrão.

Automação que impede review é regressão.

---

## Relação com classes de risco

### R0
Automações read-only são as candidatas mais seguras.

### R1
Automações locais e reversíveis podem ser promovidas com baixa fricção.

### R2
Automações devem ter evidência, validação e boundaries claros.

### R3
Automações precisam de maturidade forte e geralmente aprovação estratégica.

### R4
Automação padrão não deve operar ações R4.

---

## Relação com MCP

Automação via MCP deve seguir política ainda mais conservadora.

Por padrão:
- leitura antes de escrita;
- escopo estreito;
- menor privilégio;
- trusted integration;
- autorização humana para writes sensíveis.

A existência de MCP não justifica automação write.

---

## Relação com scripts e commands

Scripts e commands devem ser versionados e documentados quando virarem parte oficial do fluxo.

Um script promovido deve ter:

- nome claro;
- finalidade;
- inputs esperados;
- outputs esperados;
- riscos;
- modo de uso;
- limites;
- relação com authority commands, quando aplicável.

---

## Relação com skills

Uma skill não é automação de execução bruta.  
Ela é automação de método.

Promover uma skill faz sentido quando o harness precisa repetir um raciocínio, checklist ou análise especializada de forma consistente.

---

## Sinais de automação prematura

São sinais de alerta:

- “vamos automatizar porque dá”;
- script sem dono;
- command que altera estado demais;
- plugin antes de checklist;
- integração antes de política;
- automação para fluxo que ainda muda toda hora;
- automação que aumenta risco para economizar poucos segundos.

---

## Revisão de automações

Toda automação oficial deve poder ser revisada.

A revisão deve perguntar:

- ainda é usada?
- ainda é segura?
- ainda reduz entropia?
- ainda representa o fluxo correto?
- ainda respeita o runtime atual?
- deveria virar skill, command, checklist ou ser removida?

---

## Declaração operacional curta

Automação boa nasce de processo entendido.  
Automação prematura cristaliza confusão.  
O harness promove automação por maturidade, não por entusiasmo.