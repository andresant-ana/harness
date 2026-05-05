# Checklist — Pre-Merge Review

## Finalidade

Este checklist orienta revisão antes de merge, PR, commit final ou aceite de entrega relevante.

Ele verifica se o diff é causal, seguro, validado, proporcional e livre de slop evidente.

---

## Identificação

```text
Projeto:
Branch:
PR:
Task/Issue:
Reviewer:
Data:
Classe de risco:
```

---

## 1. Estado Git

Executar ou confirmar:

```bash
git status
git diff --stat
git diff --check
```

Verificar:

- [ ] branch correta;
- [ ] diff pertence à task;
- [ ] sem arquivos acidentais;
- [ ] sem line endings massivos;
- [ ] sem segredo;
- [ ] sem arquivos gerados indevidos;
- [ ] commit/PR não mistura escopos.

---

## 2. Aderência ao objetivo

Verificar:

- [ ] objetivo foi atendido;
- [ ] critérios de aceite foram cobertos;
- [ ] fora de escopo foi preservado;
- [ ] não há refactor lateral;
- [ ] mudanças são causais.

Problemas:

```text
<problemas>
```

---

## 3. Qualidade do diff

Verificar:

- [ ] código segue convenção local;
- [ ] não há duplicação óbvia;
- [ ] não há complexidade injustificada;
- [ ] não há dependência nova sem justificativa;
- [ ] não há abstração prematura;
- [ ] não há componente/arquivo inchado sem razão;
- [ ] não há TODO crítico sem follow-up.

---

## 4. Testes e validação

Confirmar:

- [ ] build executado ou lacuna registrada;
- [ ] testes executados ou lacuna registrada;
- [ ] lint/format/typecheck executados quando aplicável;
- [ ] validação funcional feita;
- [ ] validação manual registrada, se aplicável;
- [ ] falhas anteriores ao trabalho foram diferenciadas de falhas novas.

Comandos/resultados:

```text
<comandos e resultados>
```

---

## 5. Segurança

Verificar:

- [ ] sem secrets no diff;
- [ ] input externo validado;
- [ ] auth/authz considerada;
- [ ] dados sensíveis protegidos;
- [ ] logs não vazam informação sensível;
- [ ] dependências novas revisadas;
- [ ] frontend não virou barreira de autorização;
- [ ] cloud/IaC não abriu superfície indevida.

Lacunas:

```text
<lacunas>
```

---

## 6. Banco e dados

Se aplicável, verificar:

- [ ] migration revisada;
- [ ] dados existentes considerados;
- [ ] rollback considerado;
- [ ] locks considerados;
- [ ] query shape revisado;
- [ ] N+1 considerado;
- [ ] índices/constraints justificados;
- [ ] transações não fazem I/O externo.

---

## 7. Produção e operação

Se aplicável, verificar:

- [ ] observabilidade considerada;
- [ ] health/logs/métricas considerados;
- [ ] config por ambiente considerada;
- [ ] rollback/mitigação considerada;
- [ ] deploy não é implícito;
- [ ] pipeline não foi fragilizado;
- [ ] runtime/cloud não mudou sem decisão.

---

## 8. Arquitetura e entropia

Verificar:

- [ ] boundaries respeitados;
- [ ] arquitetura local preservada;
- [ ] ADR criado se decisão relevante;
- [ ] `PROJECT_STATE.md` considerado;
- [ ] documentação atualizada quando necessário;
- [ ] complexidade paga aluguel;
- [ ] sistema ficou mais claro, não mais confuso.

---

## 9. Artifacts

Confirmar presença ou justificativa:

- [ ] Implementation Packet;
- [ ] Execution Plan;
- [ ] Completion Packet;
- [ ] Review Report;
- [ ] Escalation Note, se houve risco;
- [ ] Investigation Note, se houve pesquisa;
- [ ] Project State Entry, se houve mudança durável;
- [ ] ADR, se houve decisão arquitetural.

---

## 10. Handoff

Confirmar que o handoff registra:

- [ ] o que foi feito;
- [ ] onde foi feito;
- [ ] como foi validado;
- [ ] o que não foi validado;
- [ ] riscos remanescentes;
- [ ] próximos passos;
- [ ] sugestão de commit/PR.

---

## 11. Veredito

Escolher:

- [ ] aprovado para merge/commit;
- [ ] aprovado com ressalvas;
- [ ] precisa ajuste;
- [ ] bloquear.

Motivo:

```text
<motivo>
```

Ações obrigatórias:

- `<ação 1>`;
- `<ação 2>`.