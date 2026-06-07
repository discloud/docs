---
description: Complete guide to host Go applications on Discloud.
icon: golang
---

# Go

## 📁 **Preparing the Files**

Before uploading your project, you must **exclude unnecessary files** to optimize the deployment.

#### ❌ **Files to Exclude**

Ensure the following files and directories are **not** included in your [`.zip`](../../../faq/general-questions/wip-how-to-compress.md):

```diff
- bin/
- *.exe
- .git/
```

📌 **Use a** [**`.discloudignore`**](../../../configurations/.discloudignore.md) **file** to automatically exclude these files. Do **not** exclude `go.mod` or `go.sum`.

🔗 **Need help setting up your** [**`go.mod`**](go.mod.md) **or find** [**main file**](../../../faq/general-questions/what-is-the-main-file.md)**?**

***

### 🌐 **Hosting Websites & APIs in Go**

Before deploying your website or API on Discloud, ensure that you meet the following **requirements**:

{% hint style="success" %}
[Platinum plan or higher](https://discloud.com/plans) is required to host websites or APIs.
{% endhint %}

{% hint style="success" %}
[A subdomain must be created](../../../faq/general-questions/how-to-create-a-subdomain.md) before deployment.
{% endhint %}

{% hint style="danger" %}
Port `8080` is mandatory – Applications must listen on this port.
{% endhint %}

{% tabs %}
{% tab title="🤖 Discord Bot" %}
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
  if token == "" { log.Fatal("DISCORD_TOKEN not set") }

  dg, err := discordgo.New("Bot " + token)
  if err != nil { log.Fatal(err) }

  dg.AddHandler(func(s *discordgo.Session, r *discordgo.Ready) {
    log.Println("Bot is ready")
  })

  if err := dg.Open(); err != nil { log.Fatal(err) }
  log.Println("Bot running. Press CTRL+C to exit.")

  stop := make(chan os.Signal, 1)
  signal.Notify(stop, os.Interrupt, syscall.SIGTERM)
  <-stop
  dg.Close()
}
```

> Bots do not need to bind any HTTP port. They just have to keep the process alive.
{% endtab %}

{% tab title="⚙️ Basic HTTP Server" %}
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
    fmt.Fprintln(w, "Hello from Go on Discloud!")
  })

  log.Println("Starting server on :8080")
  if err := http.ListenAndServe(":8080", mux); err != nil {
    log.Fatal(err)
  }
}
```
{% endtab %}

{% tab title="🔀 REST API (chi)" %}
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
    w.Write([]byte("Hello, "+name))
  })
  log.Println("API on :8080")
  log.Fatal(http.ListenAndServe(":8080", r))
}
```
{% endtab %}
{% endtabs %}

***

## ✍️ **Deploying Your Application**

Once your project is **configured and compressed**, you can choose one of the following **deployment methods** on Discloud:

<table data-card-size="large" data-view="cards"><thead><tr><th data-card-target data-type="content-ref"></th><th align="center"></th><th data-hidden></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td><a href="../../../how-to-host-using/dashboard.md">dashboard.md</a></td><td align="center">Upload and manage your application via the web interface.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/discord-bot.md">discord-bot.md</a></td><td align="center">Deploy directly through Discloud’s Discord bot commands.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/visual-studio-code.md">visual-studio-code.md</a></td><td align="center">Integrate with VS Code for seamless project management.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/cli.md">cli.md</a></td><td align="center">Use the command-line interface for quick and efficient deployment.</td><td></td><td></td><td></td></tr></tbody></table>
