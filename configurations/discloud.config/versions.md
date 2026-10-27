---
description: >-
  Change your application's language version whenever necessary, from older
  releases to the latest.
icon: code-fork
---

# Versions

## ⚙️ **Setting Up Your Application Version**

When deploying your application on **Discloud**, you may need to specify the correct **language version** for your project. You can do this by setting the `VERSION=` parameter inside your [`discloud.config`](./) file.

**📌 How to Set the Version**

To set the desired version, add the following line to your configuration file:

<pre class="language-properties" data-title="discloud.config"><code class="lang-properties"><a data-footnote-ref href="#user-content-fn-1"># ...</a>
VERSION=current
# ...
</code></pre>

Replace `"current"` with your preferred version from the list below.

{% hint style="info" %}
If you're unsure which version to choose, using `latest` will always select the latest stable **LTS (Long-Term Support) version**, which is recommended for most applications.
{% endhint %}

***

## 📑 **Available Versions**

<details>

<summary>🟨 JavaScript (Node.js)</summary>

<table><thead><tr><th width="177">Available Versions</th><th>Additional Information</th></tr></thead><tbody><tr><td><code>latest</code></td><td>Latest <strong>stable</strong> version of <strong>Node.js (LTS)</strong> <mark style="color:green;">(<strong>recommended</strong>)</mark>.</td></tr><tr><td><code>current</code></td><td>Latest <strong>available</strong> version of <strong>Node.js</strong>.</td></tr><tr><td><code>20</code></td><td>Node.js 20.x</td></tr><tr><td><code>18</code></td><td>Node.js 18.x</td></tr><tr><td><code>16.13.2</code></td><td>Node.js 16.13.2</td></tr><tr><td><code>18.x.x</code></td><td>Alternative stable release of Node.js 18</td></tr><tr><td><code>14.18.3</code></td><td>Node.js 14.18.3 (deprecated)</td></tr><tr><td><code>legacy</code></td><td>Older legacy version of Node.js.</td></tr><tr><td><code>suja</code></td><td>Heavier version of <code>latest</code> with <strong>pre-installed</strong> <a href="apt.md"><strong>APT packages</strong></a>. Recommended only as a <strong>last resort</strong>.</td></tr></tbody></table>

</details>

<details>

<summary>🐍 Python</summary>

<table><thead><tr><th width="178">Available Versions</th><th>Additional Information</th></tr></thead><tbody><tr><td>latest</td><td>Latest <strong>stable</strong> version of <strong>Python (LTS)</strong> <mark style="color:green;">(<strong>recommended</strong>)</mark>.</td></tr><tr><td>3.11</td><td>Python 3.11</td></tr><tr><td>3.10</td><td>Python 3.10</td></tr><tr><td>3.9</td><td>Python 3.9</td></tr><tr><td>3.9.10</td><td>Python 3.9.10</td></tr><tr><td>2.7</td><td>Python 2.7 (deprecated)</td></tr><tr><td>legacy</td><td>Older legacy version of Python.</td></tr><tr><td><code>suja</code></td><td>Heavier version of <code>latest</code> with <strong>pre-installed</strong> <a href="apt.md"><strong>APT packages</strong></a>. Recommended only as a <strong>last resort</strong>.</td></tr></tbody></table>

</details>

<details>

<summary>☕ Java</summary>

<table><thead><tr><th width="180">Available Versions</th><th>Additional Information</th></tr></thead><tbody><tr><td><code>latest</code></td><td>Latest stable version of <strong>OpenJDK</strong>.</td></tr><tr><td><code>18.x.x</code></td><td>OpenJDK 18</td></tr><tr><td><code>17.x.x</code></td><td>OpenJDK 17</td></tr><tr><td><code>16.x.x</code></td><td>OpenJDK 16</td></tr></tbody></table>

</details>

<details>

<summary>💎 Ruby</summary>

<table><thead><tr><th width="179">Available Versions</th><th>Additional Information</th></tr></thead><tbody><tr><td><code>latest</code></td><td>Latest stable version of <strong>Ruby</strong> (<strong>recommended</strong>).</td></tr><tr><td><code>3.1.0</code></td><td>Ruby 3.1.0</td></tr><tr><td><code>2.7.5</code></td><td>Ruby 2.7.5</td></tr></tbody></table>

</details>

<details>

<summary>🐹 Go</summary>

<table><thead><tr><th width="179">Available Versions</th><th>Additional Information</th></tr></thead><tbody><tr><td><code>latest</code></td><td>Latest stable version of <strong>Go</strong> (<strong>recommended</strong>).</td></tr><tr><td><code>1.16.13</code></td><td>Go 1.16.13</td></tr><tr><td><code>1.7.6</code></td><td>Go 1.7.6</td></tr></tbody></table>

</details>

<details>

<summary>🐘 PHP</summary>

<table><thead><tr><th width="180">Available Versions</th><th>Additional Information</th></tr></thead><tbody><tr><td><code>latest</code></td><td>Latest stable version of <strong>PHP</strong> (<strong>recommended</strong>).</td></tr></tbody></table>

</details>

<details>

<summary>🦀 Rust</summary>

<table><thead><tr><th width="187">Available Versions</th><th>Additional Information</th></tr></thead><tbody><tr><td><code>latest</code></td><td>Latest stable version of <strong>Rust</strong> (<strong>recommended</strong>).</td></tr><tr><td><code>suja</code></td><td>Heavier version of <code>latest</code> with <strong>pre-installed APT packages</strong>. Recommended only as a <strong>last resort</strong>.</td></tr></tbody></table>

</details>

[^1]: **Note:** The **`...`** only indicate the continuation of other previous or subsequent options that are not relevant to mention on this page.
