# Economia e Compactação de Contexto

## Finalidade

Este protocolo define como o harness deve tratar contexto como recurso finito, caro e degradável.

Seu papel é impedir:
- inflar a janela do modelo com material irrelevante;
- arrastar histórico demais para tasks novas;
- confundir memória útil com transcript bruto;
- piorar precisão por excesso de contexto.

---

## Tese central

Mais contexto não significa automaticamente melhor resultado.

Contexto bom é:
- relevante;
- verdadeiro;
- atualizado;
- delimitado;
- economicamente útil para a task atual.

A engenharia trata contexto como budget, não como depósito.

---

## Fontes de contexto do sistema

O sistema opera com três camadas principais:

### 1. Contexto global
O que é durável entre projetos:
- princípios;
- leis;
- protocols;
- policies;
- agents;
- skills;
- templates;
- taxonomias.

### 2. Contexto de workspace
O que é verdadeiro para um projeto específico:
- arquitetura local;
- comandos reais;
- authority sources;
- riscos locais;
- boundaries do repositório;
- `PROJECT_STATE.md`;
- operational reality.

### 3. Contexto de sessão
O que é efêmero e ligado à task:
- hipótese atual;
- arquivos tocados;
- desvios do plan;
- erros observados;
- decisões locais temporárias;
- progresso corrente da execução.

---

## Regra de ouro

O que é durável vira documento.  
O que é efêmero não deve ser arrastado indefinidamente.

Se a informação:
- será útil depois,
- precisa sobreviver a sessões,
- define verdade do projeto,
- ou explica o estado técnico atual,

ela deve virar artifact formal, não permanecer só na conversa.

---

## Quando contexto está bom

O contexto está saudável quando:
- contém apenas o necessário para a task;
- aponta para authority sources em vez de duplicá-las;
- não mistura múltiplas frentes irrelevantes;
- preserva clareza causal;
- mantém o plan e o review legíveis.

---

## Sinais de contexto ruim

O contexto está degradado quando:
- a sessão está carregando histórico demais;
- o runtime começa a repetir informação irrelevante;
- a task atual está soterrada por tasks antigas;
- o review fica confuso;
- a leitura vira dispersa;
- o agente perde foco estrutural.

---

## Quando compactar

Compactação é recomendada quando:
- a task vai continuar, mas o histórico bruto já está grande demais;
- a sessão contém informação útil misturada com ruído;
- o agente precisa preservar só decisões e fatos, não toda a conversa;
- a continuidade exige clareza, não verbosidade.

---

## O que deve entrar em uma compactação

Uma boa compactação deve preservar:

- objetivo atual;
- estado da task;
- plan vigente;
- arquivos ou módulos relevantes;
- decisões tomadas;
- validações já realizadas;
- dúvidas abertas;
- riscos remanescentes;
- próximo passo.

---

## O que não deve entrar em uma compactação

Não deve entrar:
- transcript completo;
- tentativas descartadas sem valor residual;
- raciocínio verborrágico;
- duplicação de contextos já documentados;
- teoria genérica que já está no harness global.

---

## Relação com discovery

Discovery bom reduz necessidade de carregar contexto bruto.

Em vez de empilhar código e conversa, o sistema deve preferir:
- mapa estrutural;
- authority sources;
- identificação de área afetada;
- artifacts formais.

---

## Relação com skills

Skills existem justamente para evitar inflar o contexto-base.

Em vez de despejar especialização permanentemente no prompt, o sistema:
- mantém o contexto global enxuto;
- e chama a skill certa quando necessário.

---

## Relação com state e board

`PROJECT_STATE.md` e board reduzem a dependência de memória conversacional.

Eles existem para impedir que:
- a continuidade dependa de transcript cru;
- a tarefa futura precise reabrir toda a conversa passada;
- a memória operacional do projeto fique implícita.

---

## Compactação não é perda de rigor

Compactar não significa empobrecer.  
Significa transformar contexto em forma mais legível, econômica e reutilizável.

A regra é:
- preservar fatos,
- remover ruído,
- manter continuidade.

---

## Declaração operacional curta

Contexto é recurso finito.  
A boa engenharia não carrega tudo.  
Ela carrega o necessário, documenta o durável e descarta o ruído.