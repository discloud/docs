---
description: Lista de todos os comandos do Bot da Discloud no Discord.
icon: list
---

# Comandos do Bot

O Bot da Discloud usa **comandos de barra (slash)**. Digite `/` no canal [**`#🔌・commands`**](https://discord.com/channels/584490943034425391/1051126795883261962) do **Servidor Discord da Discloud** e escolha o comando na lista que o Discord mostra.

{% hint style="info" %}
Para usar os comandos, sua conta precisa estar verificada no servidor. Veja como em [**Bot do Discord**](./).
{% endhint %}

{% hint style="info" %}
Nos comandos que aceitam a opção `app`, informe o **ID da aplicação**, ou `all` para aplicar a todas as suas aplicações. Exemplo: `/reiniciar app:all`.
{% endhint %}

***

## 🚀 Hospedagem

| Comando     | O que faz                                                                                                          |
| ----------- | ------------------------------------------------------------------------------------------------------------------ |
| `/upconfig` | Faz o upload de uma aplicação usando o arquivo [`discloud.config`](../../configurations/discloud.config/).         |
| `/up`       | Faz o upload de uma aplicação com configuração guiada.                                                             |
| `/upsite`   | Faz o upload de um site.                                                                                           |
| `/commit`   | Atualiza os arquivos de uma aplicação. Veja [**Como fazer commit?**](../../faq/general-questions/how-to-commit.md) |

### 📤 Durante o upload

| Comando     | O que faz                                                     |
| ----------- | ------------------------------------------------------------- |
| `/cancelar` | Cancela o upload em andamento. Use dentro do canal de upload. |
| `/fechar`   | Fecha o canal de upload.                                      |

***

## ⚙️ Gerenciar aplicações

| Comando              | O que faz                                                                                              |
| -------------------- | ------------------------------------------------------------------------------------------------------ |
| `/apps`              | Lista as aplicações que você tem hospedadas.                                                           |
| `/status (ID)`       | Mostra o status de uma aplicação.                                                                      |
| `/logs`              | Mostra os logs da sua aplicação.                                                                       |
| `/iniciar app:all`   | Inicia sua aplicação.                                                                                  |
| `/parar app:all`     | Para sua aplicação.                                                                                    |
| `/reiniciar app:all` | Reinicia sua aplicação.                                                                                |
| `/memoria`           | Altera a memória RAM máxima que uma aplicação pode usar.                                               |
| `/autorestart`       | Ativa ou desativa o reinício automático da aplicação.                                                  |
| `/version`           | Altera a [versão da linguagem](../../configurations/discloud.config/versions.md) usada pela aplicação. |
| `/apt`               | Instala [pacotes](../../configurations/discloud.config/apt.md) na instância Linux da sua aplicação.    |
| `/backup`            | Faz um backup dos arquivos da sua aplicação.                                                           |
| `/restorepoints`     | Cria pontos de restauração para uma aplicação.                                                         |
| `/removerapp (ID)`   | Exclui a aplicação, apagando todos os dados e configurações.                                           |

{% hint style="danger" %}
**`/removerapp` é permanente.** Faça um `/backup` antes se quiser guardar os arquivos.
{% endhint %}

***

## 🌐 Domínios e subdomínios

| Comando       | O que faz                                                                                                 |
| ------------- | --------------------------------------------------------------------------------------------------------- |
| `/subdominio` | Registra ou remove um [subdomínio](../../faq/general-questions/how-to-create-a-subdomain.md) na Discloud. |
| `/dominio`    | Gerencia seu [domínio personalizado](../../api-and-integrations/custom-domain.md).                        |

{% hint style="info" %}
Recomendamos gerenciar domínios e subdomínios pelo [**site da Discloud**](https://discloud.com/dashboard), que tem uma integração melhor do que os comandos do bot.
{% endhint %}

***

## 👥 Equipe

| Comando | O que faz                                    |
| ------- | -------------------------------------------- |
| `/mod`  | Gerencia os moderadores das suas aplicações. |

***

## 👤 Conta

| Comando              | O que faz                                                                                                       |
| -------------------- | --------------------------------------------------------------------------------------------------------------- |
| `/api`               | Gera o [token para usar a API da Discloud](../../faq/general-questions/how-can-i-get-my-discloud-api-token.md). |
| `/userinfo [userid]` | Mostra as informações de um cliente.                                                                            |
| `/planos`            | Mostra todos os planos disponíveis e seus benefícios.                                                           |
| `/locale`            | Altera o idioma em que o Bot da Discloud responde.                                                              |
| `/cleardm`           | Apaga todas as mensagens que o bot enviou na sua DM.                                                            |

***

## 🧰 Outros

| Comando | O que faz                                   |
| ------- | ------------------------------------------- |
| `/help` | Mostra a mensagem de ajuda com os comandos. |
| `/ping` | Mostra a latência.                          |

***

## ❓ Ainda precisa de ajuda?

Use `/help` no Discord ou junte-se ao nosso [**Servidor Discord**](https://discord.discloudbot.com/) para suporte.
