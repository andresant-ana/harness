# Skill — Frontend Security Baseline

## Finalidade

Esta skill orienta a revisão de segurança em frontend, especialmente exposição de dados, tokens, XSS, manipulação de estado, chamadas de API, rendering de conteúdo e limites entre cliente e servidor.

Seu papel é impedir que o agente trate o frontend como camada confiável ou armazene/exponha dados sensíveis indevidamente.

---

## Quando usar

Use esta skill quando a task tocar:

- React;
- componentes que renderizam dados externos;
- formulários;
- auth no frontend;
- token;
- localStorage/sessionStorage;
- cookies;
- chamadas de API;
- upload;
- download;
- HTML dinâmico;
- markdown renderizado;
- links externos;
- redirects;
- feature flags;
- dados privados na UI.

---

## Quando não usar

Não use esta skill quando:

- a mudança for visual e estática sem dados externos;
- não houver input, auth, token ou API;
- a análise duplicar revisão de segurança já feita.

---

## Tese central

Frontend não é fronteira de confiança.

Tudo que está no cliente pode ser visto, alterado ou chamado manualmente.

Segurança real precisa existir no backend, mas o frontend também deve evitar exposição, XSS e armazenamento inseguro.

---

## Método

### 1. Identificar dados renderizados

Perguntar:

- os dados vêm de usuário?
- vêm de API externa?
- contêm HTML?
- contêm markdown?
- contêm dado sensível?
- podem conter script, URL ou payload malicioso?

---

### 2. Avaliar XSS

Verificar:

- uso de HTML bruto;
- markdown sem sanitização;
- dangerouslySetInnerHTML;
- templates dinâmicos;
- atributos de URL;
- conteúdo vindo de usuário;
- bibliotecas de sanitização.

---

### 3. Avaliar armazenamento

Perguntar:

- token está em localStorage?
- dado sensível fica persistido?
- sessionStorage é necessário?
- cookie tem flags adequadas?
- frontend guarda segredo que deveria estar no backend?

Nunca colocar segredo real no frontend.

---

### 4. Avaliar autorização aparente

Verificar:

- UI esconde botão, mas backend autoriza?
- rota protegida no frontend é apenas conveniência?
- dados privados são filtrados no backend?
- há risco de usuário chamar API manualmente?

---

### 5. Avaliar chamadas de API

Perguntar:

- erros expõem detalhes?
- token é enviado corretamente?
- endpoint é chamado com dados mínimos?
- há CSRF quando cookie-based auth?
- redirect externo é validado?

---

### 6. Avaliar dependências frontend

Quando houver biblioteca nova:

- justificar necessidade;
- avaliar segurança;
- avaliar bundle;
- avaliar manutenção;
- evitar biblioteca para tarefa trivial.

---

## Output esperado

```md
# Frontend Security Baseline Review

## Superfície analisada
<componente, página, fluxo, formulário ou chamada API>

## Dados externos renderizados
- <dado 1>
- <dado 2>

## Risco de XSS
<baixo | moderado | alto | incerto>

## Tokens/dados sensíveis
<análise curta>

## Autorização real
<backend enforcement | apenas UI | incerto>

## Storage
<localStorage | sessionStorage | cookie | memória | não aplicável>

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

Antes de aceitar, verificar:

- conteúdo externo é escapado/sanitizado?
- não há HTML bruto inseguro?
- token não está exposto indevidamente?
- segredo não está no frontend?
- dado sensível não é persistido sem necessidade?
- backend impõe autorização?
- UI não é a única barreira?
- redirect externo é seguro?
- erros não expõem detalhes internos?
- dependência frontend foi justificada?

---

## Critérios de escalonamento

Escalar quando:

- houver token ou dado sensível no cliente;
- houver HTML/markdown de usuário;
- houver mudança em auth frontend;
- houver cookie/session security;
- houver risco de CSRF;
- houver redirect externo;
- houver exposição de dados privados;
- a correção exigir mudança backend.

---

## Anti-patterns

Evitar:

- segredo em variável frontend;
- confiar em esconder botão;
- usar localStorage para token sensível sem decisão consciente;
- renderizar HTML de usuário;
- abrir link externo sem proteção adequada;
- confiar em validação client-side;
- retornar entidade inteira para frontend filtrar;
- usar frontend como camada de autorização.

---

## Declaração operacional curta

Frontend melhora experiência, não estabelece confiança.  
Tudo que importa em segurança precisa ser validado e autorizado no backend.