# Política de Segurança de Comandos

## Finalidade

Esta policy define como o harness deve tratar execução de comandos no ambiente local, no workspace do projeto e em qualquer superfície conectada ao runtime.

Seu papel é impedir que o executor trate shell, terminal e tooling como espaço neutro de ação. Comandos alteram estado, consomem recursos, podem destruir dados, vazar informação, mascarar erro e ampliar blast radius. Por isso, execução de comando é matéria de governança, não simples detalhe de implementação.

---

## Tese central

Todo comando executado pelo sistema deve ser:
- necessário;
- proporcional à task;
- compatível com a classe de risco;
- compatível com a política de autonomia;
- rastreável;
- e seguro o suficiente para o contexto em que roda.

A engenharia rejeita o uso de comando como improviso, tentativa aleatória ou substituto de raciocínio.

---

## Regra operacional principal

Nenhum comando deve ser executado apenas porque “é comum rodar”.

Antes de executar, o sistema deve ser capaz de responder:
1. por que este comando é necessário;
2. que estado ele lê ou altera;
3. qual o risco associado;
4. se existe alternativa mais segura;
5. se o comando está alinhado aos authority commands do projeto.

Se essas respostas não estiverem claras, o comando não está maduro para execução.

---

## Categorias de comando

### 1. Comandos read-only
Comandos que apenas leem estado:
- listagem de diretórios;
- leitura de config;
- inspeção de git;
- consulta de versões;
- grep, find e equivalentes;
- checagens de status;
- leitura de logs localmente;
- consultas de metadata.

Esses comandos tendem a ser os mais permissivos, desde que não exponham informação sensível.

### 2. Comandos de validação
Comandos usados para confirmar qualidade ou coerência:
- build;
- test;
- lint;
- format em modo check;
- validações de contrato;
- dry-runs;
- checagens de segurança;
- profiling e inspeções controladas.

São geralmente permitidos quando alinhados ao workspace e à classe de risco.

### 3. Comandos de mutação local controlada
Comandos que alteram estado de forma reversível e delimitada:
- geração local de arquivos;
- formatação com write;
- restore/install local;
- geração de migration;
- atualização de artifacts locais.

Exigem maior cautela e devem respeitar escopo e autoridade local.

### 4. Comandos destrutivos, sensíveis ou potencialmente irreversíveis
Comandos que podem:
- apagar dados;
- sobrescrever massa de arquivos;
- alterar estado fora do repo;
- tocar produção;
- alterar segredo;
- reconfigurar ambiente;
- rodar com efeitos amplos.

Esses comandos não pertencem à autonomia padrão do executor.

---

## Regra de classificação antes da execução

Todo comando deve ser mentalmente classificado pelo sistema como:

- leitura;
- validação;
- mutação local controlada;
- sensível/destrutivo.

Se o executor não consegue classificar o comando, ele ainda não entendeu o suficiente para rodá-lo com segurança.

---

## Comandos permitidos por padrão

Em condições normais, o executor pode usar com autonomia padrão:

- comandos de inspeção de repo e filesystem;
- comandos de leitura de configuração;
- authority commands de build, test, lint e format, quando documentados;
- comandos locais necessários para discovery e validação proporcional;
- comandos de git estritamente locais e não destrutivos, conforme a git policy.

---

## Comandos que exigem cautela reforçada

Devem ser tratados com maior prudência:

- install/update de dependências;
- geração de migrations;
- comandos que alteram muitos arquivos;
- profiling que consome recursos relevantes;
- varreduras de larga escala;
- scripts locais com efeitos não triviais;
- comandos não documentados como authority commands.

Esses comandos podem ser legítimos, mas exigem justificativa melhor.

---

## Comandos proibidos na autonomia padrão

Sem autorização explícita, o executor não deve rodar:

- comandos destrutivos de filesystem sem delimitador claro;
- remoções em massa;
- alteração direta de produção;
- manipulação de segredo;
- comandos com blast radius externo;
- comandos remotos com efeito write sensível;
- qualquer operação irreversível fora do envelope da task;
- comandos que alterem board, cloud, banco ou integrações externas sem permissão explícita.

---

## Relação com authority commands

Se o projeto possui authority commands documentados, eles devem ser preferidos sobre:
- improviso no shell;
- alias não documentado;
- sequência inventada pelo modelo;
- conhecimento genérico do framework.

Quando não houver authority commands suficientes, o executor deve:
- registrar essa ausência;
- operar com mais cautela;
- evitar sequência inventada onde o risco for relevante.

---

## Relação com classes de risco

### R0
Alta permissividade para comandos de leitura.

### R1
Permissividade moderada para leitura, validação e mutação local pequena.

### R2
Comandos de mutação e validação devem estar claramente ligados ao plan.

### R3
Comandos sensíveis, amplos ou estruturalmente impactantes tendem a exigir escalonamento.

### R4
Ações sensíveis estão fora do fluxo padrão.

---

## Relação com output e evidência

Todo comando relevante precisa gerar consequência observável para o fluxo:
- insight;
- evidência;
- validação;
- artifact;
- ou mudança explicitamente necessária.

Comando que não agrega evidência, progresso ou clarificação é ruído operacional.

---

## Heurísticas de segurança

Antes de rodar um comando, o sistema deve desconfiar quando:

- o comando não é authority command nem é simples leitura;
- o comando altera muito estado sem necessidade clara;
- o comando exige confiança em script opaco;
- o comando toca ambiente externo ou sensível;
- o comando parece “atalho conveniente” demais;
- o comando pode mascarar erro em vez de expor o problema.

---

## Regra de fallback

Quando houver dúvida relevante sobre o efeito de um comando, a postura correta é:
- não executar imediatamente;
- buscar authority source;
- reclassificar o risco;
- escalar, se necessário.

---

## Declaração operacional curta

Comando não é gesto neutro.  
Todo comando muda alguma coisa: estado, confiança, custo ou risco.  
O harness executa comando com intenção explícita, não por reflexo.