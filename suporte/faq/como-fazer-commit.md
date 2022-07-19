---
description: Como atualizar os arquivos do seu Bot hospedado na DisCloud
---

# Como fazer um Commit?

## 👨🔬 Preparando os arquivos

Selecione os arquivos que deseja atualizar em seu diretório, caso eles estejam dentro de alguma pasta, envie a pasta junto dos arquivos para que sejam alocados corretamente em seu diretório. Após preparar os arquivos, selecione-os e zipe (o formato de sua pasta compactada deve ser **`.zip`**).

Caso não saiba como compactar seu arquivos, veja este [guia](https://docs.discloudbot.com/faq/como-compactar-zipar-os-meus-arquivos).

## Commit com Deploy Automático

Através da nossa integração com o **Github** e **Gitlab** você tem a facilidade e rapidez de atualizar suas instancias DisCloud sincronizadas com seu repositório Git.

{% content-ref url="../integracao/github-e-gitlab/" %}
[github-e-gitlab](../integracao/github-e-gitlab/)
{% endcontent-ref %}

## Commit com Deploy Manual

### <img src="../../.gitbook/assets/discloudlogo.png" alt="" data-size="line"> Website

Primeiro você deve fazer **Login** no site da DisCloud, em seguida, clique na sua foto de perfil e selecione **Painel de Controle**.

![](<../../.gitbook/assets/Bx3UKaF - Imgur.gif>)

Depois selecione o bot que deseja atualizar, em seguida, envie o arquivo `.zip` com os arquivos que serão atualizados. Por fim, clique em **Commitar Alterações**.

![](https://i.imgur.com/AknNPZ9.png)

### <img src="../../.gitbook/assets/DiscordLogo1.png" alt="" data-size="line"> Discord

Vá ao canal `🔌┃cmd-discloud` e digite `.commit` (caso você tenha mais de um bot é necessário informar o ID).

![](<../../.gitbook/assets/foc5si4 - Imgur.gif>)

Feito isso, aparecerá um canal de texto com o seu Nickname e Tag (exemplo: `#SeuNick-1234`).

![](https://i.imgur.com/W8f4Iu4.png)

Dentro do canal você deve enviar o arquivo `.zip` para efetuar as alterações. Feito as alterações, você receberá uma notificação no canal `🤖┃bots-logs` de que as alterações foram concluídas.

![](https://i.imgur.com/vKs6z17.png)
