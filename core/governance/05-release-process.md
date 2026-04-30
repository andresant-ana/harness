# Processo de Release do Harness

## Finalidade

Este documento define como versionar, congelar e liberar versões do harness.

Seu papel é impedir que a engenharia mude continuamente sem marco, sem changelog, sem revisão e sem critério de estabilidade.

Release existe para transformar evolução em versão governável.

---

## Tese central

Harness precisa de versão porque comportamento precisa ser rastreável.

Quando a engenharia muda, o comportamento esperado do agente também muda.

Sem release process:
- não sabemos qual regra valia;
- não conseguimos comparar replays;
- não sabemos o que foi testado;
- não sabemos o que está estável;
- não conseguimos voltar atrás com clareza.

---

## Versionamento

O harness deve usar versionamento simples inspirado em SemVer:

```text
MAJOR.MINOR.PATCH-status
```

Exemplos:

```text
0.1.0-alpha
0.2.0-alpha
0.3.0-pilot
1.0.0
1.1.0
1.1.1
```

---

## Significado dos números

### MAJOR

Incrementar quando houver:
- mudança estrutural grande;
- quebra de compatibilidade conceitual;
- redesign da arquitetura;
- mudança profunda na forma de operar.

### MINOR

Incrementar quando houver:
- novo bloco de core;
- novas skills relevantes;
- novo agent;
- novo adapter capability;
- novo template importante;
- melhoria comportamental compatível.

### PATCH

Incrementar quando houver:
- correção;
- ajuste editorial relevante;
- clareza;
- pequena melhoria sem alterar comportamento central.

---

## Status possíveis

### `alpha`

Engenharia em construção, ainda sem piloto completo.

### `pilot`

Engenharia em uso controlado.

### `rc`

Release candidate, candidata a estável.

### stable sem sufixo

Versão considerada estável.

### `deprecated`

Versão ou peça não recomendada para uso novo.

---

## Critérios para release alpha

Pode existir release alpha quando:

- estrutura canônica está materializada;
- documentos fundadores existem;
- comportamento ainda está em formação;
- não há garantia de estabilidade.

---

## Critérios para release pilot

Pode existir release pilot quando:

- core está fechado;
- adapter mínimo existe;
- templates mínimos existem;
- piloto controlado pode rodar;
- artifacts e policies são utilizáveis.

---

## Critérios para release candidate

Pode existir RC quando:

- piloto executado;
- principais falhas corrigidas;
- excesso cortado;
- docs coerentes;
- adapter funcional;
- skills prioritárias validadas;
- governança revisada.

---

## Critérios para stable

Pode virar stable quando:

- comportamento do harness é previsível;
- tasks reais validaram o fluxo;
- review e handoff funcionam;
- não há contradições relevantes;
- o sistema não está burocrático demais;
- versionamento, templates e adapter estão consistentes.

---

## Processo de release

### 1. Congelar escopo

Definir o que entra e o que não entra na release.

### 2. Revisar changelog

Garantir que mudanças relevantes foram registradas.

### 3. Revisar maturidade

Verificar status das peças principais.

### 4. Rodar evals ou replay, quando aplicável

Comparar comportamento com versão anterior.

### 5. Atualizar VERSION

Ajustar o arquivo `VERSION`.

### 6. Criar commit de release

Usar mensagem clara.

Exemplo:

```text
release 0.2.0-alpha
```

### 7. Criar tag, quando apropriado

Exemplo:

```text
v0.2.0-alpha
```

---

## Changelog

O changelog deve registrar:

- novas peças;
- mudanças estruturais;
- mudanças de comportamento;
- depreciações;
- remoções;
- integrações;
- ajustes de adapter;
- decisões relevantes de governança.

Não precisa registrar toda correção de typo.

---

## Release notes

Quando a versão for relevante, release notes devem explicar:

- objetivo da versão;
- principais mudanças;
- impacto prático;
- peças experimentais;
- breaking changes;
- próximos passos.

---

## Relação com replay

Mudança comportamental relevante deve considerar replay.

Exemplos:
- alteração no review protocol;
- nova policy de comandos;
- mudança em artifact schema;
- nova skill de arquitetura;
- alteração no adapter do OpenCode.

---

## Relação com depreciação

Release deve registrar peças deprecated ou removed.

A release não deve esconder remoção de comportamento.

---

## Relação com piloto

Durante piloto, versões podem avançar rapidamente, mas ainda devem preservar changelog e tags importantes.

---

## O que evitar

Evitar:

- mudar VERSION sem changelog;
- criar release sem escopo;
- chamar de stable sem piloto;
- ignorar peças experimentais;
- fazer breaking change silenciosa;
- versionar por vaidade.

---

## Declaração operacional curta

Release é checkpoint de comportamento.  
O harness versiona para saber que engenharia estava governando o agente em cada momento.