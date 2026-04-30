# Política de Introdução de Dependências

## Finalidade

Esta policy define como o harness deve tratar a introdução, atualização ou substituição de dependências em projetos.

Seu papel é impedir que o executor adicione bibliotecas, frameworks, SDKs, packages, tools ou serviços por conveniência imediata, sem avaliar custo, risco, manutenção e real necessidade.

---

## Tese central

Dependência é complexidade importada.

Toda dependência adiciona:
- código externo;
- risco de segurança;
- custo de atualização;
- superfície de manutenção;
- possíveis conflitos;
- peso cognitivo;
- e acoplamento técnico.

Por isso, dependência nova precisa pagar aluguel.

---

## Regra operacional principal

Nenhuma dependência deve ser adicionada sem responder:

1. qual problema ela resolve;
2. por que o projeto não resolve isso de forma simples sem ela;
3. que alternativa nativa ou local foi considerada;
4. que risco de supply chain ela introduz;
5. que custo de manutenção ela traz;
6. se ela é coerente com a stack e arquitetura local;
7. se ela será usada de forma suficiente para justificar sua presença.

---

## Tipos de dependência

### 1. Biblioteca de runtime
Entra no produto em execução.

Exige maior cautela porque afeta:
- segurança;
- performance;
- deploy;
- compatibilidade;
- comportamento em produção.

### 2. Dependência de desenvolvimento
Usada em build, test, lint, generation ou tooling.

Também exige cautela, especialmente quando roda scripts ou altera pipeline.

### 3. SDK ou client externo
Aumenta acoplamento com fornecedor, API ou plataforma.

Deve ser avaliado quanto a:
- estabilidade;
- lock-in;
- versionamento;
- tratamento de erro;
- observabilidade;
- segurança.

### 4. Framework
Altera modelo mental e arquitetura.

Só deve entrar com justificativa forte.

### 5. Serviço externo
Não é só dependência de código. É dependência operacional.

Exige análise de custo, disponibilidade, segurança, dados e lock-in.

---

## Critérios para aceitar dependência

Uma dependência pode ser aceita quando:

- resolve dor real;
- evita implementação local arriscada;
- é madura e mantida;
- tem uso claro;
- tem licença aceitável;
- tem baixo risco de supply chain;
- é coerente com a stack;
- reduz complexidade líquida;
- possui alternativa de saída ou isolamento razoável.

---

## Critérios para rejeitar dependência

Rejeitar ou reavaliar quando:

- é usada para tarefa trivial;
- substitui poucas linhas simples;
- entra por conveniência do agente;
- possui manutenção duvidosa;
- tem histórico de vulnerabilidades preocupante;
- exige permissão ampla;
- adiciona acoplamento excessivo;
- duplica capacidade já existente no projeto;
- aumenta bundle, runtime, cold start ou superfície operacional sem necessidade.

---

## Preferência por recursos nativos

Antes de adicionar dependência, considerar:

- biblioteca padrão;
- recurso do framework já usado;
- utilitário local simples;
- capacidade existente no projeto;
- command/tooling já presente.

Isso não significa reinventar tudo.  
Significa evitar importar complexidade para resolver problema pequeno.

---

## Dependência e arquitetura por dor real

Dependência nova deve seguir a mesma lógica de arquitetura por dor real.

Perguntas:
- essa dependência resolve dor atual?
- ou antecipa necessidade imaginária?
- o custo é menor do que a alternativa local?
- ela torna o sistema mais claro ou mais opaco?

---

## Dependência e segurança

Toda dependência nova deve ser lida como alteração de surface area.

Considerar:
- origem;
- manutenção;
- licença;
- vulnerabilidades conhecidas;
- scripts de instalação;
- permissões;
- popularidade não como garantia, mas como sinal auxiliar;
- impacto em supply chain.

---

## Dependência e contexto de agente

Dependências também afetam agentes.

Cada dependência nova pode:
- aumentar documentação necessária;
- criar APIs novas para o agente entender;
- introduzir padrões diferentes;
- ampliar chance de uso incorreto;
- exigir skills ou instructions adicionais.

---

## Atualização de dependência

Atualização de dependência deve considerar:

- breaking changes;
- changelog;
- impacto em runtime;
- impacto em build/test;
- impacto em segurança;
- compatibilidade com lockfile;
- validação proporcional.

Atualizar “só porque existe versão nova” não é política aceitável.

---

## Remoção de dependência

Remover dependência é positivo quando:

- ela não é mais usada;
- foi substituída por recurso nativo;
- adiciona risco desnecessário;
- reduz bundle, superfície ou manutenção;
- simplifica arquitetura.

Mas remoção também exige validação para evitar regressão oculta.

---

## O que o Execution Plan deve registrar

Ao introduzir dependência, o plan deve explicitar:

- nome da dependência;
- finalidade;
- alternativa considerada;
- razão de escolha;
- risco;
- validação prevista;
- impacto em arquitetura, segurança e operação.

---

## O que o Completion Packet deve registrar

Ao finalizar task com dependência nova ou atualizada, registrar:

- dependência adicionada/alterada;
- por que foi necessária;
- como foi validada;
- risco residual;
- follow-up de segurança ou manutenção.

---

## O que o reviewer deve bloquear

O reviewer deve bloquear quando:

- dependência entra sem justificativa;
- problema seria simples sem ela;
- há duplicação de capacidade existente;
- risco de supply chain foi ignorado;
- o agente adicionou por tentativa e erro;
- não há validação suficiente.

---

## Declaração operacional curta

Dependência é complexidade importada.  
O harness só aceita dependência quando ela reduz complexidade líquida ou risco real de forma justificável.