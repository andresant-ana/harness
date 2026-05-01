# Skill — Consistency Scanner

## Finalidade

Esta skill orienta a busca por inconsistências internas em código, documentação, nomenclatura, estrutura, artifacts e convenções.

Seu papel é impedir que o projeto acumule pequenas divergências que dificultam navegação, review, automação e continuidade por agentes ou humanos.

---

## Quando usar

Use esta skill quando houver risco de:

- nomes diferentes para o mesmo conceito;
- padrões duplicados;
- arquivos parecidos com responsabilidades divergentes;
- documentação contraditória;
- schemas e templates desalinhados;
- comandos descritos de formas diferentes;
- artifacts com campos incompatíveis;
- estrutura de diretórios inconsistente;
- convenção local ignorada;
- mudança que cria padrão paralelo.

---

## Quando não usar

Não use esta skill quando:

- a task é simples e não afeta consistência;
- a inconsistência é puramente estética e irrelevante;
- a varredura aumentaria contexto sem decisão;
- o problema já está claramente delimitado.

---

## Tese central

Consistência reduz carga cognitiva.

Quanto mais o projeto usa os mesmos nomes, formatos, padrões e fronteiras para as mesmas ideias, mais fácil fica para humano, agente e Core Architect entenderem e evoluírem o sistema.

Consistência não é uniformidade cega.  
Consistência é previsibilidade útil.

---

## Método

### 1. Definir o eixo de consistência

Antes de escanear, declarar o que será comparado.

Exemplos:

- nomenclatura;
- estrutura de arquivos;
- campos de artifacts;
- comandos;
- formato de documentação;
- padrões de erro;
- organização de módulos;
- contratos HTTP;
- nomes de domínio.

---

### 2. Localizar referência principal

Encontrar fonte de verdade:

- arquivo atual mais maduro;
- schema canônico;
- template;
- documento de authority;
- convenção dominante no repositório;
- policy ou protocol aplicável.

---

### 3. Comparar amostras relevantes

Não ler o repo inteiro sem critério.

Comparar:

- arquivos diretamente relacionados;
- exemplos existentes;
- templates equivalentes;
- variações do mesmo padrão;
- nomes do mesmo conceito em camadas diferentes.

---

### 4. Classificar inconsistência

Classificar como:

- intencional;
- aceitável;
- ruído leve;
- risco de confusão;
- drift real;
- contradição bloqueante.

---

### 5. Recomendar correção proporcional

Ações possíveis:

- não agir;
- ajustar nome;
- alinhar documentação;
- consolidar padrão;
- criar follow-up;
- escalar se a inconsistência revelar decisão não resolvida.

---

## Output esperado

```md
# Consistency Scan

## Eixo analisado
<nomenclatura, estrutura, docs, artifacts, comandos, etc>

## Referência principal
<fonte usada como padrão>

## Inconsistências encontradas
- <inconsistência 1>
- <inconsistência 2>

## Classificação
<intencional | aceitável | ruído leve | risco de confusão | drift | bloqueante>

## Impacto
<como afeta navegação, review, execução ou continuidade>

## Ação recomendada
<não agir | ajustar agora | documentar | follow-up | escalar>

## Risco residual
<risco que permanece>
```

---

## Checklist de qualidade

Antes de concluir, verificar:

- o eixo de comparação foi definido?
- existe referência principal?
- a inconsistência é real ou só estilo?
- há impacto prático?
- a correção cabe no escopo?
- a correção pode gerar diff desnecessário?
- há risco de mudar comportamento?
- precisa virar follow-up?

---

## Critérios de escalonamento

Escalar quando:

- a inconsistência revelar decisão arquitetural pendente;
- houver conflito entre documentos de autoridade;
- não estiver claro qual padrão deve vencer;
- a correção exigir mudança ampla;
- a inconsistência afetar segurança, operação ou dados;
- o agente precisar escolher entre convenções concorrentes.

---

## Anti-patterns

Evitar:

- varrer tudo sem pergunta;
- renomear em massa por estética;
- impor consistência que quebra contexto local;
- corrigir estilo em task funcional sem necessidade;
- confundir variação intencional com erro;
- criar padrão novo enquanto tenta alinhar consistência;
- transformar scan em refactor amplo.

---

## Declaração operacional curta

Consistência boa reduz ruído e melhora navegação.  
Scanner bom procura divergência com impacto, não perfeição estética.