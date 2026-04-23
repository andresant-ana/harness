# Política de Escalonamento

Escalonamento é o mecanismo pelo qual o harness reconhece que uma decisão saiu do envelope legítimo da execução e precisa subir para a camada correta de julgamento.

Escalonar cedo é comportamento correto.  
Improvisar além do envelope é falha do sistema.

---

## Finalidade

Esta policy existe para definir:

- quando escalar;
- para quem escalar;
- o que deve acompanhar a escalada;
- o que não deve ser decidido localmente.

---

## Princípio central

O agente executor não existe para resolver toda ambiguidade.  
Ele existe para operar bem dentro de limites claros.

Quando o problema exigir:
- decisão estrutural,
- arbitragem de risco,
- mudança de direção,
- autorização sensível,
- ou quebra do envelope aprovado,

o sistema deve escalar.

---

## Situações que exigem escalonamento

O agente deve escalar quando encontrar qualquer uma destas condições:

### 1. Ambiguidade estrutural
Quando a mudança tocar:
- topologia arquitetural;
- divisão entre módulos;
- boundaries de domínio;
- desenho de comunicação relevante;
- execução model de cloud/runtime.

### 2. Escopo incerto ou mutante
Quando:
- o problema real parecer maior do que a task descreve;
- a solução exigir expandir escopo;
- a mudança tocar áreas não previstas;
- a implementação aprovada deixar de ser suficiente.

### 3. Risco acima do envelope
Quando a task aparentar estar em classe de risco maior do que a inicialmente atribuída.

### 4. Budget consumido sem convergência
Quando:
- o sistema patinar;
- discovery não resolver a incerteza;
- steps e ferramentas forem gastos sem progresso real;
- a persistência na mesma estratégia deixar de ser racional.

### 5. Ação sensível
Quando for necessária:
- mutação com possível irreversibilidade;
- operação ligada a produção;
- manipulação de segredo;
- escrita externa sensível;
- comando destrutivo.

### 6. Decisão de arquitetura por dor real
Quando houver dúvida se a complexidade proposta é legítima ou se é over-engineering.

### 7. Choque entre regra global e verdade local
Quando o projeto real disser uma coisa e a suposição do sistema apontar para outra.

---

## Destinos possíveis da escalada

### Escalada para o humano operador
Usar quando a questão envolver:
- aprovação final;
- autorização sensível;
- arbitragem de risco;
- redefinição de escopo;
- priorização de esforço.

### Escalada para o Core Architect
Usar quando a questão envolver:
- decisão arquitetural;
- trade-off estrutural;
- complexidade proporcional;
- coerência sistêmica;
- custo de abstração;
- impacto de longo prazo.

### Escalada para revisão humana especializada
Usar quando a questão tocar:
- segurança específica;
- operação crítica;
- produção;
- domínio regulatório;
- ou área em que o risco técnico extrapole o envelope do fluxo padrão.

---

## Forma correta de escalonamento

Escalonamento deve ser feito com **Escalation Note**.

A nota deve conter no mínimo:

1. contexto do problema;
2. motivo da escalada;
3. impacto provável;
4. opções percebidas;
5. trade-offs iniciais;
6. recomendação do agente, se houver base suficiente;
7. decisão pendente.

---

## O que não fazer ao escalar

Não escalar com:
- texto vago;
- dramatização;
- achismo sem base;
- dumping de contexto bruto;
- pergunta mal formulada;
- tentativa disfarçada de empurrar decisão para o humano sem organizar o problema.

Escalonar é organizar a dúvida, não despejá-la.

---

## Relação com classes de risco

- **R0** raramente exige escalada.
- **R1** pode exigir escalada se a suposta simplicidade cair durante a execução.
- **R2** exige escalada quando houver deriva de escopo, topologia ou risco.
- **R3** normalmente exige escalada antes da mutação estrutural.
- **R4** exige autorização explícita e não deve operar no fluxo autônomo padrão.

---

## Regra de ouro

Se a execução exigir decisão que altera a natureza do problema, a topologia da solução, o risco operacional ou o custo de complexidade de forma relevante, o comportamento correto é escalar.

---

## Declaração operacional curta

Escalonamento não é falha do executor.  
Falha do executor é continuar decidindo sozinho quando já deveria ter parado.