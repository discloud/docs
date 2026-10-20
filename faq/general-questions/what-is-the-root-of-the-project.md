---
description: >-
  Understand the project root (base directory) so Discloud can detect configs,
  dependencies and your main file correctly.
---

# What is the root of the project?

## 🧾 Overview

The project root ("root directory") is the **top-level folder of your application,** the place you compress and upload to Discloud. It contains the configuration file ([`discloud.config`](../../configurations/discloud.config/)), dependency manifest (e.g. [`package.json`](../../development-environment/supported-languages/javascript/package.json.md), [`requirements.txt`](../../development-environment/supported-languages/python/requirements.txt.md), [`Cargo.toml`](../../development-environment/supported-languages/rust/cargo.toml.md), [`Gemfile`](../../development-environment/supported-languages/ruby/gemfile.md)), optional [`.env`](.env-file.md), and the folders with your source code (e.g. `src/`).

If the structure is wrong (for example, you zip a folder that contains another single folder that actually holds the files), Discloud may fail to detect the main file or dependencies.

***

## 🖼️ Visual Example

The green zone represents the **root** you should compress. Yellow shows a nested folder containing code files. Everything inside green is included once you zip that directory.

<figure><img src="../../.gitbook/assets/project-root-structure-example.png" alt=""><figcaption></figcaption></figure>

***

### 🚫 Common Mistakes

| Mistake                        | Result                             | Fix                                                                                           |
| ------------------------------ | ---------------------------------- | --------------------------------------------------------------------------------------------- |
| Zipping parent of actual root  | Missing config / main file         | Zip the folder containing [`discloud.config`](../../configurations/discloud.config/) directly |
| Including `node_modules`       | Large upload, possible size issues | Remove; let Discloud install                                                                  |
| Hardcoding tokens in code      | Security exposure                  | Use [`.env`](.env-file.md) and environment variables                                          |
| Multiple entry files ambiguous | Startup failure                    | Define `MAIN` in [`discloud.config`](../../configurations/discloud.config/) explicitly        |
