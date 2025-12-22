---
description: Guia completo para hospedar aplicações Go na Discloud.
icon: golang
---

# Go

## 📁 **Preparando os Arquivos**

Antes de fazer upload do seu projeto, você deve **excluir arquivos desnecessários** para otimizar o deploy.

#### ❌ **Arquivos a Excluir**

Certifique-se de que os seguintes arquivos e diretórios **não** sejam incluídos no seu [`.zip`](../../../faq/general-questions/em-andamento-como-comprimir.md):

```diff
- bin/
- *.exe
- .git/
```

📌 **Use um arquivo** [**`.discloudignore`**](../../../configurations/.discloudignore.md) **para excluir automaticamente esses arquivos. Não** exclua `go.mod` ou `go.sum`.

🔗 **Precisa de ajuda para configurar seu** [**`go.mod`**](go.mod.md) **ou encontrar o** [**arquivo principal**](../../../faq/general-questions/what-is-the-main-file.md)**?**

***

### 🌐 **Hospedando Websites & APIs em Go**

Antes de fazer deploy do seu website ou API na Discloud, certifique-se de que você atenda aos seguintes **requisitos**:

{% hint style="success" %}
[Plano Platinum ou superior](https://discloud.com/plans) é necessário para hospedar websites ou APIs.
{% endhint %}

{% hint style="success" %}
[Um subdomínio deve ser criado](../../../faq/general-questions/how-to-create-a-subdomain.md) antes do deploy.
{% endhint %}

{% hint style="danger" %}
Porta `8080` é obrigatória – As aplicações devem escutar nesta porta.
{% endhint %}

{% tabs %}
{% tab title="🤖 Bot Discord" %}
```go
package main

import (
  "log"
  "os"
  "os/signal"
  "syscall"
  "github.com/bwmarrin/discordgo"
)

func main() {
  token := os.Getenv("DISCORD_TOKEN")
  if token == "" { log.Fatal("DISCORD_TOKEN não definido") }

  dg, err := discordgo.New("Bot " + token)
  if err != nil { log.Fatal(err) }

  dg.AddHandler(func(s *discordgo.Session, r *discordgo.Ready) {
    log.Println("Bot está pronto")
  })

  if err := dg.Open(); err != nil { log.Fatal(err) }
  log.Println("Bot executando. Pressione CTRL+C para sair.")

  stop := make(chan os.Signal, 1)
  signal.Notify(stop, os.Interrupt, syscall.SIGTERM)
  <-stop
  dg.Close()
}
```

> Bots não precisam bindar nenhuma porta HTTP. Eles só precisam manter o processo vivo.
{% endtab %}

{% tab title="⚙️ Servidor HTTP Básico" %}
```go
package main

import (
  "fmt"
  "log"
  "net/http"
)

func main() {
  mux := http.NewServeMux()
  mux.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "Olá do Go na Discloud!")
  })

  log.Println("Iniciando servidor em :8080")
  if err := http.ListenAndServe(":8080", mux); err != nil {
    log.Fatal(err)
  }
}
```
{% endtab %}

{% tab title="🔀 API REST (chi)" %}
```go
package main

import (
  "net/http"
  "log"
  "github.com/go-chi/chi/v5"
)

func main() {
  r := chi.NewRouter()
  r.Get("/health", func(w http.ResponseWriter, r *http.Request) { w.Write([]byte("ok")) })
  r.Get("/hello/{name}", func(w http.ResponseWriter, r *http.Request) {
    name := chi.URLParam(r, "name")
    w.Write([]byte("Olá, "+name))
  })
  log.Println("API em :8080")
  log.Fatal(http.ListenAndServe(":8080", r))
}
```
{% endtab %}
{% endtabs %}

***

## ✍️ Fazendo Deploy **da Sua Aplicação**

Uma vez que seu projeto esteja **configurado e comprimido**, você pode escolher um dos seguintes **métodos de deploy** na Discloud:

<table data-card-size="large" data-view="cards"><thead><tr><th data-card-target data-type="content-ref"></th><th align="center"></th><th data-hidden></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td><a href="../../../how-to-host-using/dashboard.md">dashboard.md</a></td><td align="center">Faça upload e gerencie sua aplicação via interface web.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/discord-bot.md">discord-bot.md</a></td><td align="center">Faça deploy diretamente através dos comandos do bot Discord da Discloud.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/visual-studio-code.md">visual-studio-code.md</a></td><td align="center">Integre com VS Code para gerenciamento contínuo de projetos.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/cli.md">cli.md</a></td><td align="center">Use a interface de linha de comando para deploy rápido e eficiente.</td><td></td><td></td><td></td></tr></tbody></table>
