# Política de Segredos e Produção

## Finalidade

Esta policy define como o harness deve tratar segredos, credenciais, ambientes de produção, operações sensíveis e qualquer ação com potencial de dano real fora do ambiente local controlado.

Seu papel é impedir que o executor trate produção, segredo ou configuração sensível como uma extensão comum do fluxo de desenvolvimento.

---

## Tese central

Produção e segredos não pertencem à autonomia padrão do executor.

Qualquer ação que toque ambiente real, credencial, chave, token, dado sensível, configuração crítica ou efeito irreversível deve ser tratada como superfície de alto risco.

A engenharia assume que:
- erro em código local é reversível;
- erro com segredo pode vazar confiança;
- erro em produção pode gerar dano real;
- erro em configuração crítica pode comprometer operação e segurança.

---

## Regra operacional principal

Sem autorização explícita, o executor não deve:

- acessar segredo;
- imprimir segredo;
- alterar segredo;
- criar segredo;
- remover segredo;
- modificar produção;
- executar comando com efeito real em produção;
- alterar configuração sensível;
- executar operação destrutiva em ambiente externo.

O caminho padrão é leitura local, ambiente de desenvolvimento e validação controlada.

---

## O que conta como segredo

São considerados segredos:

- API keys;
- tokens;
- passwords;
- connection strings;
- private keys;
- certificates;
- OAuth secrets;
- service principal secrets;
- cloud credentials;
- database credentials;
- signing keys;
- webhook secrets;
- qualquer valor que permita acesso, impersonação ou mutação sensível.

---

## O que conta como produção

Produção inclui:

- ambiente usado por usuários reais;
- banco de dados real;
- storage real;
- fila real;
- cloud resource real;
- pipeline de deploy real;
- observabilidade com dados reais;
- sistemas integrados com impacto externo;
- qualquer ambiente cujo erro possa afetar operação, cliente, custo ou reputação.

Ambientes de staging também podem ser sensíveis dependendo do contexto.

---

## Ações proibidas na autonomia padrão

O executor não deve, sem autorização explícita:

- rodar migration em produção;
- alterar variável de ambiente sensível;
- rotacionar chave;
- apagar recurso cloud;
- alterar firewall, IAM, role ou policy;
- executar script contra banco real;
- limpar fila real;
- alterar DNS;
- disparar deploy;
- publicar release;
- modificar secret store;
- fazer push que acione deploy automático não autorizado.

---

## Leitura de segredos

Mesmo leitura de segredo é sensível.

O executor deve evitar:

- solicitar valor de segredo;
- imprimir segredo em terminal;
- copiar segredo para artifact;
- registrar segredo em log;
- incluir segredo em prompt;
- persistir segredo em arquivo.

Quando a existência de um segredo precisar ser confirmada, a preferência deve ser por verificar metadata, nome, presença ou configuração sem revelar o valor.

---

## Logs e outputs

O sistema deve tratar logs e outputs com cautela.

Logs podem conter:

- tokens;
- headers;
- payloads sensíveis;
- dados pessoais;
- connection strings;
- stack traces com informação interna;
- URLs com parâmetros secretos.

O executor deve evitar colar logs extensos ou sensíveis em artifacts sem filtragem.

---

## Arquivos proibidos ou sensíveis

O executor deve ter cautela reforçada com:

- `.env`;
- `.env.*`;
- arquivos de credenciais cloud;
- arquivos de certificado;
- dumps de banco;
- backups;
- arquivos de configuração de produção;
- secrets locais;
- service account files;
- arquivos gerados por tooling de autenticação.

Esses arquivos não devem ser abertos, alterados ou reproduzidos sem necessidade clara e autorização apropriada.

---

## Relação com Git

Segredos nunca devem ser commitados.

O harness deve bloquear ou escalar quando houver:

- segredo em diff;
- segredo em arquivo staged;
- credential material em documentação;
- valor sensível em exemplo real;
- configuração de produção acidentalmente versionada.

Se segredo for detectado no histórico, isso deixa de ser simples correção local e passa a ser incidente potencial.

---

## Relação com produção

Produção exige tratamento excepcional.

Antes de qualquer ação que possa afetar produção, deve haver:

1. autorização explícita do humano;
2. objetivo claro;
3. comando ou ação exata;
4. entendimento do risco;
5. plano de rollback ou mitigação;
6. evidência de que o ambiente alvo está correto;
7. confirmação de que não há alternativa read-only ou local.

Sem isso, a ação não deve ocorrer.

---

## Relação com classes de risco

### R0
Leitura local sem exposição de segredo pode ser permitida. Leitura de metadata sensível exige cautela.

### R1
Mudanças locais sem segredo e sem produção podem seguir com autonomia moderada.

### R2
Mudanças que tocam configuração sensível exigem plano e evidência explícita.

### R3
Mudanças próximas a produção, credenciais, auth ou infraestrutura exigem escalonamento.

### R4
Produção, segredos e irreversibilidade ficam fora da autonomia padrão.

---

## Uso de valores fictícios

Quando for necessário documentar exemplos, usar valores claramente fictícios:

- `YOUR_API_KEY_HERE`
- `<connection-string>`
- `<secret-value>`
- `example-token`
- `localhost`
- valores sem formato realista de credencial válida.

Exemplo não deve parecer segredo real.

---

## Relação com MCP e integrações externas

MCP ou qualquer integração externa não deve ser usado para mutar produção ou segredo sem política específica, trusted integration e autorização explícita.

O padrão é:

- read-only first;
- menor privilégio;
- sem escrita sensível;
- sem automação de produção por conveniência.

---

## O que o executor deve fazer ao encontrar segredo

Se o executor encontrar possível segredo em arquivo, diff, log ou output:

1. parar reprodução do valor;
2. não copiar para artifact;
3. registrar a existência sem revelar o conteúdo;
4. classificar risco;
5. sugerir revisão humana;
6. escalar se houver chance de exposição real.

---

## O que o reviewer deve bloquear

O reviewer deve bloquear:

- segredo em código;
- segredo em documentação;
- segredo em log;
- produção tratada como local;
- deploy implícito;
- mutation externa sem autorização;
- alteração de config sensível sem plano;
- operação irreversível sem rollback.

---

## Declaração operacional curta

Segredo não é dado comum.  
Produção não é ambiente comum.  
O harness trata ambos como superfícies de risco elevado e fora da autonomia padrão.