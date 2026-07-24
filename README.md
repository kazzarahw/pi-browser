> [!IMPORTANT]
> **This repository is archived.** `pi-browser` now lives in [kazzarahw/pi-suite](https://github.com/kazzarahw/pi-suite)
> as [`browser/`](https://github.com/kazzarahw/pi-suite/tree/main/browser), alongside the other six extensions.
>
> The install command in this README **no longer works**. It fails with
> `Cannot find package 'pi-shared'`, because Pi installs packages with
> `npm install --omit=dev` while this repo imported shared runtime values from a
> `devDependency`. Consolidating the suite into a single package removed that
> failure mode entirely — `shared/` is now an internal module rather than a
> dependency, and CI guards it with a real `--omit=dev` install test.
>
> ```sh
> pi install git:github.com/kazzarahw/pi-suite
> ```
>
> Full commit history for these files is preserved in pi-suite.

---

# pi-browser

**The web in one tool** — a [Pi](https://pi.dev) extension wrapping the [`agent-browser`](https://www.npmjs.com/package/agent-browser) CLI: search, fetch, snapshot, and interact with real pages, over a persistent browser session. Keyless — no search API, no provider config.

Part of the [`pi-*` suite](https://github.com/kazzarahw/pi-shared).

## What it does

Registers one `browser` tool whose `action` selects an `agent-browser` verb, so search/fetch/automation are all one tight surface instead of many tools. A persistent daemon keeps the browser **session** alive across calls, so sequential actions act on the same page.

## Tool

```
browser({ action, url?, query?, ref?, text?, key?, values?, direction?, amount?, path?, what?, wait? })
```

Key actions:
- **`search`** — look something up (keyless). Tries `html.duckduckgo.com/html` first, falls back to Bing, and detects bot-walls to fall through.
- **`open`** + **`snapshot`** — load a page and get an accessibility tree with `@ref` handles (the primary AI sense).
- **`read`** — a page's text (optionally at a `url` — this is "fetch").
- **`click` / `type` / `fill` / `press` / `hover` / `select` / `check` / `scroll`** — interact, targeting an `@ref` or a CSS selector.
- **`back` / `forward` / `reload` / `wait` / `screenshot` / `get`** — navigation, capture, introspection.

## Configure

`/pi-browser` opens a settings panel (or `/pi-browser binPath <path>` / `session <name>`). Persisted to `~/.pi/agent/pi-browser.json`:

| Setting | Default | Meaning |
|---|---|---|
| `binPath` | `agent-browser` | the agent-browser binary |
| `session` | *(default)* | agent-browser session name, for isolation |

## Install

```sh
pi install git:github.com/kazzarahw/pi-browser
```

Requires the `agent-browser` CLI on `PATH`. AGPL-3.0.
