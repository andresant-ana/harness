# Skill — Bash Linux Ops

## Finalidade

Esta skill orienta o uso seguro, preciso e verificável de shell Linux/Bash em tarefas do harness.

Seu papel é impedir que o agente execute comandos destrutivos, amplos, opacos ou baseados em suposição, especialmente em ambientes WSL, Linux local, containers ou CI.

---

## Quando usar

Use esta skill quando a task envolver:

- comandos Bash;
- criação de diretórios e arquivos;
- inspeção de filesystem;
- busca com `find`, `grep`, `rg`, `sed`, `awk`;
- scripts locais;
- permissões;
- variáveis de ambiente;
- execução de comandos de build/test;
- manipulação de texto;
- operações em lote;
- diagnóstico em Linux/WSL/container.

---

## Quando não usar

Não use esta skill quando:

- não houver comando shell;
- a ação já estiver definida por authority command local;
- a task for puramente documental;
- o comando for trivial e sem risco.

---

## Tese central

Shell é ferramenta de precisão e também de dano.

O agente deve preferir comandos:

- pequenos;
- legíveis;
- reversíveis;
- verificáveis;
- restritos ao escopo;
- sem efeito destrutivo implícito.

---

## Método

### 1. Definir intenção do comando

Antes de executar, saber:

- o que o comando deve descobrir ou alterar;
- em qual diretório deve rodar;
- qual saída é esperada;
- se é read-only ou mutação;
- qual é o risco se estiver errado.

---

### 2. Confirmar diretório

Antes de comandos relevantes, usar:

```bash
pwd
```

ou garantir explicitamente:

```bash
cd ~/engineering/harness
```

Nunca assumir diretório atual.

---

### 3. Preferir inspeção antes de mutação

Antes de alterar, inspecionar:

```bash
find <path> -maxdepth 2 -type f | sort
git status
git diff --stat
```

---

### 4. Usar comandos restritos

Preferir comandos com paths explícitos.

Bom:

```bash
find skills/platform -type f | sort
```

Ruim:

```bash
find . -type f
```

quando o escopo necessário é menor.

---

### 5. Evitar comandos destrutivos sem aprovação

Tratar com alto cuidado:

```bash
rm -rf
git reset --hard
git clean -fd
chmod -R
chown -R
find . -delete
sed -i
```

Comandos destrutivos exigem escopo claro, inspeção prévia e autorização quando houver risco.

---

### 6. Validar resultado

Após comando de mutação, verificar:

```bash
git status
git diff --check
find <path> -type f | sort
```

---

## Output esperado

```md
# Bash/Linux Ops Note

## Objetivo do comando
<o que precisa ser feito>

## Diretório alvo
<path>

## Comandos propostos
```bash
<comando>
```

## Classificação
<read-only | mutação local | sensível>

## Riscos
- <risco 1>
- <risco 2>

## Validação pós-comando
```bash
<comando de validação>
```

## Veredito
<executar | ajustar | escalar>
```

---

## Checklist de qualidade

Antes de rodar comando relevante, verificar:

- o diretório está correto?
- o comando tem escopo restrito?
- o comando é read-only ou mutante?
- há risco de apagar, sobrescrever ou mover arquivos?
- há alternativa mais segura?
- o output esperado está claro?
- há validação depois?
- comando destrutivo foi aprovado?

---

## Critérios de escalonamento

Escalar quando:

- comando pode apagar arquivos;
- comando pode alterar muitos arquivos;
- comando toca produção, segredo ou config sensível;
- comando depende de glob amplo;
- comando envolve permissão de sistema;
- comando não é compreendido;
- comando executa script externo não auditado.

---

## Anti-patterns

Evitar:

- rodar comando sem `pwd` ou contexto;
- usar glob amplo por pressa;
- usar `rm -rf` como limpeza padrão;
- pipe destrutivo sem preview;
- `curl | bash`;
- script externo sem leitura;
- mutação em lote sem `git diff`;
- comando que resolve no ambiente do agente, mas não no workspace real.

---

## Declaração operacional curta

Bash deve ser usado com escopo, intenção e validação.  
Comando que não pode ser explicado não deve ser executado.