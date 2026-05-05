# Checklist — Release Readiness

## Finalidade

Este checklist verifica prontidão mínima para release, publicação, deploy ou entrega relevante.

Ele deve ser usado antes de qualquer release com impacto real ou antes de considerar uma entrega pronta para ambiente compartilhado.

---

## Identificação

```text
Projeto:
Versão/Release:
Ambiente alvo:
Responsável:
Data:
Classe de risco:
```

---

## 1. Escopo da release

Verificar:

- [ ] mudanças incluídas estão claras;
- [ ] issues/PRs associados estão listados;
- [ ] fora de escopo está claro;
- [ ] não há mudança acidental;
- [ ] release não mistura blocos incompatíveis.

Resumo:

```text
<escopo>
```

---

## 2. Estado Git/PR

Verificar:

- [ ] branch correta;
- [ ] PR revisado;
- [ ] commits causais;
- [ ] sem arquivos acidentais;
- [ ] sem conflitos;
- [ ] CI verde ou lacunas aceitas;
- [ ] tag/versionamento definidos, se aplicável.

---

## 3. Build e testes

Confirmar:

- [ ] build executado;
- [ ] testes unitários executados;
- [ ] testes de integração executados ou lacuna aceita;
- [ ] lint/format/typecheck executados;
- [ ] smoke test definido;
- [ ] regressões conhecidas documentadas.

Comandos/resultados:

```text
<comandos e resultados>
```

---

## 4. Segurança

Verificar:

- [ ] sem secrets no diff;
- [ ] dependências revisadas;
- [ ] auth/authz impactadas foram revisadas;
- [ ] dados sensíveis protegidos;
- [ ] logs seguros;
- [ ] pipeline seguro;
- [ ] cloud/IaC revisado, se aplicável;
- [ ] CORS/rede/firewall revisados, se aplicável.

---

## 5. Banco e migrations

Se aplicável:

- [ ] migrations revisadas;
- [ ] SQL gerado revisado;
- [ ] dados existentes considerados;
- [ ] rollback/mitigação definido;
- [ ] backfill definido;
- [ ] locks considerados;
- [ ] execução em produção exige aprovação;
- [ ] compatibilidade app/schema considerada.

---

## 6. Configuração e secrets

Verificar:

- [ ] variáveis obrigatórias existem no ambiente alvo;
- [ ] secrets estão no secret store correto;
- [ ] valores reais não foram expostos;
- [ ] feature flags estão corretas;
- [ ] config não aponta para ambiente errado;
- [ ] fallback perigoso não existe.

---

## 7. Deploy

Verificar:

- [ ] método de deploy está claro;
- [ ] artefato correto está identificado;
- [ ] branch/tag correta será publicada;
- [ ] pipeline tem gates adequados;
- [ ] rollback/mitigação existe;
- [ ] deploy em produção tem autorização explícita;
- [ ] downtime esperado está documentado, se houver.

---

## 8. Observabilidade

Verificar:

- [ ] logs de startup disponíveis;
- [ ] health check disponível;
- [ ] métricas de erro/latência disponíveis;
- [ ] traces/correlation disponíveis quando necessário;
- [ ] alertas relevantes existem;
- [ ] dashboard/runbook existe para fluxo crítico;
- [ ] smoke test pós-deploy definido.

---

## 9. Compatibilidade

Verificar:

- [ ] contratos HTTP compatíveis ou versionados;
- [ ] frontend/backend compatíveis;
- [ ] app antiga/schema novo considerados;
- [ ] app nova/schema antigo considerados;
- [ ] clientes externos considerados;
- [ ] feature flags/rollout considerados.

---

## 10. Documentação e state

Verificar:

- [ ] `PROJECT_STATE.md` atualizado ou não necessário;
- [ ] ADR criado/atualizado, se houve decisão;
- [ ] `OPERATIONAL_REALITY.md` atualizado, se operação mudou;
- [ ] `LOCAL_COMMANDS.md` atualizado, se comando mudou;
- [ ] README/docs atualizados, se comportamento público mudou;
- [ ] release notes preparadas, se aplicável.

---

## 11. Riscos remanescentes

| Risco | Severidade | Aceito por | Mitigação |
|------|------------|------------|-----------|
| `<risco>` | `<baixa/média/alta>` | `<nome/papel>` | `<mitigação>` |

---

## 12. Critério de go/no-go

### Go

Release pode seguir se:

- [ ] validações essenciais passaram;
- [ ] riscos são conhecidos e aceitos;
- [ ] rollback/mitigação existe;
- [ ] observabilidade mínima existe;
- [ ] ambiente/config estão corretos;
- [ ] autorização existe quando necessária.

### No-go

Bloquear release se:

- [ ] segredo exposto;
- [ ] validação essencial ausente;
- [ ] migration destrutiva sem plano;
- [ ] produção sem autorização;
- [ ] rollback inexistente para mudança sensível;
- [ ] observabilidade insuficiente para risco;
- [ ] CI falhando sem explicação;
- [ ] escopo indefinido.

---

## Veredito final

Escolher:

- [ ] Go;
- [ ] Go com ressalvas;
- [ ] No-go;
- [ ] Adiar.

Justificativa:

```text
<justificativa>
```

Ações antes do release:

- `<ação 1>`;
- `<ação 2>`.

Ações pós-release:

- `<ação 1>`;
- `<ação 2>`.