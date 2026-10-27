---
description: >-
  Altere a versão da linguagem da sua aplicação sempre que necessário, das
  versões mais antigas às mais recentes.
icon: code-fork
---

# Versões

## ⚙️ **Configurando a Versão da Sua Aplicação**

Ao fazer o upload da sua aplicação no **Discloud**, você pode precisar especificar a **versão da linguagem** correta para seu projeto. Você pode fazer isso definindo o parâmetro `VERSION=` dentro do seu arquivo [`discloud.config`](./).

**📌 Como Definir a Versão**

Para definir a versão desejada, adicione a seguinte linha ao seu arquivo de configuração:

<pre class="language-properties" data-title="discloud.config"><code class="lang-properties"><a data-footnote-ref href="#user-content-fn-1"># ...</a>
VERSION=current
# ...
</code></pre>

Substitua `"current"` pela sua versão preferida da lista abaixo.

{% hint style="info" %}
Se você não tiver certeza de qual versão escolher, usar `latest` sempre selecionará a versão mais recente estável **LTS (Long-Term Support)**, que é recomendada para a maioria das aplicações.
{% endhint %}

***

## 📑 **Versões Disponíveis**

<details>

<summary>🟨 JavaScript (Node.js)</summary>

<table><thead><tr><th width="177">Versões Disponíveis</th><th>Informações Adicionais</th></tr></thead><tbody><tr><td><code>latest</code></td><td>Versão mais recente <strong>estável</strong> do <strong>Node.js (LTS)</strong> <mark style="color:green;">(<strong>recomendada</strong>)</mark>.</td></tr><tr><td><code>current</code></td><td>Versão mais recente <strong>disponível</strong> do <strong>Node.js</strong>.</td></tr><tr><td><code>20</code></td><td>Node.js 20.x</td></tr><tr><td><code>18</code></td><td>Node.js 18.x</td></tr><tr><td><code>16.13.2</code></td><td>Node.js 16.13.2</td></tr><tr><td><code>18.x.x</code></td><td>Versão estável alternativa do Node.js 18</td></tr><tr><td><code>14.18.3</code></td><td>Node.js 14.18.3 (descontinuado)</td></tr><tr><td><code>legacy</code></td><td>Versão legada mais antiga do Node.js.</td></tr><tr><td><code>suja</code></td><td>Versão mais pesada do <code>latest</code> com <a href="apt.md"><strong>pacotes APT</strong></a> <strong>pré-instalados</strong>. Recomendado apenas como <strong>último recurso</strong>.</td></tr></tbody></table>

</details>

<details>

<summary>🐍 Python</summary>

<table><thead><tr><th width="178">Versões Disponíveis</th><th>Informações Adicionais</th></tr></thead><tbody><tr><td>latest</td><td>Versão mais recente <strong>estável</strong> do <strong>Python (LTS)</strong> <mark style="color:green;">(<strong>recomendada</strong>)</mark>.</td></tr><tr><td>3.11</td><td>Python 3.11</td></tr><tr><td>3.10</td><td>Python 3.10</td></tr><tr><td>3.9</td><td>Python 3.9</td></tr><tr><td>3.9.10</td><td>Python 3.9.10</td></tr><tr><td>2.7</td><td>Python 2.7 (descontinuado)</td></tr><tr><td>legacy</td><td>Versão legada mais antiga do Python.</td></tr><tr><td><code>suja</code></td><td>Versão mais pesada do <code>latest</code> com <a href="apt.md"><strong>pacotes APT</strong></a> <strong>pré-instalados</strong>. Recomendado apenas como <strong>último recurso</strong>.</td></tr></tbody></table>

</details>

<details>

<summary>☕ Java</summary>

<table><thead><tr><th width="180">Versões Disponíveis</th><th>Informações Adicionais</th></tr></thead><tbody><tr><td><code>latest</code></td><td>Versão estável mais recente do <strong>OpenJDK</strong>.</td></tr><tr><td><code>18.x.x</code></td><td>OpenJDK 18</td></tr><tr><td><code>17.x.x</code></td><td>OpenJDK 17</td></tr><tr><td><code>16.x.x</code></td><td>OpenJDK 16</td></tr></tbody></table>

</details>

<details>

<summary>💎 Ruby</summary>

<table><thead><tr><th width="179">Versões Disponíveis</th><th>Informações Adicionais</th></tr></thead><tbody><tr><td><code>latest</code></td><td>Versão estável mais recente do <strong>Ruby</strong> (<strong>recomendada</strong>).</td></tr><tr><td><code>3.1.0</code></td><td>Ruby 3.1.0</td></tr><tr><td><code>2.7.5</code></td><td>Ruby 2.7.5</td></tr></tbody></table>

</details>

<details>

<summary>🐹 Go</summary>

<table><thead><tr><th width="179">Versões Disponíveis</th><th>Informações Adicionais</th></tr></thead><tbody><tr><td><code>latest</code></td><td>Versão estável mais recente do <strong>Go</strong> (<strong>recomendada</strong>).</td></tr><tr><td><code>1.16.13</code></td><td>Go 1.16.13</td></tr><tr><td><code>1.7.6</code></td><td>Go 1.7.6</td></tr></tbody></table>

</details>

<details>

<summary>🐘 PHP</summary>

<table><thead><tr><th width="180">Versões Disponíveis</th><th>Informações Adicionais</th></tr></thead><tbody><tr><td><code>latest</code></td><td>Versão estável mais recente do <strong>PHP</strong> (<strong>recomendada</strong>).</td></tr></tbody></table>

</details>

<details>

<summary>🦀 Rust</summary>

<table><thead><tr><th width="187">Versões Disponíveis</th><th>Informações Adicionais</th></tr></thead><tbody><tr><td><code>latest</code></td><td>Versão estável mais recente do <strong>Rust</strong> (<strong>recomendada</strong>).</td></tr><tr><td><code>suja</code></td><td>Versão mais pesada do <code>latest</code> com <strong>pacotes APT pré-instalados</strong>. Recomendado apenas como <strong>último recurso</strong>.</td></tr></tbody></table>

</details>

[^1]: **Nota:** Os **`...`** indicam apenas a continuação de outras opções anteriores ou subsequentes que não são relevantes para mencionar nesta página.
