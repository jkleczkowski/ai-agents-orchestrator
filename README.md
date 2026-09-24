# AI Agents Orchestrator

A lightweight manager for running many AI agent sessions side by side
(Claude Code, Codex, opencode) on macOS, Windows and Linux.

- **Remembers your sessions** — return to an earlier conversation with one click.
- **Tells you who is waiting** — hooks into the agents and flags the session that
  has stopped and needs your decision. That notification does not fade on its
  own; it clears only once you answer.
- **Markdown viewer** next to the terminal.

This repository holds **releases only**. The source code is not public.

## Install

Download the package for your platform from
[Releases](https://github.com/jkleczkowski/ai-agents-orchestrator/releases).

| Platform | File |
|---|---|
| macOS (Apple Silicon) | `*-osx-arm64-*` |
| Windows (Intel/AMD) | `*-win-x64-Setup.exe` |
| Windows (ARM) | `*-win-arm64-Setup.exe` |
| Linux (x64) | `*-linux-x64-*` |

### macOS — one-time unblock

Releases are not yet signed with an Apple Developer certificate, so macOS will
report the app as coming from an unidentified developer:

```bash
xattr -dr com.apple.quarantine "/Applications/AI Agents Orchestrator.app"
```

### Windows

SmartScreen warns when you launch the installer, because the binary is
unsigned: **More info** → **Run anyway**.

## Updates

The app updates itself: a new version downloads in the background and is applied
the next time you start it.

**An update never interrupts a running agent session.** The "restart now" button
appears only when no session is running — restarting mid-turn would destroy
exactly what this app exists to protect.

### Pointing at your own artifact server

By default updates come from this repository and need no configuration. In an
environment where artifacts must pass through an internal server (Artifactory,
Nexus, any HTTP server), point the app at it in `~/.aao/config.json`:

```json
{
  "UpdateSourceKind": "http",
  "UpdateSourceUrl": "https://artifactory.example.com/artifactory/aao-generic"
}
```

| Field | Default | Meaning |
|---|---|---|
| `UpdateEnabled` | `true` | `false` disables update checks entirely |
| `UpdateSourceKind` | `"github"` | `"github"` or `"http"` |
| `UpdateSourceUrl` | this repository | repository URL (`github`) or feed base URL (`http`) |
| `UpdateToken` | none | token for an authenticated feed |

If the feed requires authentication, supply the token through the
**`AAO_UPDATE_TOKEN` environment variable** — it takes precedence over the file
and leaves no secret on disk. The `UpdateToken` field exists as a fallback for
the app launched from Finder on macOS, which does not inherit shell variables.

## Project status

Early days. Developed and used mainly on macOS (Apple Silicon) — Windows and
Linux packages are built automatically but have not yet been exercised in real
use. Bug reports welcome in
[Issues](https://github.com/jkleczkowski/ai-agents-orchestrator/issues).
