# Table of contents

## Introdução <a href="#introduction" id="introduction"></a>

* [Bem-vindo à Discloud](README.md)

## Primeiros Passos <a href="#getting-started" id="getting-started"></a>

* [Bots](getting-started/bots.md)
* [Websites e APIs](getting-started/websites-and-apis.md)
* [Frameworks](getting-started/frameworks/README.md)
  * [Next.js](getting-started/frameworks/nextjs.md)
  * [NestJS](getting-started/frameworks/nestjs.md)
* [VPS](getting-started/vps.md)
* [Lavalink](getting-started/lavalink.md)
* [Migrar de Outra Hospedagem](getting-started/migrating-from-another-host.md)

## Formas de Deploy <a href="#deployment-methods" id="deployment-methods"></a>

* [Painel de Controle](deployment-methods/dashboard.md)
* [Bot do Discord](deployment-methods/discord-bot/README.md)
  * [Comandos do Bot](deployment-methods/discord-bot/commands.md)
* [Visual Studio Code](deployment-methods/visual-studio-code.md)
* [CLI](deployment-methods/cli.md)
* [Integração com GitHub](deployment-methods/github-integration.md)

## Recursos da Plataforma <a href="#platform-features" id="platform-features"></a>

* [Projetos](platform-features/projects.md)
* [Equipes e Permissões](platform-features/teams-and-permissions.md)
* [Variáveis de Ambiente](platform-features/environment-variables.md)
* [Backups](platform-features/backups.md)
* [Snapshots](platform-features/snapshots.md)
* [Bancos de Dados](platform-features/databases.md)
* [Edge](platform-features/edge.md)
* [Domínio Personalizado](platform-features/custom-domain.md)

## Configurações <a href="#configurations" id="configurations"></a>

* [discloud.config](configurations/discloud.config/README.md)
  * [APT](configurations/discloud.config/apt.md)
  * [Versões](configurations/discloud.config/versions.md)
  * [VLAN](configurations/discloud.config/vlan.md)
* [.discloudignore](configurations/.discloudignore.md)
* [Puppeteer](configurations/puppeteer.md)

## Ambiente de Desenvolvimento <a href="#development-environment" id="development-environment"></a>

* [Linguagens Suportadas](development-environment/supported-languages/README.md)
  * [JavaScript](development-environment/supported-languages/javascript/README.md)
    * [TypeScript](development-environment/supported-languages/javascript/typescript.md)
    * [package.json](development-environment/supported-languages/javascript/package.json.md)
  * [Python](development-environment/supported-languages/python/README.md)
    * [requirements.txt](development-environment/supported-languages/python/requirements.txt.md)
  * [Java](development-environment/supported-languages/java.md)
  * [Ruby](development-environment/supported-languages/ruby/README.md)
    * [Gemfile](development-environment/supported-languages/ruby/gemfile.md)
  * [Rust](development-environment/supported-languages/rust/README.md)
    * [Cargo.toml](development-environment/supported-languages/rust/cargo.toml.md)
  * [Go](development-environment/supported-languages/go/README.md)
    * [go.mod](development-environment/supported-languages/go/go.mod.md)
  * [PHP](development-environment/supported-languages/php/README.md)
    * [composer.json](development-environment/supported-languages/php/composer.json.md)
* [Ambiente Local](development-environment/local-environment/README.md)
  * [Node.js](development-environment/local-environment/nodejs.md)
  * [Python](development-environment/local-environment/python.md)
  * [Ruby](development-environment/local-environment/ruby.md)
  * [Rust](development-environment/local-environment/rust.md)
  * [Go](development-environment/local-environment/golang.md)
  * [Java](development-environment/local-environment/java.md)
  * [PHP](development-environment/local-environment/php.md)

## API e SDKs <a href="#api-and-sdks" id="api-and-sdks"></a>

