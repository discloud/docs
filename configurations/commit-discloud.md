---
icon: code-commit
---

# Commit Discloud

## Como realizar commits corretamente na Discloud para criar, editar e substituir arquivos

Ao realizar commits na Discloud, é fundamental entender como funciona o processo de envio de arquivos e como o sistema identifica os arquivos que devem ser criados ou substituídos.

O ponto mais importante é compreender que **a Discloud utiliza os caminhos e os nomes dos arquivos enviados para determinar onde cada arquivo será criado ou atualizado.** Portanto, se você deseja substituir um arquivo existente, precisa garantir que o arquivo enviado corresponda exatamente ao caminho do arquivo original.

Um pequeno erro no caminho, no nome de uma pasta ou até mesmo na utilização de letras maiúsculas e minúsculas pode fazer com que um novo arquivo seja criado em outro local, em vez de substituir o arquivo original.

A seguir, vamos explicar como esse processo funciona e quais cuidados devem ser tomados para evitar problemas.

### 1. Entenda como funciona o commit na Discloud

Quando você envia um commit pela Discloud, o sistema recebe os arquivos enviados e utiliza seus caminhos para determinar onde eles devem ser criados ou atualizados no projeto.

Existem duas situações principais:

* **Criar um arquivo:** quando o caminho informado ainda não contém um arquivo com aquele nome, o sistema poderá criar um novo arquivo nesse local.
* **Substituir um arquivo existente:** quando o caminho e o nome correspondem exatamente aos de um arquivo existente, o sistema poderá atualizar o arquivo original com o novo conteúdo.

Isso significa que, para substituir um arquivo, não basta enviar outro arquivo com o mesmo nome. É necessário reproduzir corretamente toda a estrutura de diretórios até chegar ao arquivo desejado.

> **A Discloud não deve ser tratada como um sistema que procura automaticamente um arquivo pelo nome e descobre onde você pretendia substituí-lo. Você precisa informar o caminho correto.**

### 2. Todo caminho deve ser reproduzido a partir da raiz do projeto

Considere que a estrutura do seu bot seja a seguinte:

```
meu-bot/
├── package.json
├── index.js
└── src/
    └── comandos/
        └── ping.js
```

Nesse exemplo, o arquivo `ping.js` está dentro da pasta `comandos`, que está dentro da pasta `src`.

Portanto, o caminho completo relativo à raiz do projeto é:

```
src/comandos/ping.js
```

Agora, imagine que você queira modificar esse arquivo e enviar a alteração por meio de um commit na Discloud.

Você não deve colocar apenas o arquivo `ping.js` na raiz do ZIP. Também não deve ignorar a pasta `comandos` ou alterar a organização dos diretórios.

O ZIP precisa reproduzir a estrutura original:

```
arquivo.zip
└── src/
    └── comandos/
        └── ping.js
```

Observe que o arquivo continua dentro de `comandos`, e essa pasta continua dentro de `src`.

Esse detalhe é fundamental porque **a Discloud considera os caminhos enviados a partir da raiz do projeto para localizar os arquivos que serão criados ou atualizados.**

Se o arquivo original estiver dentro de uma pasta ou de várias subpastas, você deverá reproduzir todos esses níveis no ZIP, respeitando a estrutura existente.

### 3. Os nomes das pastas e dos arquivos precisam ser idênticos

Esse é um dos pontos mais importantes de todo o processo.

Quando falamos em nomes idênticos, estamos falando de uma reprodução exata, incluindo:

* Letras maiúsculas e minúsculas.
* Nome completo de cada pasta.
* Nome completo do arquivo.
* Extensão do arquivo, como `.js`, `.ts`, `.json` ou `.py`.
* Caracteres especiais e demais caracteres presentes nos nomes.
* Todos os níveis da estrutura de diretórios.

Imagine que a estrutura original do seu bot seja:

```
src/
└── comandos/
    └── ping.js
```

A pasta original se chama `comandos`, com todas as letras minúsculas.

Agora, imagine que você prepare o ZIP com esta estrutura:

```
src/
└── Comandos/
    └── ping.js
```

Observe a diferença: você colocou a letra `C` maiúscula no nome da pasta `Comandos`.

Embora os nomes pareçam iguais visualmente, eles não são iguais para o sistema de arquivos Linux utilizado pela Discloud.

O resultado poderá ser uma estrutura semelhante a esta:

```
projeto/
└── src/
    ├── comandos/
    │   └── ping.js
    └── Comandos/
        └── ping.js
```

Em vez de substituir o arquivo original, você poderá acabar criando uma segunda pasta dentro de `src`, contendo outro arquivo chamado `ping.js`.

Isso acontece porque, no Linux, `comandos` e `Comandos` são caminhos diferentes.

