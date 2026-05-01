# Skill — .NET Solution Ops

## Finalidade

Esta skill orienta leitura, operação e validação de solutions e projects em C#/.NET.

Seu papel é ajudar o agente a entender a estrutura real de uma solução .NET antes de alterar código, referências, projetos, comandos, testes ou build.

A skill não ensina .NET do zero.  
Ela define um método operacional para trabalhar com soluções .NET sem inventar estrutura, comando ou dependência.

---

## Quando usar

Use esta skill quando a task tocar:

- `.sln`;
- `.csproj`;
- múltiplos projects;
- referências entre projects;
- build;
- test;
- restore;
- package;
- target framework;
- estrutura de backend;
- organização de camadas/módulos;
- erro de compilação;
- configuração de projeto;
- adição ou remoção de project;
- alteração que pode afetar dependency graph.

---

## Quando não usar

Não use esta skill quando:

- a task não envolve .NET;
- o arquivo alvo é isolado e a solution já foi descoberta;
- a mudança é puramente documental;
- os comandos locais já estão claros e a skill só repetiria informação.

---

## Tese central

Solution .NET é mapa operacional do backend.

Antes de editar, o agente precisa entender:

- quais projects existem;
- quem referencia quem;
- quais comandos são autoridade;
- onde ficam testes;
- qual target framework está em uso;
- quais boundaries locais existem;
- como build e test são executados neste workspace.

Conhecimento genérico de .NET não vence a estrutura real do repositório.

---

## Método

### 1. Localizar solution e projects

Procurar:

- arquivos `.sln`;
- arquivos `.csproj`;
- `Directory.Build.props`;
- `Directory.Packages.props`;
- `global.json`;
- `NuGet.config`;
- projetos de teste;
- projetos de API;
- projetos de domínio/aplicação/infra, se existirem.

Registrar se há uma solution principal ou múltiplas solutions.

---

### 2. Entender grafo de projects

Identificar:

- project de entrada;
- projects de biblioteca;
- projects de teste;
- referências entre projects;
- dependências externas;
- boundaries de módulo;
- dependências suspeitas ou invertidas.

Atenção especial a referências que quebram intenção arquitetural.

---

### 3. Confirmar target e SDK

Verificar:

- target framework;
- SDK version;
- nullable context;
- implicit usings;
- language version;
- package management centralizado;
- warnings como errors, se aplicável.

Não assumir versão de .NET.

---

### 4. Localizar comandos de autoridade

Preferir comandos do projeto:

- `LOCAL_COMMANDS.md`;
- README;
- scripts;
- Makefile;
- pipeline;
- docs;
- comandos já usados no repo.

Se não houver comando local, sugerir comando padrão com ressalva.

Exemplos possíveis:

```bash
dotnet restore
dotnet build
dotnet test
```

Mas esses comandos não devem ser tratados como autoridade se o projeto define outra forma.

---

### 5. Entender organização local

Mapear se o projeto usa:

- modular monolith;
- vertical slices;
- camadas tradicionais;
- Clean/Hexagonal simplificada;
- minimal APIs;
- controllers;
- feature folders;
- separação por bounded context;
- projects por camada;
- projects por módulo.

Não impor arquitetura externa.

---

### 6. Avaliar impacto da mudança

Antes de alterar:

- qual project será tocado?
- há teste correspondente?
- a referência atual permite essa alteração?
- a mudança exige novo package?
- a mudança exige novo project reference?
- a alteração quebra boundary?
- o build de qual solution/project deve rodar?

---

### 7. Validar

Validação típica:

```bash
dotnet build <solution-or-project>
dotnet test <solution-or-project>
```

Quando aplicável:

```bash
dotnet format --verify-no-changes
```

Mas sempre respeitar authority commands locais.

---

## Output esperado

```md
# .NET Solution Ops Note

## Solution/projects analisados
- <solution/project 1>
- <solution/project 2>

## Estrutura relevante
<API, tests, domain, infra, modules, etc>

## Target/SDK
<target framework, SDK, global.json, observações>

## Grafo de dependências
<resumo das referências relevantes>

## Comandos de autoridade
- <comando 1>
- <comando 2>

## Área de impacto
- <project/arquivo 1>
- <project/arquivo 2>

## Riscos
- <risco 1>
- <risco 2>

## Validação recomendada
- <build/test/format>

## Veredito
<suficiente | ajustar | investigar mais | escalar>
```

---

## Checklist de qualidade

Antes de agir, verificar:

- a solution principal foi identificada?
- os projects relevantes foram localizados?
- target framework foi verificado?
- comandos locais foram procurados?
- project references foram entendidas?
- a mudança respeita boundaries?
- testes relacionados foram localizados?
- novo package é realmente necessário?
- validação está definida?
- há risco de build quebrar em outro project?

---

## Critérios de escalonamento

Escalar quando:

- a mudança exigir novo project;
- a mudança alterar referências entre módulos;
- houver risco de boundary quebrado;
- houver conflito entre arquitetura documentada e structure real;
- build/test estiverem quebrados antes da task;
- não houver comando confiável de validação;
- a mudança exigir package relevante;
- a alteração afetar múltiplos projects de forma estrutural.

---

## Anti-patterns

Evitar:

- editar sem localizar `.sln`/`.csproj`;
- assumir Clean Architecture por padrão;
- adicionar interface/project sem dor real;
- criar project novo para feature simples;
- adicionar package sem checar alternativa existente;
- rodar comando genérico ignorando script local;
- tratar erro de build como detalhe;
- misturar reorganização de solution com feature.

---

## Declaração operacional curta

Solution .NET é mapa de execução e dependência.  
Antes de mudar código, entenda projects, references, comandos e boundaries locais.