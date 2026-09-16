# Kino

**The agentic workflow platform that lets one person ship a whole sprint.**
Built for agent-native companies — teams where the humans plan and review,
and coding agents do the work.

Drop a folder. Get a kanban board. Dispatch agents on every card — at the
same time, each in its own git worktree. Or hit autopilot and run the whole
sprint: cards dispatch in dependency order, get reviewed and fixed
automatically, and land themselves while you sleep. Works with 11 agent CLIs
— Claude Code, Codex, Gemini, Cursor, Copilot, Amp, OpenCode, Droid, CCR,
Qwen, plus any ACP-compatible CLI.

Free to use. This repo hosts the downloads; the source is not public.

## Download

Latest build: **[releases/latest](../../releases/latest)**

| Platform            | File                                |
| ------------------- | ----------------------------------- |
| macOS Apple Silicon | `kino-<version>-mac-arm64.dmg`      |
| macOS Intel         | `kino-<version>-mac-x64.dmg`        |
| Windows x64         | `kino-<version>-win-x64.exe`        |
| Linux x64           | `kino-<version>-linux-x64.AppImage` |
| Linux x64           | `kino-<version>-linux-x64.tar.xz`   |

## First launch — read this

Builds are **not code-signed** (certificates are a recurring cost this project
does not carry yet). Your OS will object the first time, once:

### macOS

Drag `Kino.app` to `/Applications`, then:

- **macOS 15 and newer** — you'll see _"Kino is damaged and can't be opened.
  You should move it to the Trash."_ It is not damaged; that is the wording
  macOS uses for unsigned apps now, and right-click → Open does **not** get
  past it. Clear the quarantine flag:

  ```sh
  xattr -dr com.apple.quarantine "/Applications/Kino.app"
  ```

  Then open it normally.

- **macOS 14 and older** — you'll see _"Apple cannot check it for malicious
  software."_ Right-click the app, choose **Open**, then **Open** again.

### Windows

SmartScreen shows _"Windows protected your PC."_ Click **More info** →
**Run anyway**.

### Linux

AppImage: `chmod +x kino-<version>-linux-x64.AppImage` and run it.
Tarball: extract anywhere and run `./kino`.

You only go through this once per machine.

## Updating

Kino checks for updates automatically and lets you know two ways: a toast
in the app, and a **Check for updates** entry in the account menu
(bottom-left).

- **macOS (signed), Windows, Linux AppImage** — the update downloads in
  the background and installs the next time you quit. The toast says
  "Update ready — restart to update"; click it (or the account menu
  entry) to restart now.
- **macOS (unsigned), Linux tar.xz** — the app can see a new version but
  can't install it in place. The toast says "Update available"; click it
  to open this releases page and download the new build the same way you
  got this one.

You can also watch this repo (**Watch → Custom → Releases**) to hear
about new versions as they're published.

## What you need

Kino doesn't sign you in to anything — it calls the agent CLIs already on
your `PATH`, reusing whatever auth they have. Install **at least one**:

| Agent              | CLI            | Sign in                 |
| ------------------ | -------------- | ----------------------- |
| Claude Code        | `claude`       | `claude /login`         |
| Codex              | `codex`        | `codex login`           |
| Gemini             | `gemini`       | `gemini auth`           |
| Cursor CLI         | `cursor-agent` | `cursor-agent login`    |
| GitHub Copilot CLI | `gh-copilot`   | `gh auth login`         |
| Amp                | `amp`          | `amp login`             |
| OpenCode           | `opencode`     | `opencode auth`         |
| Droid              | `droid`        | `droid auth`            |
| CCR                | `ccr`          | reuses Claude Code auth |
| Qwen Code          | `qwen`         | `qwen auth`             |

You'll also want **git**. Add `gh` + `gh auth login` if you want Kino to
drive real GitHub Issues rather than its own local board.

## First run

Pick any folder containing a git repository. Kino creates a `.kino/`
directory inside it — SQLite database, config, and per-run worktrees — and
drops you on the board. Nothing is written outside that directory.

Your data is local. There is no account and no server.

## Heads up

Agents write and delete files in the repositories you point them at, and spawn
processes on your machine. Every run happens in an isolated git worktree with a
pre-push hook that stops agents pushing on their own, and landing work on a real
branch is always an explicit click. Even so: **review what an agent produces
before you promote it, and keep backups.**

## Reporting a problem

Open an issue on this repo. Include your OS and the version from the app's
**About** panel.

## License

Proprietary. Copyright © 2026 LiansTech. All rights reserved. Free to download
and use; not open-source, and not redistributable. Bundled third-party
open-source components keep their own licenses.