* [Visão Geral da API](api-and-sdks/api-overview/README.md)
  * [Autenticação](api-and-sdks/api-overview/authentication.md)
  * [Usuário](api-and-sdks/api-overview/user.md)
  * [Aplicações](api-and-sdks/api-overview/applications.md)
  * [Aplicações da Equipe](api-and-sdks/api-overview/team-apps.md)
  * [Variável de Ambiente](api-and-sdks/api-overview/environment-variable.md)
  * [Snapshot](api-and-sdks/api-overview/snapshot.md)
  * [Subdomínio](api-and-sdks/api-overview/subdomain.md)
  * [Domínio Personalizado](api-and-sdks/api-overview/custom-domain.md)
  * [Banco de Dados](api-and-sdks/api-overview/database.md)
  * [Projeto](api-and-sdks/api-overview/project.md)
  * [Equipe](api-and-sdks/api-overview/team.md)
* [Biblioteca NPM](api-and-sdks/npm-library/README.md)
  * [Introdução](api-and-sdks/npm-library/getting-started.md)
  * [Exemplos de Uso](api-and-sdks/npm-library/usage-examples.md)
* [\[EM ANDAMENTO\] Biblioteca Python](api-and-sdks/python-library/README.md)
  * [\[EM ANDAMENTO\] Introdução](api-and-sdks/python-library/getting-started.md)
  * [\[EM ANDAMENTO\] Exemplos de Uso](api-and-sdks/python-library/usage-examples.md)

## FAQ

* [Onde Obter Ajuda](faq/where-to-get-help.md)
* [Perguntas Gerais](faq/general-questions/README.md)
  * [O que é a raiz do projeto?](faq/general-questions/what-is-the-root-of-the-project.md)
  * [Arquivo .env](faq/general-questions/.env-file.md)
  * [Qual é o arquivo principal?](faq/general-questions/what-is-the-main-file.md)
  * [Como funciona a RAM?](faq/general-questions/how-does-ram-work.md)
  * [Como criar um subdomínio?](faq/general-questions/how-to-create-a-subdomain.md)
  * [Como posso obter o ID do meu bot do Discord?](faq/general-questions/how-can-i-get-my-discord-bot-id.md)
  * [Como comprimir?](faq/general-questions/how-to-compress.md)
  * [Como fazer commit?](faq/general-questions/how-to-commit.md)
  * [Como acessar os logs da aplicação?](faq/general-questions/how-to-access-the-application-logs.md)
  * [Como verificar uma conta do Discord?](faq/general-questions/how-to-verify-a-discord-account.md)
  * [Como construir e empacotar uma aplicação Java?](faq/general-questions/how-to-build-and-package-a-java-application.md)
  * [Gerenciamento de Assinaturas](faq/general-questions/subscription-management.md)
  * [Como obter o meu token da API da Discloud?](faq/general-questions/how-can-i-get-my-discloud-api-token.md)
  * [Como obter o ID da minha conta Discloud?](faq/general-questions/how-can-i-get-my-discloud-account-id.md)
  * [Como proteger meus tokens?](faq/general-questions/how-to-protect-my-tokens.md)
  * [Como fazer sharding do meu bot?](faq/general-questions/how-to-shard-my-bot.md)
* [Soluções de Problemas](faq/troubleshooting-solutions/README.md)
  * [Diagnosticando Aplicações Offline](faq/troubleshooting-solutions/diagnosing-offline-applications.md)
  * [Por que meu bot não responde?](faq/troubleshooting-solutions/bot-not-responding.md)
  * [Bot Muito Pesado](faq/troubleshooting-solutions/bot-too-heavy.md)
  * [Por que as dependências não instalam?](faq/troubleshooting-solutions/dependencies-not-installing.md)
  * [Por que não consigo acessar meu site?](faq/troubleshooting-solutions/why-cant-i-access-my-website.md)

## Sobre <a href="#about" id="about"></a>

* [Doações](about/donations.md)

***

* [Marca Discloud](https://discloud.com/brand)
* [Servidor do Discord](https://discord.discloudbot.com/)
* [Termos de Serviço (ToS)](https://discloud.com/legal)
* [Política de Uso Aceitável (AUP)](https://discloud.com/legal)
