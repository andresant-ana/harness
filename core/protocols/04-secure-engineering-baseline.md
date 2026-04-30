# Baseline de Engenharia Segura

## Finalidade

Este protocolo define o comportamento mínimo de segurança que toda task relevante deve respeitar dentro do harness.

Seu papel é impedir que segurança seja tratada como detalhe tardio, como responsabilidade implícita do framework ou como tema reservado apenas a mudanças explicitamente “de segurança”.

A baseline existe para lembrar que toda mudança de sistema:
- altera superfície de risco;
- altera confiança;
- altera potencial de abuso;
- e pode introduzir vulnerabilidade mesmo quando o objetivo da task parece funcional ou pequeno.

---

## Tese central

Segurança não é uma especialização separada da engenharia.  
Ela é uma dimensão constitutiva da qualidade do sistema.

Por isso, o harness assume que toda task deve ao menos responder:
- o que esta mudança expõe;
- o que esta mudança toca;
- o que esta mudança confia;
- e qual risco novo ela pode introduzir.

---

## Regra operacional principal

Toda task relevante deve passar por uma leitura mínima de segurança, proporcional ao seu risco.

Isso não significa que toda task exigirá:
- análise pesada,
- threat model formal,
- ou revisão especializada.

Mas significa que nenhuma task relevante pode seguir como se segurança fosse automaticamente resolvida pelo contexto, pelo framework ou pela boa intenção da implementação.

---

## Perguntas mínimas de segurança

Antes de aprovar ou executar uma mudança, o sistema deve tentar responder:

1. esta mudança toca entrada de usuário ou dado não confiável?
2. esta mudança toca autenticação, autorização ou sessão?
3. esta mudança toca segredo, configuração sensível ou credencial?
4. esta mudança altera contrato externo, integração ou boundary?
5. esta mudança introduz dependência nova ou altera supply chain?
6. esta mudança toca infraestrutura, pipeline ou execução em cloud?
7. esta mudança aumenta a surface area da aplicação?
8. esta mudança pode vazar dado, ampliar privilégio ou abrir comportamento abusável?

Se alguma dessas respostas for “sim”, a task já saiu da inocência técnica e precisa de atenção explícita.

---

## Dimensões mínimas da baseline

### 1. Input trust
O sistema deve considerar se a mudança lida com:
- entrada externa;
- payload de API;
- query string;
- header;
- body;
- arquivo;
- webhook;
- evento;
- mensagem de fila;
- configuração externa.

Entrada não confiável nunca deve ser tratada como dado já limpo só porque chegou pela aplicação.

### 2. Authn / Authz
Sempre que a mudança tocar identidade, permissão ou sessão, o sistema deve considerar:
- quem pode acessar;
- quem não pode acessar;
- onde a checagem acontece;
- se a regra é realmente aplicada;
- se existe privilégio implícito demais.

### 3. Secrets and config hygiene
Sempre que a mudança tocar:
- segredo;
- credencial;
- token;
- chave;
- variável de ambiente;
- configuração de produção;
- integração com provedor externo,

o sistema deve verificar se:
- o segredo não foi materializado onde não deveria;
- o log não expõe dado sensível;
- a configuração está coerente com o ambiente;
- o valor não foi acidentalmente fixado em código.

### 4. Dependency and supply chain
Toda dependência nova, upgrade sensível ou troca estrutural de biblioteca deve ser lida como alteração de superfície de risco.

A pergunta nunca é só “funciona?”.  
A pergunta também é:
- isso é necessário?
- isso adiciona risco?
- isso amplia o blast radius?
- isso tem custo de atualização e exposição?

### 5. External boundaries
Mudanças em contratos externos exigem atenção porque:
- podem poluir o domínio;
- podem assumir confiança demais;
- podem introduzir parsing inseguro;
- podem tornar o sistema vulnerável a comportamentos não controlados.

### 6. Operational exposure
Toda mudança em:
- infra,
- runtime,
- container,
- pipeline,
- health checks,
- observabilidade,
- execução em cloud

também é mudança de segurança, porque altera superfície operacional e confiança sistêmica.

---

## Relação com classes de risco

### R0
Leitura e síntese podem apenas apontar riscos e ausência de baseline.

### R1
Mudanças pequenas ainda precisam observar:
- entrada,
- segredo,
- authn/authz,
- logs e configs,
quando aplicável.

### R2
A baseline precisa aparecer claramente no plan e no completion packet.

### R3
A leitura de segurança deixa de ser implícita e tende a exigir escalonamento ou revisão mais forte.

### R4
A task já está fora do fluxo padrão e exige tratamento excepcional.

---

## O que o Execution Plan deve registrar

Quando segurança for relevante, o plan deve explicitar:

- superfície tocada;
- hipótese de risco;
- validações de segurança previstas;
- lacunas conhecidas;
- se há necessidade de skill específica;
- se há necessidade de revisão humana especializada.

---

## O que o Completion Packet deve registrar

Quando segurança for relevante, o completion packet deve explicitar:

- o que foi checado;
- o que não foi checado;
- dependências introduzidas ou alteradas;
- risco residual;
- necessidade de follow-up;
- se houve alteração de configuração, segredo, boundary ou exposure.

---

## O que o reviewer deve bloquear

O reviewer deve bloquear ou pedir reavaliação quando perceber:

- input não confiável tratado como seguro por suposição;
- authz fraca ou ausente;
- segredo exposto ou mal tratado;
- log vazando dado sensível;
- dependência introduzida sem rationale;
- surface area ampliada sem justificativa;
- mudança operacional sensível tratada como detalhe irrelevante;
- linguagem confiante escondendo ausência de verificação.

---

## Relação com skills

Esta baseline é o protocolo mínimo.  
Quando a task exigir profundidade maior, o sistema deve acionar skills específicas, como:

- `secure-coding-baseline`
- `authn-authz-review`
- `secrets-and-config-hygiene`
- `dependency-and-supply-chain-review`
- `api-abuse-and-input-validation`
- `iac-security-review`

---

## O que este protocolo não exige

Este protocolo não exige que toda task:
- tenha threat model formal;
- vire exercício de AppSec;
- tenha rigor idêntico independentemente do risco.

A baseline existe para impedir cegueira, não para burocratizar tudo.

---

## Declaração operacional curta

Toda mudança toca confiança em algum grau.  
Segurança mínima não é opcional.  
O que muda de task para task é a profundidade, não a responsabilidade.