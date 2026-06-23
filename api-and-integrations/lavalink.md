---
description: Guia passo a passo para hospedar um servidor de áudio Lavalink na Discloud.
icon: music
tags:
  - novo
---

# Lavalink

### 🎵 O que é o Lavalink?

O **Lavalink** é um servidor de streaming de áudio independente usado por bots de música do Discord para reproduzir áudio de fontes como YouTube, SoundCloud, Bandcamp, Twitch e muito mais. Em vez de processar o áudio diretamente no bot, o Lavalink delega todo o processamento de áudio pesado para um servidor dedicado.

O Lavalink é executado como uma **aplicação Java** e expõe uma API WebSocket à qual seu bot se conecta.

***

### ✅ Requisitos

{% hint style="success" %}
[**Plano Platinum ou Superior**](https://discloud.com/plans) – Necessário para todas as aplicações `TYPE=site`.
{% endhint %}

{% hint style="success" %}
[**Subdomínio**](../faq/general-questions/how-to-create-a-subdomain.md) – Você deve registrar um subdomínio único na Discloud.
{% endhint %}

{% hint style="danger" %}
**Porta 8080 & Host 0.0.0.0** – Sua aplicação **deve** ouvir na porta `8080` e host `0.0.0.0` para ser acessível externamente.
{% endhint %}

{% hint style="info" %}
**RAM** – Um mínimo de **512MB** é recomendado para aplicações web.
{% endhint %}

***

### 🚀 Configuração Passo a Passo

{% stepper %}
{% step %}
**⬇️ Baixe o `Lavalink.jar`**

Baixe a versão estável mais recente do Lavalink no repositório oficial do GitHub:

👉 [https://github.com/lavalink-devs/Lavalink/releases](https://github.com/lavalink-devs/Lavalink/releases)

Baixe o arquivo chamado `Lavalink.jar` na seção Assets do release mais recente.

{% hint style="info" %}
O Lavalink 4.x é a versão estável atual e é recomendado. Ele requer Java 17 ou superior.
{% endhint %}
{% endstep %}

{% step %}
**📝 Crie o `application.yml`**

Crie um arquivo chamado `application.yml` na mesma pasta que o `Lavalink.jar`. Este é o arquivo de configuração principal do Lavalink.

{% code title="application.yml" expandable="true" %}
```yaml
server:
  port: 8080
  address: 0.0.0.0

lavalink:
  server:
    password: "youshallnotpass"
    sources:
      youtube: false
      bandcamp: true
      soundcloud: true
      twitch: true
      vimeo: true
      http: true
      local: false

  plugins:
    # Substitua VERSION pela versao atual, conforme mostrado na guia Releases, ou por um hash de commit longo para snapshots.
    - dependency: "dev.lavalink.youtube:youtube-plugin:VERSION"
      snapshot: false

plugins:
  youtube:
    enabled: true
    allowSearch: true
    allowDirectVideoIds: true
    allowDirectPlaylistIds: true
    oauth:
      enabled: true

logging:
  level:
    root: INFO
    lavalink: INFO
```
{% endcode %}

{% hint style="danger" %}
**Defina `server.port` como `8080`** - Isso é necessário para que a Discloud roteie o tráfego externo corretamente.

**Defina `server.address` como `0.0.0.0`** - Isso permite que conexões externas alcancem o Lavalink.
{% endhint %}

{% hint style="warning" %}
**Altere a senha** - Substitua `"youshallnotpass"` por uma senha forte e única. Qualquer pessoa que souber sua senha pode usar seu servidor Lavalink.
{% endhint %}

{% hint style="info" %}
**Plugin do YouTube** - A configuração `youtube: false` em `sources` desabilita a fonte YouTube nativa (descontinuada). O `youtube-plugin` listado em `plugins` a substitui por uma implementação mais atualizada. Verifique a [página de releases do plugin](https://github.com/lavalink-devs/youtube-source/releases) para obter o número da versão mais recente.
{% endhint %}
{% endstep %}

{% step %}
**⚙️ Crie o `discloud.config`**

Crie um arquivo [`discloud.config`](../configurations/discloud.config/) na mesma pasta:

```ini
NAME=MeuLavalink
TYPE=site
MAIN=Lavalink.jar
RAM=512
VERSION=17.x.x
ID=meu-subdomain-lavalink
```

* **`TYPE=site`** - Obrigatório porque o Lavalink escuta em uma porta de rede.
* **`MAIN=Lavalink.jar`** - Deve corresponder exatamente ao nome do arquivo JAR.
* **`VERSION=17.x.x`** - O Lavalink 4.x requer Java 17. Use `17.x.x` ou `latest`.
* **`ID`** - Seu subdomínio registrado (sem `.discloud.app`).
{% endstep %}

{% step %}
**📦 Crie o arquivo ZIP**

Sua pasta deve conter exatamente estes três arquivos:

```
lavalink-upload/
├─ Lavalink.jar
├─ application.yml
└─ discloud.config
```

Compacte esses arquivos em um arquivo `.zip`. Certifique-se de que os arquivos estão [**na raiz**](../faq/general-questions/what-is-the-root-of-the-project.md) do ZIP, não compacte uma pasta.
{% endstep %}

{% step %}
**🚀 Envie para a Discloud**

{% content-ref url="https://app.gitbook.com/s/vUqkKIFudeQ2TQOirm35/how-to-host" %}
[Como Hospedar](https://app.gitbook.com/s/vUqkKIFudeQ2TQOirm35/how-to-host)
{% endcontent-ref %}
{% endstep %}

{% step %}
**🤖 Configure seu bot**

Conecte seu bot do Discord ao Lavalink usando seu subdomínio. Como a Discloud usa HTTPS/WSS com proxy reverso, você deve conectar na **porta 443 com `secure: true`**.

```json
{
  "host": "meu-subdomain-lavalink.discloud.app",
  "port": 443,
  "secure": true,
  "password": "youshallnotpass"
}
```

Substitua `meu-subdomain-lavalink` pelo seu subdomínio real e `youshallnotpass` pela senha que você definiu no `application.yml`.

{% hint style="warning" %}
**Não** conecte na porta `8080` a partir do seu bot. A porta `8080` é apenas para uso interno pela Discloud. Seu bot deve sempre conectar na porta `443` com `secure: true`.
{% endhint %}
{% endstep %}
{% endstepper %}

***

### 🔗 Conectando uma conta do YouTube (OAuth2)

Por padrão, o Lavalink pode exibir uma solicitação de login nos logs pedindo para você autorizar uma conta do YouTube. Isso é necessário para evitar limitações e erros de reprodução do YouTube.

{% hint style="info" %}
Se você habilitou `oauth.enabled: true` no seu `application.yml`, o Lavalink irá automaticamente gerar uma URL de autorização de dispositivo na primeira inicialização.
{% endhint %}

{% stepper %}
{% step %}
**📋 Inicie o Lavalink e verifique os logs**

Após enviar e iniciar sua instância do Lavalink, verifique os logs da aplicação. Procure por uma mensagem semelhante a:

```
Please navigate to https://www.youtube.com/device?user_code=XXXX-XXXX and grant access.
```
{% endstep %}

{% step %}
**🔑 Autorize a conta do YouTube**

Abra a URL dos logs no seu navegador (ex.: `https://www.youtube.com/device?user_code=XXXX-XXXX`).

Faça login com a conta Google / YouTube que você deseja que o Lavalink use. Uma conta pessoal funciona bem, uma conta dedicada é recomendada.

{% hint style="warning" %}
Você deve concluir esta etapa **antes que o código expire** (geralmente em poucos minutos). Se expirar, reinicie o Lavalink para gerar um novo código.
{% endhint %}
{% endstep %}

{% step %}
**✅ Confirme a autorização**

Após conceder acesso, retorne aos logs do seu Lavalink. Você deverá ver uma mensagem confirmando que a autorização foi bem-sucedida:

```
YouTube token refreshed successfully.
```

O Lavalink salvará o token e o reutilizará automaticamente em futuras reinicializações. Você não precisa repetir este processo a menos que revogue o acesso ou altere a conta.
{% endstep %}
{% endstepper %}
