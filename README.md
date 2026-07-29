# TronTerm

**A native macOS terminal for developers who live inside AI tools.**
Free download, Developer ID signed and Apple notarized — opens without a warning.

If you spend your day in Claude Code, Codex, or another AI CLI, TronTerm is built for
you. It isn't trying to out-feature iTerm2 or replace Ghostty — both are excellent,
mature terminals. TronTerm is an **AI cockpit**: AI as a first-class citizen, and
long-running agents that don't die when you close the window.

## Install

**Homebrew (recommended)**

```sh
brew install --cask pct/tap/tronterm
```

**Direct download** — grab `TronTerm-x.y.z.zip` from
[Releases](https://github.com/pct/tronterm/releases/latest), unzip, and drag
`TronTerm.app` into Applications. It's notarized by Apple, so Gatekeeper won't
complain.

Requires macOS 13 (Ventura) or later, Apple Silicon.

## It doesn't freeze when AI floods the screen

AI TUIs repaint thousands of times per second, and that's exactly when ghostty and
iTerm2 start to stutter. Three defenses make stalling structurally impossible:

1. **Off-thread parsing** — PTY reads and VT parsing run on background queues. The
   main thread only handles input and drawing.
2. **Frame coalescing** — the parser consumes all output immediately; rendering caps
   at 60fps and only ever draws the latest frame.
3. **Hard resource ceilings** — scrollback is capped, so memory has a provable upper
   bound.

Rendering goes through CoreText + NSView, the mature system path. No custom GPU
pipeline to destabilize your Mac.

## Built-in AI, vendor-neutral

Other terminals that added AI lock you to one vendor and ask you to paste an API key.
TronTerm does neither.

- **⌘I — natural language → command.** Describe what you want. The AI gets your
  current screen, working directory, and history as context, then fills the command
  into your input line. Nothing runs until *you* press Enter.
- **⌘E — explain the screen.** Ask what an error means and how to fix it.
- **Every AI you've installed, auto-detected.** On launch TronTerm scans your PATH and
  adds the CLIs you already have — `claude`, `codex`, `gemini`, `llm`, `ollama`, and
  friends. Switch between them from the **AI ▸ Engine** menu: your best model for hard
  problems, a cheap one for chores, one click apart. No API keys, no SDK lock-in, no
  vendor owning your terminal.
- **Memory stays local.** Command history and AI interactions live in a local SQLite
  file (`~/.tronterm/tronterm.db`). Not a byte leaves your machine.

The AI engine runs in an isolated subprocess with a hard timeout — it can never drag
down your terminal or leave zombie processes behind.

## Let agents run overnight — closing the window won't kill them

The bundled `tt-daemon` keeps sessions alive independently of windows. Start an agent,
close the window, reopen TronTerm later and reattach — your shell and your agent are
still running. Nothing to install, no tmux to learn. Native session persistence.

## Also a genuinely good terminal

Split panes, Quick Terminal (global hotkey dropdown), search, mouse reporting, prompt
marks and jumping, resize reflow, undercurl, 24-bit color, full CJK and input-method
support, configurable themes, and a clean iTerm-style settings panel. UI available in
7 languages.

## Privacy

TronTerm runs locally and never sends terminal contents back to the vendor. AI
features invoke the command-line tool you configured yourself, so where your data goes
is determined by the AI vendor you chose.

---

<sub>Copyright © 2026 1Tron System Co., Ltd. This repository hosts releases and issue
reports; the source is not public.</sub>
