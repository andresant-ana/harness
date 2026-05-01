# Skill — React Component Architecture

## Finalidade

Esta skill orienta a criação, alteração e revisão de componentes React com foco em composição, responsabilidade, legibilidade, boundaries de UI, reuso proporcional e prevenção de componentes gigantes.

Seu papel é impedir que o agente gere frontend funcional, mas difícil de manter, com componente inchado, duplicação visual, props confusas, responsabilidade misturada ou estrutura de UI desalinhada com o projeto.

Esta skill não ensina React do zero.  
Ela define um método operacional para construir componentes React de forma clara, localmente coerente e proporcional ao escopo da task.

---

## Quando usar

Use esta skill quando a task tocar:

- componente React relevante;
- página;
- layout;
- feature de UI;
- formulário;
- lista;
- tabela;
- card;
- modal;
- fluxo visual;
- composição de componentes;
- reuso de UI;
- props complexas;
- duplicação visual;
- componente grande demais;
- mudança em design system local;
- boundary entre componente de apresentação e componente de feature.

---

## Quando não usar

Não use esta skill quando:

- a mudança for visual trivial e isolada;
- o componente alvo já estiver claro e a alteração for mínima;
- a task for puramente de estado, data fetching ou effects;
- a task não envolver React;
- a aplicação da skill criaria cerimônia desnecessária.

---

## Tese central

Componente React bom tem responsabilidade clara.

A pergunta correta não é:

“posso quebrar isso em mais componentes?”

A pergunta correta é:

“essa decomposição melhora legibilidade, reuso real, teste, boundary ou manutenção sem criar fragmentação artificial?”

Componente grande demais vira bagunça.  
Componente fragmentado demais vira labirinto.

---

## Método

### 1. Identificar papel do componente

Antes de alterar ou criar, declarar:

- o que o componente representa;
- se é página, feature, layout, primitive, widget ou componente de apresentação;
- quem consome o componente;
- quais dados recebe;
- quais eventos emite;
- qual responsabilidade não deve ter.

---

### 2. Verificar convenções locais

Procurar padrões existentes no projeto:

- organização de pastas;
- nomenclatura;
- co-location;
- separação entre page/feature/components;
- uso de design system;
- estilo de props;
- testes;
- padrão de forms;
- padrão de chamadas API;
- padrão de error/loading/empty states.

Não impor arquitetura genérica de React se o projeto já tem convenção local.

---

### 3. Separar responsabilidades

Avaliar se o componente mistura indevidamente:

- layout;
- regra de negócio;
- data fetching;
- transformação de dados;
- estado de formulário;
- renderização;
- validação;
- side effects;
- roteamento;
- autorização visual.

Mistura nem sempre é erro, mas precisa ser proporcional ao tamanho e ao risco.

---

### 4. Avaliar decomposição

Decompor quando:

- há bloco visual com nome claro;
- há repetição real;
- há responsabilidade independente;
- há props simples;
- há melhora de leitura;
- há teste ou reuso plausível;
- há redução de complexidade local.

Não decompor quando:

- o subcomponente teria nome artificial;
- o componente extra só embrulha JSX;
- a separação exige props demais;
- o fluxo fica mais difícil de seguir;
- o reuso é hipotético.

---

### 5. Avaliar props

Props devem ser:

- explícitas;
- mínimas;
- estáveis;
- nomeadas pelo domínio da UI;
- sem vazamento excessivo de estrutura interna;
- sem passar objetos gigantes quando campos pequenos bastam.

Evitar prop drilling excessivo.  
Mas não criar estado global só para evitar duas passagens de props.

---

### 6. Avaliar estados visuais

Componentes que carregam dados ou representam fluxo devem considerar:

- loading;
- empty;
- error;
- success;
- disabled;
- pending;
- optimistic, se aplicável;
- permission denied, se aplicável.

Não tratar apenas caminho feliz.

---

### 7. Avaliar acessibilidade mínima

Quando aplicável, verificar:

- labels;
- botões reais;
- foco;
- semântica HTML;
- aria apenas quando necessário;
- navegação por teclado;
- texto alternativo;
- estados desabilitados compreensíveis.

---

### 8. Avaliar segurança de renderização

Se renderiza conteúdo externo:

- não usar HTML bruto sem sanitização;
- não confiar em dado vindo de usuário;
- não expor dados sensíveis;
- não tratar frontend como autorização real.

Quando houver risco, acionar `frontend-security-baseline`.

---

## Output esperado

```md
# React Component Architecture Review

## Componente/área analisada
<componente, página ou feature>

## Papel do componente
<page | feature | layout | presentational | primitive | widget | outro>

## Responsabilidades atuais/propostas
- <responsabilidade 1>
- <responsabilidade 2>

## Boundaries
<o que pertence e o que não pertence ao componente>

## Decomposição
<manter | decompor | consolidar | investigar>

## Props
<análise de shape, clareza e acoplamento>

## Estados visuais
<loading, empty, error, disabled, etc>

## Acessibilidade
<análise curta ou não aplicável>

## Riscos
- <risco 1>
- <risco 2>

## Veredito
<suficiente | ajustar | escalar>

## Risco residual
<risco que permanece>
```

---

## Checklist de qualidade

Antes de aceitar o componente, verificar:

- o papel do componente está claro?
- a estrutura segue convenção local?
- há responsabilidade demais em um único arquivo?
- a decomposição melhora leitura ou só cria fragmentação?
- props são mínimas e explícitas?
- há prop drilling problemático?
- estados loading/empty/error foram considerados?
- não há lógica de autorização confiada só à UI?
- conteúdo externo é renderizado com segurança?
- acessibilidade mínima foi considerada?
- o diff é proporcional à task?

---

## Critérios de escalonamento

Escalar quando:

- a mudança redefinir arquitetura de frontend;
- houver disputa entre estado local, contexto global e data fetching externo;
- componente crescer por necessidade de produto maior que o escopo;
- houver risco de segurança no frontend;
- houver mudança relevante em design system;
- a feature exigir decisão de UX/produto;
- a decomposição alterar boundaries importantes.

---

## Anti-patterns

Evitar:

- componente de 500 linhas sem fronteira clara;
- decompor JSX em componentes sem nome real;
- criar pasta para cada componente pequeno por ritual;
- passar objeto gigante como prop por conveniência;
- usar estado global para dado local;
- misturar fetch, transformação pesada e renderização complexa sem motivo;
- esconder regra de autorização apenas na UI;
- duplicar componente visual em vez de extrair padrão real;
- criar abstração de componente antes de segunda ocorrência;
- aplicar design pattern React por hype.

---

## Declaração operacional curta

Componente React bom tem responsabilidade clara, props compreensíveis e decomposição proporcional.  
A arquitetura de UI deve reduzir confusão, não criar labirinto.