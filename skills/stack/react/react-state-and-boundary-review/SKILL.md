# Skill — React State and Boundary Review

## Finalidade

Esta skill orienta a revisão de estado, efeitos, hooks, data fetching, sincronização e boundaries em React.

Seu papel é impedir que o agente use `useEffect`, estado global, context, props ou fetching como cola universal, criando acoplamento, bugs de renderização, loops, estados duplicados ou UI difícil de raciocinar.

Esta skill não substitui julgamento de arquitetura frontend.  
Ela ajuda a decidir onde o estado deve viver, quem deve ser fonte de verdade e quais efeitos são realmente necessários.

---

## Quando usar

Use esta skill quando a task tocar:

- `useState`;
- `useEffect`;
- `useMemo`;
- `useCallback`;
- custom hooks;
- Context API;
- estado global;
- estado compartilhado;
- data fetching;
- cache client-side;
- formulário;
- sincronização com URL;
- renderização condicional;
- bug de re-render;
- props derivadas;
- loading/error state;
- optimistic UI;
- integração com API;
- boundary entre UI, state e servidor.

---

## Quando não usar

Não use esta skill quando:

- a mudança for visual estática;
- não houver estado, efeito ou fetching relevante;
- o estado já estiver localizado e a alteração for mínima;
- a task for melhor coberta por `react-component-architecture`;
- a análise seria especulativa sem sintoma real.

---

## Tese central

Estado tem dono.

Grande parte da complexidade em React nasce quando o projeto não sabe responder:

- qual é a fonte de verdade?
- este estado é local, derivado, remoto ou global?
- este `useEffect` representa efeito real ou cálculo disfarçado?
- este dado precisa ser sincronizado ou apenas calculado?
- este componente deveria saber disso?

Estado mal posicionado cria bugs invisíveis.

---

## Tipos de estado

### Estado local

Use para:

- interação local;
- toggle;
- input temporário;
- UI state pequeno;
- modal aberto/fechado;
- seleção local.

Não promover para global sem dor real.

---

### Estado derivado

Use cálculo em vez de estado duplicado quando o valor pode ser derivado de props, query result ou outro estado.

Evitar:

- duplicar props em `useState`;
- sincronizar manualmente valores calculáveis;
- `useEffect` só para calcular valor derivado.

---

### Estado remoto

Dados vindos de API/banco/backend devem ter fonte de verdade clara.

Perguntar:

- há cache?
- há invalidação?
- há loading/error?
- há refetch?
- há stale data?
- há optimistic update?
- há rollback?

---

### Estado global

Use apenas quando:

- múltiplas áreas distantes precisam do mesmo dado;
- prop drilling ficou realmente custoso;
- há conceito global real, como auth/session/theme/tenant;
- há lifecycle e invalidação claros.

Não usar global como atalho para design ruim de componentes.

---

### Estado de URL

Use URL quando:

- precisa ser compartilhável;
- precisa sobreviver refresh;
- representa filtro, paginação, aba, busca ou navegação;
- melhora navegação/back button.

---

## Método

### 1. Identificar fonte de verdade

Perguntar:

- quem é dono do dado?
- o backend?
- a URL?
- um componente pai?
- o próprio componente?
- contexto global?
- cache client-side?

Se houver duas fontes de verdade, há risco.

---

### 2. Classificar estado

Classificar cada estado como:

- local;
- derivado;
- remoto;
- global;
- URL;
- formulário;
- temporário;
- persistido.

---

### 3. Revisar efeitos

Para cada `useEffect`, perguntar:

- qual efeito externo ele sincroniza?
- ele faz I/O?
- mexe em subscription?
- depende de timer?
- sincroniza URL?
- ou está apenas calculando valor derivado?

Se for cálculo, preferir render derivation, `useMemo` quando necessário, ou simples variável.

---

### 4. Revisar dependências de hooks

Verificar:

- dependency array correta;
- closure obsoleta;
- função recriada sem necessidade;
- loop de render;
- efeito disparando mais do que deveria;
- cleanup necessário.

---

### 5. Revisar data fetching

Perguntar:

- fetching está no nível certo?
- componente de apresentação está buscando dado sem necessidade?
- loading/error/empty foram tratados?
- refetch e invalidação fazem sentido?
- há duplicação de chamadas?
- há race condition?
- há cancelamento ou proteção contra update após unmount, quando aplicável?

---

### 6. Revisar boundaries

Separar:

- componente de UI;
- hook de estado;
- client de API;
- transformação de dados;
- validação;
- regra de negócio;
- roteamento.

Não misturar tudo em componente visual se isso prejudicar leitura.

---

### 7. Revisar performance de renderização

Perguntar:

- estado está alto demais na árvore?
- re-renderiza filhos demais?
- context muda com frequência?
- memoização é necessária ou ornamental?
- listas têm keys estáveis?
- handlers causam prop churn relevante?

Não usar `useMemo`/`useCallback` como decoração.

---

## Output esperado

```md
# React State and Boundary Review

## Componente/fluxo analisado
<componente, página, hook ou feature>

## Fonte de verdade
<backend | URL | local | parent | context | cache | incerta>

## Estados identificados
- <estado>: <local | derivado | remoto | global | URL | form | temporário>

## Effects/hooks
<análise de useEffect/custom hooks/dependencies>

## Data fetching
<localização, loading/error, cache, invalidação>

## Boundaries
<UI, hook, API client, transformação, regra>

## Riscos
- <risco 1>
- <risco 2>

## Ação recomendada
<manter | mover estado | derivar | extrair hook | reduzir global | escalar>

## Veredito
<suficiente | ajustar | escalar>

## Risco residual
<risco que permanece>
```

---

## Checklist de qualidade

Antes de aceitar, verificar:

- fonte de verdade está clara?
- há estado duplicado que deveria ser derivado?
- `useEffect` representa efeito real?
- dependency arrays estão corretas?
- há risco de render loop?
- estado global é realmente necessário?
- fetching está no boundary certo?
- loading/error/empty foram considerados?
- URL deveria guardar filtros/paginação?
- context não está amplo demais?
- memoização é necessária ou ornamental?
- estado não subiu demais na árvore?

---

## Critérios de escalonamento

Escalar quando:

- a decisão redefinir arquitetura de estado do frontend;
- houver troca ou introdução de biblioteca de state/data fetching;
- estado global passar a coordenar múltiplos domínios;
- fluxo envolver auth/session/tenant;
- houver conflito entre UX, performance e simplicidade;
- a correção exigir refactor amplo;
- frontend estiver tentando compensar ausência de contrato backend.

---

## Anti-patterns

Evitar:

- `useEffect` para calcular valor derivado;
- duplicar props em state sem motivo;
- context global para estado local;
- store global como lixeira;
- fetching dentro de componente puramente visual;
- loading/error ignorados;
- dependency array manipulada para calar linter;
- memoização em tudo;
- estado alto demais na árvore;
- custom hook que esconde regra crítica sem boundary claro;
- frontend tentando ser fonte de verdade de dado que pertence ao backend.

---

## Declaração operacional curta

Estado React precisa de dono, boundary e motivo.  
Se a fonte de verdade não está clara, o bug já começou.