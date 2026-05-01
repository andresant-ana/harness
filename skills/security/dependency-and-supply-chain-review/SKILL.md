# Skill — Dependency and Supply Chain Review

## Finalidade

Esta skill orienta a avaliação de dependências, pacotes, bibliotecas, SDKs, ferramentas e componentes externos antes de introduzir, atualizar ou substituir no projeto.

Seu papel é impedir que o agente importe complexidade, risco de supply chain, vulnerabilidade ou acoplamento externo sem necessidade real.

---

## Quando usar

Use esta skill quando a task envolver:

- nova dependência;
- atualização de dependência;
- remoção de dependência;
- novo SDK;
- novo package de build;
- nova action de CI;
- novo container base;
- nova ferramenta de dev;
- nova integração de terceiro;
- alerta de vulnerabilidade;
- lockfile;
- package manager;
- plugin ou extensão.

---

## Quando não usar

Não use esta skill quando:

- não houver dependência envolvida;
- a alteração for puramente documental;
- a dependência já estiver aprovada e a task não mexer nela;
- a análise duplicar uma policy já aplicada sem novo risco.

---

## Tese central

Dependência é código de outra pessoa rodando no seu sistema.

Toda dependência precisa justificar:

- valor;
- necessidade;
- manutenção;
- segurança;
- licença;
- custo;
- acoplamento;
- risco operacional.

---

## Método

### 1. Identificar a dependência

Registrar:

- nome;
- tipo;
- versão;
- origem;
- package manager;
- finalidade;
- onde será usada;
- runtime ou dev-only.

---

### 2. Justificar necessidade

Perguntar:

- qual problema ela resolve?
- há recurso nativo que resolve?
- há biblioteca já existente no projeto?
- seria simples implementar localmente?
- a dependência reduz risco ou só economiza digitação?

Dependência precisa reduzir complexidade líquida ou risco real.

---

### 3. Avaliar manutenção

Verificar, quando possível:

- projeto ativo;
- frequência de releases;
- issues críticas;
- documentação;
- adoção;
- compatibilidade com stack;
- maturidade.

Popularidade ajuda, mas não garante segurança.

---

### 4. Avaliar segurança

Considerar:

- vulnerabilidades conhecidas;
- scripts de instalação;
- transitive dependencies;
- permissões;
- origem do pacote;
- risco de typosquatting;
- risco de maintainer compromise;
- impacto se a dependência for comprometida.

---

### 5. Avaliar licença

Verificar se a licença é compatível com o projeto.

Se a licença for desconhecida, registrar lacuna.

---

### 6. Avaliar impacto operacional

Perguntar:

- aumenta bundle?
- aumenta cold start?
- afeta performance?
- afeta build?
- afeta deploy?
- exige configuração sensível?
- cria lock-in?
- exige credencial?

---

### 7. Definir validação

Recomendar:

- build;
- test;
- lockfile review;
- vulnerability scan;
- license check;
- diff review;
- changelog review;
- teste funcional.

---

## Output esperado

```md
# Dependency and Supply Chain Review

## Dependência
<nome, versão e origem>

## Tipo
<runtime | dev | SDK | CI | container | plugin | outro>

## Finalidade
<problema resolvido>

## Alternativas consideradas
- <alternativa 1>
- <alternativa 2>

## Justificativa
<por que a dependência é necessária>

## Riscos de supply chain
- <risco 1>
- <risco 2>

## Licença
<compatível | incerta | incompatível | não verificada>

## Impacto operacional
<bundle, build, runtime, deploy, cold start, lock-in>

## Validação recomendada
- <validação 1>
- <validação 2>

## Veredito
<aceitar | rejeitar | adiar | escalar>

## Risco residual
<risco que permanece>
```

---

## Checklist de qualidade

Antes de aceitar, verificar:

- a dependência resolve dor real?
- alternativa nativa foi considerada?
- já existe algo no projeto que resolve?
- é runtime ou dev-only?
- manutenção é aceitável?
- licença foi considerada?
- vulnerabilidade foi considerada?
- lockfile foi revisado?
- impacto em build/deploy foi considerado?
- risco residual foi registrado?

---

## Critérios de escalonamento

Escalar quando:

- a dependência for crítica;
- tocar segurança, auth, criptografia ou dados sensíveis;
- tiver licença incerta;
- tiver vulnerabilidade conhecida relevante;
- exigir segredo ou permissão externa;
- alterar arquitetura;
- criar lock-in importante;
- houver dúvida entre implementar localmente ou importar pacote.

---

## Anti-patterns

Evitar:

- adicionar pacote para poucas linhas simples;
- instalar dependência por tentativa e erro;
- ignorar lockfile;
- ignorar transitive dependencies;
- atualizar major version sem changelog;
- usar pacote abandonado;
- usar package parecido com nome conhecido sem verificar origem;
- aceitar SDK externo sem entender permissões;
- tratar dev dependency como irrelevante.

---

## Declaração operacional curta

Dependência é complexidade e confiança importadas.  
Só entra quando a dor real justifica o custo e o risco.