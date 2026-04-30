# Missão do Harness

## Finalidade

A missão desta engenharia é transformar o coding agent em um executor disciplinado, verificável, econômico em contexto, seguro por desenho e subordinado a uma camada estratégica humana.

O harness existe para impedir que a execução dependa apenas de improviso contextual, confiança verbal do modelo ou comportamento oportunista do runtime.

## Tese central

Modelos geram texto e código.  
Engenharia de harness gera comportamento operacional confiável.

O diferencial real não está em “ter acesso ao melhor modelo”, mas em estruturar:

- missão;
- princípios;
- leis;
- classes de risco;
- políticas de autonomia;
- protocolos de trabalho;
- artifacts formais;
- guardrails de segurança;
- controle de contexto;
- controle de entropia;
- governança.

## O problema que o sistema resolve

Sem harness, o agente tende a:

- misturar descoberta, decisão, implementação e review em um único fluxo;
- improvisar arquitetura;
- mutar cedo demais;
- inflar contexto sem necessidade;
- introduzir abstrações prematuras;
- operar acima do envelope de risco desejado;
- encerrar tasks com linguagem confiante, mas sem evidência suficiente;
- degradar a coerência do sistema ao longo do tempo.

O harness existe para reduzir esse conjunto de falhas.

## O que o harness protege

Esta engenharia protege:

- a clareza entre estratégia e execução;
- a previsibilidade do fluxo;
- a rastreabilidade da decisão;
- a honestidade da evidência;
- a segurança operacional;
- a integridade da arquitetura local;
- a coerência evolutiva do sistema;
- a manutenção da simplicidade proporcional.

## O que o harness não pretende fazer

O harness não existe para:

- substituir julgamento humano;
- eliminar revisão;
- automatizar toda decisão;
- transformar o runtime em oráculo;
- inflar o processo por formalismo;
- introduzir cerimônia sem ganho real.

O sistema existe para reduzir entropia, não para produzir ritual vazio.

## Relação com a camada estratégica

O harness não é a camada estratégica.

A camada estratégica continua sendo responsabilidade de:

- humano operador;
- Core Architect;
- revisão humana especializada quando necessário.

O harness serve à camada estratégica e não o contrário.

## Relação com o runtime

O runtime é substituível.  
A engenharia é o núcleo.

Isso significa que:

- OpenCode é a superfície operacional atual;
- a arquitetura canônica do harness vale mais do que o adapter do momento;
- o sistema deve nascer independente do runtime concreto.

## Resultado esperado

Quando esta engenharia estiver madura, será possível operar coding agents com:

- maior previsibilidade;
- menor improviso;
- menor slop;
- melhor relação entre contexto e ação;
- melhor qualidade de handoff;
- maior clareza de risco;
- maior capacidade de revisão;
- melhor governança evolutiva.

## Declaração curta de missão

Esta engenharia existe para fazer o agente trabalhar como executor confiável de decisões humanas bem formuladas, dentro de limites explícitos de risco, contexto, segurança, evidência e coerência arquitetural.