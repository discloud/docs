---
description: >-
  Entenda a raiz do projeto (diretório base) para que a Discloud possa detectar
  configurações, dependências e seu arquivo principal corretamente.
---

# O que é a raiz do projeto?

## 🧾 Visão Geral

A raiz do projeto ("diretório raiz") é a **pasta de nível superior da sua aplicação,** o lugar que você comprime e envia para a Discloud. Ela contém o arquivo de configuração ([`discloud.config`](../../configurations/discloud.config/)), manifesto de dependências (ex. [`package.json`](../../development-environment/supported-languages/javascript/package.json.md), [`requirements.txt`](../../development-environment/supported-languages/python/requirements.txt.md), [`Cargo.toml`](../../development-environment/supported-languages/rust/cargo.toml.md), [`Gemfile`](../../development-environment/supported-languages/ruby/gemfile.md)), opcional [`.env`](.env-file.md), e as pastas com seu código fonte (ex. `src/`).

Se a estrutura estiver errada (por exemplo, você zipa uma pasta que contém outra pasta única que realmente contém os arquivos), a Discloud pode falhar em detectar o arquivo principal ou dependências.

***

## 🖼️ Exemplo Visual

A zona verde representa a **raiz** que você deve comprimir. Amarelo mostra uma pasta aninhada contendo arquivos de código. Tudo dentro do verde é incluído quando você zipa esse diretório.

<figure><img src="../../.gitbook/assets/project-root-structure-example.png" alt=""><figcaption></figcaption></figure>

***

### 🚫 Erros Comuns

| Erro                                            | Resultado                                 | Correção                                                                                           |
| ----------------------------------------------- | ----------------------------------------- | -------------------------------------------------------------------------------------------------- |
| Compactar a pasta principal em vez da raiz real | Configuração / arquivo principal ausente  | Compacte diretamente a pasta que contém [`discloud.config`](../../configurations/discloud.config/) |
| Incluir `node_modules`                          | Upload grande; possíveis erros de tamanho | Remova; deixe a Discloud instalar                                                                  |
| Tokens hardcoded no código                      | Exposição de dados sensíveis              | Use [`.env`](.env-file.md) e variáveis de ambiente                                                 |
| Múltiplos arquivos de entrada ambíguos          | Falha na inicialização                    | Defina `MAIN` em [`discloud.config`](../../configurations/discloud.config/) explicitamente         |