**Portanto, não basta reproduzir os nomes de forma parecida. É necessário reproduzi-los exatamente como existem no projeto original.**

### 4. Por que as letras maiúsculas e minúsculas fazem tanta diferença?

A Discloud utiliza infraestrutura baseada em Linux, e o sistema de arquivos Linux normalmente diferencia letras maiúsculas de minúsculas.

Isso significa que os seguintes caminhos podem representar diretórios diferentes:

```
src/comandos/ping.js
src/Comandos/ping.js
src/COMANDOS/ping.js
```

O mesmo vale para nomes de arquivos:

```
config.json
Config.json
CONFIG.json
```

Para uma pessoa, pode parecer que esses nomes representam o mesmo arquivo. Para o sistema operacional, entretanto, eles são diferentes.

Considere também o seguinte exemplo de código:

```
const ping = require("./src/comandos/ping.js");
```

Essa importação procura o arquivo no caminho `src/comandos/ping.js`.

Se você enviar o arquivo para `src/Comandos/ping.js`, a importação continuará apontando para o caminho original. O Node.js não vai procurar automaticamente em outras pastas por um arquivo com o mesmo nome.

Consequentemente, o bot poderá continuar utilizando o arquivo antigo ou apresentar um erro de módulo não encontrado, dependendo da estrutura resultante.

Por isso, respeitar os nomes originais não é apenas uma questão de organização: é uma condição importante para que as alterações funcionem corretamente.

### 5. O que acontece quando você informa o caminho errado?

Vamos imaginar que você queira substituir este arquivo:

```
src/comandos/ping.js
```

Entretanto, ao preparar o ZIP, você acaba criando:

```
src/Comandos/ping.js
```

O conteúdo do arquivo pode estar completamente correto. O código pode ter sido revisado, as alterações podem estar prontas e não haver nenhum erro de sintaxe.

Mesmo assim, o resultado poderá ser incorreto porque o arquivo foi enviado para o caminho errado.

Em vez de atualizar:

```
src/comandos/ping.js
```

o sistema poderá criar:

```
src/Comandos/ping.js
```

Assim, você terá dois arquivos com o mesmo nome, mas em diretórios diferentes.

Isso pode gerar diversos problemas:

* O bot continua executando a versão antiga do arquivo.
* As alterações enviadas não produzem o efeito esperado.
* O projeto passa a ter diretórios duplicados.
* O código pode apresentar erros de importação.
* A estrutura do projeto fica inconsistente.
* A identificação e a correção de problemas futuros tornam-se mais difíceis.

O mais perigoso é que você pode acreditar que atualizou o arquivo corretamente, quando, na realidade, apenas criou uma segunda versão em outro caminho.

É por isso que a atenção aos caminhos deve fazer parte de todo o processo de criação de commits na Discloud.

### 6. A raiz do ZIP também precisa estar correta

Além de respeitar os nomes e os caminhos internos, você precisa verificar como os arquivos estão organizados dentro do ZIP.

Imagine que você queira atualizar:

```
src/comandos/ping.js
```

A estrutura esperada para o envio é:

```
arquivo.zip
└── src/
    └── comandos/
        └── ping.js
```

Entretanto, você pode acabar compactando a pasta inteira do projeto e produzindo esta estrutura:

```
arquivo.zip
└── meu-bot/
    └── src/
        └── comandos/
            └── ping.js
```

Se a Discloud processar o ZIP preservando essa pasta externa, o caminho resultante poderá ser:

```
projeto/
├── src/
│   └── comandos/
│       └── ping.js
└── meu-bot/
    └── src/
        └── comandos/
            └── ping.js
```

Nesse caso, você poderá ter criado uma estrutura adicional, em vez de atualizar o arquivo original.

O resultado exato depende de como o mecanismo de commit da Discloud processa o ZIP. Por isso, é importante verificar se ele espera os arquivos diretamente na raiz do pacote ou se aplica alguma regra específica de extração.

A regra prática é: **a estrutura interna do ZIP precisa corresponder ao caminho relativo esperado pelo commit, considerando a forma como a Discloud processa os arquivos enviados.**

### 7. Procedimento correto antes de enviar um commit

Para evitar erros, siga estas etapas sempre que precisar criar ou substituir arquivos na Discloud.

**Passo 1 — Localize o arquivo original.**

Encontre o arquivo que deseja modificar e identifique exatamente em qual diretório ele está.

**Passo 2 — Identifique o caminho completo.**

Se o arquivo estiver em `src/comandos/ping.js`, esse é o caminho que deverá servir de referência.

**Passo 3 — Reproduza toda a estrutura.**

Crie as pastas `src` e `comandos` dentro do ZIP, respeitando a hierarquia original.

**Passo 4 — Confira os nomes.**

Verifique se cada pasta e cada arquivo possuem exatamente os mesmos nomes do projeto original, incluindo a capitalização.

