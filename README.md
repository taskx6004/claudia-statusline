# Claudia Statusline (Personal Build)

*Enhanced statusline for Claude Code - track costs, git status, and context usage in real-time*

![Claudia Statusline Screenshot](statusline.png)

A high-performance statusline for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) that shows workspace info, git status, model usage, session costs, and more.

This is a personal build based on the [original Claudia Statusline](https://github.com/hagan/claudia-statusline) by [hagan](https://github.com/hagan), which was itself inspired by [Peter Steinberger's statusline.rs](https://gist.github.com/steipete/8396e512171d31e934f0013e5651691e).

**Example output:**
```
~/myproject [main +2 ~1 ?3] • 45% [====------] Sonnet • 1h 23m • +150 -42 • $3.50 ($2.54/h)
```

## Install (Build from Source)

**Requirements**: Rust 1.70+ ([install](https://rustup.rs/))

```bash
git clone https://github.com/taskx6004/claudia-statusline
cd claudia-statusline
cargo build --release
install -m 755 target/release/statusline ~/.local/bin/statusline
```

Then add to your Claude Code settings (`~/.claude/settings.json`):

```json
{
  "statusLine": {
    "type": "command",
    "command": "~/.local/bin/statusline",
    "padding": 0
  }
}
```

Restart Claude Code and the statusline appears automatically.

## What You Get

- **Current directory** with `~` shorthand
- **Git branch and changes** (+2 added, ~1 modified, ?3 untracked)
- **Context usage** with progress bar (45% [====------])
- **Real-time compaction detection** (experimental) - instant feedback via hooks
- **Claude model** (O4.5/S4.5/H4.5 - consistent version display)
- **Session duration** (1h 23m)
- **Cost tracking** ($3.50 session, $2.54/hour burn rate)
- **Lines changed** (+150 added, -42 removed)

**Automatic features:**
- Persistent cost tracking across sessions
- Multi-console safe (run multiple Claude instances)
- **11 embedded themes** (dark, light, monokai, solarized, high-contrast, gruvbox, nord, dracula, one-dark, tokyo-night, catppuccin)
- **5 layout presets** (default, compact, detailed, minimal, power) with custom template support
- **4 model formats** (abbreviation: O4.5, full: Claude Opus 4.5, name: Opus, version: 4.5)
- SQLite database for reliability
- **Token rate metrics** (opt-in) - tokens/second with cache efficiency tracking
- **Hook-based compaction detection** (experimental, opt-in)
- **Adaptive context learning** (experimental, opt-in)
- No configuration needed (smart defaults)

## Documentation

- **[Installation Guide](docs/INSTALLATION.md)** - All platforms, build from source, troubleshooting
- **[Usage Guide](docs/USAGE.md)** - Commands, examples, JSON format, embedding API
- **[Configuration Guide](docs/CONFIGURATION.md)** - Themes, retention, git timeout, advanced settings
- **[Adaptive Learning Guide](docs/ADAPTIVE_LEARNING.md)** - Automatic context limit learning (experimental)
- **[Cloud Sync Guide](docs/CLOUD_SYNC.md)** - Turso setup for cross-machine stats (experimental)
- **[Database Migrations](docs/DATABASE_MIGRATIONS.md)** - Schema versioning and migrations

**Project docs:**
- **[ARCHITECTURE.md](ARCHITECTURE.md)** - Technical architecture and module design
- **[CONTRIBUTING.md](CONTRIBUTING.md)** - Development guidelines and debugging
- **[CHANGELOG.md](CHANGELOG.md)** - Version history and release notes

## Quick Start

### 1. Build and install

```bash
cargo build --release
install -m 755 target/release/statusline ~/.local/bin/statusline
```

### 2. Restart Claude Code

The statusline appears automatically - no configuration needed!

### 3. (Optional) Customize

```bash
# Change theme
export CLAUDE_THEME=light  # or dark (default)

# Disable colors
export NO_COLOR=1

# Advanced config
vim ~/.config/claudia-statusline/config.toml
```

**Layout Presets** - Choose from 5 built-in layouts:

| Preset | Output |
|--------|--------|
| `default` | `~/project • main +2 • 75% [======>---] • S4.5 • $12.50` |
| `compact` | `project main S4.5 $12` |
| `detailed` | Two-line with context on second line |
| `minimal` | `~/project S4.5` |
| `power` | Multi-line with all details |

```toml
# ~/.config/claudia-statusline/config.toml
[layout]
preset = "compact"  # Or create custom: format = "{directory} {model}"
```

See [Configuration Guide](docs/CONFIGURATION.md) for all options including per-component customization.

## Common Questions

<details>
<summary><b>Will this slow down Claude Code?</b></summary>

No. The binary completes in a few milliseconds on typical hardware.
</details>

<details>
<summary><b>Where is my data stored?</b></summary>

Locally in `~/.local/share/claudia-statusline/stats.db`. Nothing leaves your machine unless you enable cloud sync.
</details>

<details>
<summary><b>How do I uninstall?</b></summary>

```bash
rm ~/.local/bin/statusline
rm -rf ~/.local/share/claudia-statusline
rm -rf ~/.config/claudia-statusline
```

Then remove the `statusLine` section from `~/.claude/settings.json`.
</details>

## Troubleshooting

**"statusline not found"** after install?
```bash
export PATH="$HOME/.local/bin:$PATH"
# Add to ~/.bashrc or ~/.zshrc to persist
```

**Statusline shows only "~"?**
Ensure Claude Code settings are configured correctly (see Install section above).

**More help?** See [Installation Guide](docs/INSTALLATION.md#troubleshooting) and [Usage Guide](docs/USAGE.md#troubleshooting)

## Credits and Attribution

This is a personal build of [Claudia Statusline](https://github.com/hagan/claudia-statusline), originally developed by [hagan](https://github.com/hagan) and contributors.

**Original Inspiration**: [Peter Steinberger's statusline.rs](https://gist.github.com/steipete/8396e512171d31e934f0013e5651691e)

See [ATTRIBUTION.md](ATTRIBUTION.md), [NOTICE](NOTICE), and [CREDITS.md](CREDITS.md) for full attribution details.

**License**: MIT - See [LICENSE](LICENSE)
