# Checklist — Operational Reality

## Finalidade

Este checklist verifica se uma mudança, projeto ou release considera a realidade operacional do sistema.

Ele impede que uma solução seja considerada pronta apenas porque funciona em localhost.

---

## Identificação

```text
Projeto:
Task/Release:
Responsável:
Data:
Ambiente:
```

---

## 1. Ambientes

Verificar:

- [ ] local está descrito;
- [ ] dev/staging/prod estão descritos, se existirem;
- [ ] diferenças entre ambientes são conhecidas;
- [ ] produção não foi assumida sem confirmação;
- [ ] configuração por ambiente está clara.

Lacunas:

```text
<lacunas>
```

---

## 2. Runtime

Verificar:

- [ ] modelo de execução está claro;
- [ ] processo principal está claro;
- [ ] jobs/workers estão identificados;
- [ ] container/serverless/runtime cloud foi considerado;
- [ ] statefulness foi avaliada;
- [ ] autoscaling não está mascarando problema de código.

---

## 3. Configuração e secrets

Verificar:

- [ ] variáveis obrigatórias estão documentadas;
- [ ] valores reais não aparecem em docs/diff/logs;
- [ ] secrets vêm de local seguro;
- [ ] defaults perigosos foram evitados;
- [ ] config local não aponta para produção por acidente;
- [ ] rotação/segurança foi considerada quando aplicável.

---

## 4. Banco e dados

Verificar:

- [ ] banco local/remoto está claro;
- [ ] migrations têm comando definido;
- [ ] dados reais foram diferenciados de dados locais;
- [ ] backup/restore é conhecido quando relevante;
- [ ] mudança de schema tem rollback/mitigação;
- [ ] seed/backfill não é destrutivo sem decisão.

---

## 5. Deploy

Verificar:

- [ ] método de deploy está claro;
- [ ] pipeline ou processo manual está documentado;
- [ ] branch/tag/artefato correto é identificado;
- [ ] rollback ou mitigação existe;
- [ ] deploy em produção exige autorização;
- [ ] deploy não é tratado como detalhe final.

---

## 6. Observabilidade

Verificar:

- [ ] logs existem;
- [ ] erros relevantes são visíveis;
- [ ] métricas mínimas existem;
- [ ] health check existe quando aplicável;
- [ ] tracing/correlation existe quando necessário;
- [ ] alerts existem quando há produção;
- [ ] startup failure é diagnosticável.

Pergunta crítica:

```text
Como saberemos que isso está funcionando ou falhando?
```

---

## 7. Falhas esperadas

Considerar:

- [ ] banco indisponível;
- [ ] API externa fora;
- [ ] timeout;
- [ ] retry storm;
- [ ] fila travada;
- [ ] job falhando;
- [ ] config ausente;
- [ ] secret inválido;
- [ ] deploy parcial;
- [ ] rollback necessário.

Mitigações:

```text
<mitigações>
```

---

## 8. Segurança operacional

Verificar:

- [ ] produção não foi tocada sem autorização;
- [ ] IAM/RBAC não foi ampliado sem revisão;
- [ ] firewall/rede pública não mudou sem decisão;
- [ ] logs não expõem dados sensíveis;
- [ ] pipeline não expõe secrets;
- [ ] recurso cloud público é intencional;
- [ ] CORS é restrito quando aplicável.

---

## 9. Runbook mínimo

Para mudanças relevantes, confirmar se existe orientação para:

- [ ] startup falhando;
- [ ] erro 5xx;
- [ ] banco indisponível;
- [ ] deploy falhando;
- [ ] fila/job travado;
- [ ] rollback;
- [ ] segredo/config inválido.

---

## 10. Veredito operacional

Escolher:

- [ ] operável;
- [ ] operável com ressalvas;
- [ ] não operável;
- [ ] precisa investigação.

Ressalvas:

```text
<ressalvas>
```

Próximas ações:

- `<ação 1>`;
- `<ação 2>`.