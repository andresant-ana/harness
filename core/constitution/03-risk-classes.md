# Classes de Risco

As classes de risco existem para calibrar autonomia, nível de evidência, intensidade de review, necessidade de escalonamento e proporcionalidade do esforço operacional.

Risco não é rótulo decorativo.  
Risco muda comportamento do sistema.

---

## Visão geral

| Classe | Natureza geral | Autonomia padrão | Exigência mínima |
|--------|----------------|------------------|------------------|
| R0 | Leitura, inspeção, pesquisa e síntese sem mutação | Alta | Rastreabilidade simples |
| R1 | Mudança local de baixo impacto e alta reversibilidade | Moderada | Plano simples + validação local |
| R2 | Mudança funcional relevante com impacto moderado | Controlada | Execution Plan completo + validação mais forte |
| R3 | Mudança estrutural, sensível ou de impacto sistêmico relevante | Baixa | Escalonamento antes de mutar |
| R4 | Produção, segredos, irreversibilidade, alto risco operacional ou de segurança | Muito baixa | Fora da autonomia padrão |

---

## R0 — Leitura e inspeção

### Exemplos
- leitura de código;
- inspeção de diretórios;
- discovery de repositório;
- consulta a documentação;
- consulta read-only via MCP;
- síntese de contexto;
- diagnóstico sem mutação.

### Regra operacional
Pode operar com alta autonomia, desde que:
- não haja mutação;
- a saída seja factual;
- não haja extrapolação arquitetural indevida.

### Evidência esperada
- achados;
- arquivos relevantes;
- authority sources;
- hipóteses;
- dúvidas abertas.

---

## R1 — Mudança local de baixo risco

### Exemplos
- ajuste pequeno e reversível;
- correção pontual em arquivo ou poucos arquivos;
- melhoria documental local;
- refino localizado sem impacto sistêmico relevante;
- ajuste de baixo acoplamento.

### Regra operacional
Pode seguir com autonomia moderada, desde que:
- o escopo esteja claro;
- a reversibilidade seja alta;
- a mudança não altere arquitetura ou risco operacional relevante.

### Evidência esperada
- plano simples;
- validação local;
- explicitação do que foi ou não testado;
- review proporcional.

---

## R2 — Mudança funcional relevante

### Exemplos
- nova feature moderada;
- alteração em vários arquivos com lógica relevante;
- mudança em contrato interno importante;
- refatoração com risco funcional moderado;
- alteração de persistência ou integração sem chegar a risco estrutural alto.

### Regra operacional
Exige controle maior.  
Não pode começar sem Execution Plan completo.

### Evidência esperada
- discovery adequado;
- Execution Plan;
- validação proporcional;
- Completion Packet robusto;
- review conservador;
- explicitação de riscos remanescentes.

---

## R3 — Mudança estrutural ou sensível

### Exemplos
- alteração arquitetural relevante;
- mudança de topologia entre módulos;
- integração externa importante;
- migration significativa;
- mudança com impacto em cloud execution model;
- mudança com risco operacional considerável;
- introdução de mecanismo assíncrono relevante;
- mudança com possível blast radius alto.

### Regra operacional
Não deve ser tratada como execução autônoma padrão.  
Exige escalonamento antes da mutação relevante.

### Evidência esperada
- hipótese arquitetural clara;
- trade-off explícito;
- escalation ou validação estratégica;
- plano mais rigoroso;
- registro forte de riscos e impactos.

---

## R4 — Alto risco, produção ou irreversibilidade

### Exemplos
- alteração direta em produção;
- manipulação de segredos;
- escrita via integração externa sensível;
- operações destrutivas;
- mudanças altamente irreversíveis;
- ações com potencial grande de dano operacional, de segurança ou reputacional.

### Regra operacional
Fora da autonomia padrão do harness.

Esses casos exigem:
- autorização explícita;
- tratamento excepcional;
- revisão humana forte;
-, quando aplicável, especialização adicional.

---

## Como escolher a classe correta

A classe de risco deve ser decidida observando:

- escopo da mudança;
- reversibilidade;
- impacto potencial;
- proximidade com produção;
- impacto em segurança;
- impacto em topologia e arquitetura;
- dependência de contexto externo;
- necessidade de decisão humana.

Quando houver dúvida entre duas classes, a regra é:
**assumir a classe mais conservadora** até que haja clareza suficiente para rebaixamento.

---

## Relação entre risco e autonomia

### Quanto maior o risco:
- menor a autonomia do executor;
- maior a exigência de plano;
- maior a exigência de review;
- maior a exigência de evidência;
- maior a probabilidade de escalonamento;
- maior a necessidade de explicitar o que ficou aberto.

---

## Relação entre risco e artifacts

- **R0** pode terminar com investigation note ou síntese factual.
- **R1** normalmente exige saída simples, mas já pode produzir completion packet curto.
- **R2** exige implementation packet + execution plan + completion packet.
- **R3** frequentemente exige escalation note antes de implementation relevante.
- **R4** exige autorização explícita e tratamento fora do fluxo padrão.

---

## Regra de disciplina

A classe de risco não existe para travar o trabalho.  
Ela existe para impedir que o sistema trate como trivial aquilo que pode produzir dano, slop ou decisão irreversível sem maturidade suficiente.