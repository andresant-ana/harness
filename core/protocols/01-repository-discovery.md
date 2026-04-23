# Descoberta de Repositório

## Finalidade

Este protocolo define como o harness deve entender um repositório antes de alterar qualquer coisa relevante.

Seu papel é impedir que o agente opere “cego”, baseado em leitura parcial, heurística preguiçosa ou inferência genérica sobre a arquitetura do projeto.

---

## Tese central

Antes de ler muito, o sistema deve descobrir bem.

Discovery não é varredura indiscriminada.  
Discovery é construção de mapa estrutural suficiente para orientar plan, execução, review e handoff.

---

## Objetivos do discovery

O discovery deve responder:

1. qual é a topologia do repositório;
2. quais módulos, contextos ou camadas existem;
3. onde estão os authority files;
4. onde estão os authority commands;
5. quais áreas provavelmente serão tocadas;
6. quais regiões são estruturalmente sensíveis;
7. quais artefatos locais precisam ser respeitados.

---

## Ordem correta de discovery

### 1. Reconhecimento da raiz
Identificar:
- diretórios principais;
- arquivos de configuração;
- arquivos de documentação local;
- presença de `AGENTS.md`, `opencode.json`, `.opencode/`, `docs/`, `src/`, `tests/` e equivalentes.

### 2. Localização de authority sources
Priorizar arquivos e comandos que dizem como o projeto realmente funciona.

### 3. Leitura da topologia
Entender:
- módulos;
- boundaries;
- separação entre domínio, aplicação, infraestrutura e interfaces, se existir;
- convenção de naming;
- pontos de entrada.

### 4. Localização da área afetada
Responder:
- onde a task provavelmente toca;
- o que pode ser impactado;
- que partes não precisam ser abertas.

### 5. Leitura focalizada
Só então aprofundar nos arquivos específicos realmente necessários.

---

## Discovery mínimo esperado

Para uma task relevante, o discovery deve ao menos identificar:

- linguagem e stack dominante;
- pontos de entrada;
- localização de código de negócio;
- localização de teste;
- configuração de build/test/lint;
- estrutura principal do projeto;
- region of change provável;
- commands reais para validação.

---

## O que deve ser evitado

O discovery deve evitar:

- leitura massiva de arquivos sem critério;
- confiar apenas em nomes de pastas;
- concluir arquitetura sem verificar convenções e configurações;
- abrir muitos arquivos porque “talvez precise”;
- assumir que padrão conhecido de framework reflete a realidade do repo.

---

## Heurística de profundidade

### Discovery leve
Use quando:
- a task for pequena;
- o impacto estiver muito localizado;
- a topologia já estiver clara;
- a verdade local estiver bem documentada.

### Discovery moderado
Use quando:
- a task tocar múltiplos arquivos;
- a arquitetura local ainda não estiver clara;
- houver integração ou risco funcional moderado.

### Discovery forte
Use quando:
- a task tocar mudança estrutural;
- o projeto for grande ou confuso;
- a classe de risco estiver entre R2 e R3;
- houver risco real de over-engineering, impacto sistêmico ou interpretação errada.

---

## Resultado esperado do discovery

Ao final do discovery, o sistema deve ser capaz de dizer com clareza:

- quais arquivos ou áreas precisam ser lidos com profundidade;
- quais arquivos podem ser ignorados;
- qual é a narrativa estrutural do repositório;
- onde a task vive dentro dessa narrativa.

Se isso ainda não estiver claro, o discovery ainda não terminou.

---

## Relação com contexto

Discovery bom reduz custo de contexto.

Quanto melhor o mapa estrutural:
- menos leitura inútil;
- menos chance de ignorar arquivo crítico;
- menor chance de contexto inflado;
- menor chance de o plan nascer em falso.

---

## Relação com slop

Discovery ruim é uma das principais origens de slop.

Sem discovery:
- o agente duplica abstração;
- toca lugar errado;
- ignora convenção local;
- interpreta mal dependências;
- aumenta a entropia do sistema.

---

## Saída esperada do discovery

O discovery pode produzir:
- trecho específico no Execution Plan;
- Investigation Note;
- lista de authority sources;
- mapeamento curto da topologia;
- riscos de navegação e interpretação.

---

## Declaração operacional curta

Não comece pela edição.  
Comece pelo mapa.  
Quem entende o repositório antes de tocar nele erra menos, consome menos contexto e preserva melhor a arquitetura local.