# Política de PROJECT_STATE vs Board

## Finalidade

Esta policy define a diferença formal entre `PROJECT_STATE.md` e board de gestão, como GitHub Projects.

Seu papel é impedir que o harness confunda estado técnico do projeto com estado organizacional do trabalho.

---

## Tese central

Board responde “o que estamos fazendo?”.  
`PROJECT_STATE.md` responde “em que estado técnico o sistema está?”.

Ambos são importantes.  
Nenhum substitui o outro.

---

## O que é board

Board é ferramenta de gestão de trabalho.

Ele deve registrar:

- backlog;
- status das tasks;
- prioridade;
- responsáveis;
- sequencing;
- dependências organizacionais;
- issues;
- milestones;
- fluxo de entrega.

O board organiza execução e acompanhamento.

---

## O que é PROJECT_STATE

`PROJECT_STATE.md` é memória técnica viva do projeto.

Ele deve registrar:

- estado técnico atual;
- decisões duráveis;
- arquitetura local;
- riscos conhecidos;
- limitações;
- dívidas conscientes;
- comandos importantes;
- operational reality;
- mudanças relevantes para futuras sessões.

`PROJECT_STATE.md` orienta entendimento técnico e continuidade.

---

## Diferença essencial

### Board
É orientado a trabalho.

Exemplo:
- “Implementar autenticação”
- “Refatorar módulo Billing”
- “Corrigir bug de checkout”
- “Criar pipeline de deploy”

### PROJECT_STATE
É orientado a verdade técnica.

Exemplo:
- “Autenticação usa JWT com refresh token; rotação ainda não implementada”
- “Billing não deve importar diretamente Identity”
- “Checkout depende de gateway externo X; falha parcial exige fallback futuro”
- “Deploy ainda é manual; pipeline planejada, mas não operacional”

---

## Quando usar board

Usar board para:

- planejar trabalho;
- acompanhar andamento;
- priorizar;
- agrupar issues;
- definir sequência;
- visualizar bloqueios;
- registrar conclusão organizacional;
- comunicar progresso.

---

## Quando usar PROJECT_STATE

Usar `PROJECT_STATE.md` para registrar:

- decisão técnica durável;
- limitação confirmada;
- risco em observação;
- dívida consciente;
- mudança de comando;
- mudança de arquitetura;
- mudança operacional;
- achado técnico relevante;
- estado real que futuro agente precisa saber.

---

## O que não colocar no board

Evitar usar board para:

- documentação arquitetural;
- estado técnico detalhado;
- comandos locais;
- riscos técnicos explicados;
- decisões duráveis extensas;
- operational reality.

O board pode apontar para documentos, mas não deve virar substituto deles.

---

## O que não colocar no PROJECT_STATE

Evitar usar `PROJECT_STATE.md` para:

- lista completa de tasks;
- backlog;
- status granular de cada issue;
- comentários de execução efêmeros;
- changelog completo;
- diário de sessões;
- duplicação do board.

`PROJECT_STATE.md` deve ser denso, não burocrático.

---

## Relação entre os dois

A relação correta é complementar.

Uma issue pode gerar uma mudança.  
A mudança pode gerar um Completion Packet.  
O Completion Packet pode indicar um Project State Entry.  
O board registra que o trabalho andou.  
O `PROJECT_STATE.md` registra que o sistema mudou.

---

## Quando sincronizar

Sincronização deve ser considerada quando:

- uma task concluída altera realidade técnica;
- uma issue revela risco durável;
- um bloqueio organizacional tem causa técnica importante;
- uma decisão no board precisa virar estado técnico;
- uma atualização técnica muda o status real de uma issue.

---

## GitHub Projects via MCP

O harness pode usar MCP read-only para consultar board.

Uso legítimo:

- entender prioridade;
- ver status;
- identificar issue associada;
- checar dependências;
- evitar trabalhar em task errada.

Uso indevido:

- tratar board como documentação técnica;
- substituir discovery local;
- concluir arquitetura a partir de título de issue;
- atualizar board automaticamente sem política write específica.

---

## Relação com authority sources

`PROJECT_STATE.md` pode ser authority source técnica local.

Board é authority source de gestão de trabalho.

Quando houver conflito:

- para estado técnico, confiar no repositório e `PROJECT_STATE.md`;
- para status de trabalho, consultar board;
- para decisão ambígua, escalar.

---

## Papel do executor

O executor deve:

- consultar board quando necessário;
- não depender apenas dele;
- propor state update quando a task mudar realidade técnica;
- indicar no handoff se board e state precisam ser atualizados;
- evitar duplicação desnecessária.

---

## Papel do Core Architect

O Core Architect deve:

- garantir que decisões técnicas não fiquem presas no board;
- garantir que `PROJECT_STATE.md` não vire backlog;
- revisar se estado técnico e gestão estão coerentes;
- ajudar a decidir o que merece memória durável.

---

## Sinais de confusão

Há confusão quando:

- board contém documentação técnica longa;
- `PROJECT_STATE.md` virou lista de issues;
- agente pergunta ao board algo que deveria ler no código;
- decisões arquiteturais ficam só em comentários de issue;
- tasks são concluídas, mas estado técnico não muda onde deveria;
- futuro agente precisa ler histórico inteiro do board para entender o projeto.

---

## Declaração operacional curta

Board organiza trabalho.  
`PROJECT_STATE.md` preserva verdade técnica.  
O harness usa os dois, mas nunca confunde suas responsabilidades.