**Passo 5 — Confira a extensão.**

Se o arquivo original se chama `ping.js`, não o envie como `Ping.js`, `ping.JS` ou `ping.js.txt`.

**Passo 6 — Verifique a raiz do ZIP.**

Certifique-se de que você não incluiu uma pasta externa desnecessária que altere o caminho esperado do arquivo.

**Passo 7 — Revise o conteúdo.**

Confirme que o arquivo enviado contém as alterações desejadas e não está incompleto.

**Passo 8 — Confira o resultado do commit.**

Sempre que possível, verifique as alterações registradas e a estrutura resultante do projeto. Se a intenção era substituir um arquivo, mas o resultado indica a criação de uma pasta duplicada, investigue o problema antes de continuar.

### 8. Exemplo completo de um commit correto

Imagine que seu bot possua a seguinte estrutura:

```
meu-bot/
├── index.js
├── package.json
└── src/
    ├── comandos/
    │   ├── ping.js
    │   └── help.js
    └── eventos/
        └── ready.js
```

Você deseja alterar apenas o arquivo `ping.js`.

Nesse caso, se o mecanismo de commit da Discloud aceitar o envio parcial de arquivos, seu ZIP poderá conter somente:

```
atualizacao.zip
└── src/
    └── comandos/
        └── ping.js
```

Não é necessário incluir os demais arquivos se eles não precisarem ser alterados.

O caminho de destino esperado é:

```
src/comandos/ping.js
```

Depois de aplicar corretamente a alteração, a estrutura do projeto deverá permanecer organizada da mesma forma, com a diferença de que o conteúdo de `ping.js` terá sido atualizado.

Os arquivos `index.js`, `package.json`, `help.js` e `ready.js` deverão permanecer intactos.

Agora, se você enviar o arquivo em `src/Comandos/ping.js`, poderá criar uma pasta duplicada. Se incluir uma pasta externa `meu-bot` sem que o mecanismo de commit espere essa estrutura, também poderá acabar criando um caminho incorreto.

O objetivo é modificar exatamente o arquivo desejado, sem criar cópias desnecessárias e sem alterar a estrutura do restante do projeto.

### 9. Regras que devem ser seguidas em todos os commits

Para manter a organização do projeto e evitar problemas durante as atualizações, siga estas regras:

1. **Respeite o caminho completo:** reproduza todos os diretórios entre a raiz do projeto e o arquivo que deseja modificar.
2. **Não altere a capitalização:** `comandos` e `Comandos` são nomes diferentes no Linux.
3. **Não altere os nomes sem necessidade:** mantenha os nomes originais das pastas e dos arquivos.
4. **Não envie somente o nome do arquivo quando ele estiver em uma subpasta:** reproduza o caminho necessário.
5. **Não crie níveis adicionais desnecessários:** verifique se o ZIP não contém uma pasta externa que altere o caminho de destino.
6. **Evite enviar arquivos desnecessários:** mantenha o commit focado nas alterações pretendidas.
7. **Confira o resultado:** verifique se o arquivo original foi atualizado e se nenhuma pasta duplicada foi criada.
8. **Não presuma que a Discloud corrigirá os caminhos:** envie a estrutura correta desde o início.

### 10. A regra fundamental: precisão no caminho

O princípio mais importante é entender que a Discloud não deve ser utilizada como se fosse um sistema capaz de descobrir automaticamente qual arquivo você deseja substituir apenas pelo nome dele.

Se o arquivo original está em:

```
src/comandos/ping.js
```

esse é o caminho que precisa ser reproduzido no commit.

Se você enviar:

```
src/Comandos/ping.js
```

estará informando outro caminho.

Se enviar:

```
meu-bot/src/comandos/ping.js
```

poderá adicionar um nível desnecessário à estrutura.

E, se enviar apenas:

```
ping.js
```

poderá criar ou atualizar um arquivo na raiz, em vez de modificar aquele que realmente desejava alterar.

Por isso, antes de enviar qualquer commit na Discloud, confira sempre três pontos fundamentais:

* **O caminho completo do arquivo.**
* **A grafia exata de cada pasta.**
* **O nome e a extensão exatos do arquivo.**

Esses cuidados são essenciais para que as alterações sejam aplicadas no local correto, evitando arquivos duplicados, diretórios inconsistentes e problemas durante a execução do bot.

O objetivo não é simplesmente enviar um commit com sucesso. É garantir que o commit produza o resultado esperado, preservando a estrutura do projeto e modificando exatamente os arquivos que precisam ser alterados.

> **Na Discloud, a precisão dos caminhos é fundamental para manter a consistência do projeto. Antes de enviar um commit, confira a estrutura, valide os nomes e tenha certeza de que cada arquivo está no lugar correto.**
