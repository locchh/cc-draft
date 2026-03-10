# Claude Code CLI Reference

## 1. CLI Commands

| Command | Description |
|---------|-------------|
| `claude` | Start interactive REPL |
| `claude "query"` | Start REPL with initial prompt |
| `claude -p "query"` | Print response and exit (useful for pipes) |
| `cat file \| claude -p "query"` | Process piped content |
| `claude -c` | Continue most recent conversation in current directory |
| `claude -c -p "query"` | Continue in print mode |
| `claude -r [value]` | Resume by session ID, or open interactive picker with optional search term |
| `claude auth` | Manage authentication |
| `claude doctor` | Check the health of your Claude Code auto-updater |
| `claude install [target]` | Install Claude Code native build (`stable`, `latest`, or specific version) |
| `claude mcp` | Configure and manage MCP servers |
| `claude plugin` | Manage Claude Code plugins |
| `claude setup-token` | Set up a long-lived authentication token (requires Claude subscription) |
| `claude update` / `claude upgrade` | Check for updates and install if available |

---

## 2. CLI Options / Flags

### Core Execution

| Flag | Description |
|------|-------------|
| `-p`, `--print` | Print response and exit (useful for pipes). Skips workspace trust dialog |
| `-c`, `--continue` | Continue the most recent conversation in the current directory |
| `-r`, `--resume [value]` | Resume a conversation by session ID, or open interactive picker with optional search term |
| `--session-id <uuid>` | Use a specific session ID for the conversation (must be a valid UUID) |
| `--fork-session` | When resuming, create a new session ID instead of reusing the original (use with `--resume` or `--continue`) |

### Model & Tools

| Flag | Description |
|------|-------------|
| `--model <model>` | Model for the current session. Alias (`sonnet`, `opus`) or full name (e.g. `claude-sonnet-4-5-20250929`) |
| `--effort <level>` | Effort level for the current session (`low`, `medium`, `high`) |
| `--fallback-model <model>` | Enable automatic fallback to specified model when default is overloaded (`--print` only) |
| `--tools <tools...>` | Specify available built-in tools. `""` to disable all, `"default"` for all, or tool names (e.g. `"Bash,Edit,Read"`) |
| `--allowedTools <tools...>` | Comma or space-separated list of tool names to allow (e.g. `"Bash(git:*) Edit"`) |
| `--disallowedTools <tools...>` | Comma or space-separated list of tool names to deny (e.g. `"Bash(git:*) Edit"`) |
| `--disable-slash-commands` | Disable all skills |

### System Prompt

| Flag | Description |
|------|-------------|
| `--system-prompt <prompt>` | System prompt to use for the session |
| `--append-system-prompt <prompt>` | Append a system prompt to the default system prompt |

### Permissions & Security

| Flag | Description |
|------|-------------|
| `--permission-mode <mode>` | Permission mode: `acceptEdits`, `bypassPermissions`, `default`, `delegate`, `dontAsk`, `plan` |
| `--dangerously-skip-permissions` | Bypass all permission checks. Recommended only for sandboxes with no internet access |
| `--allow-dangerously-skip-permissions` | Enable bypassing permissions as an option without enabling it by default |

### Configuration & Context

| Flag | Description |
|------|-------------|
| `--settings <file-or-json>` | Path to a settings JSON file or a JSON string to load additional settings from |
| `--setting-sources <sources>` | Comma-separated list of setting sources to load (`user`, `project`, `local`) |
| `--add-dir <directories...>` | Additional directories to allow tool access to |
| `--mcp-config <configs...>` | Load MCP servers from JSON files or strings (space-separated) |
| `--strict-mcp-config` | Only use MCP servers from `--mcp-config`, ignoring all other MCP configurations |
| `--file <specs...>` | File resources to download at startup. Format: `file_id:relative_path` |

### Agents

| Flag | Description |
|------|-------------|
| `--agent <agent>` | Agent for the current session. Overrides the `agent` setting |
| `--agents <json>` | JSON object defining custom agents (e.g. `'{"reviewer": {"description": "...", "prompt": "..."}}'`) |

### Session Resume

| Flag | Description |
|------|-------------|
| `--from-pr [value]` | Resume a session linked to a PR by PR number/URL, or open interactive picker with optional search term |

### Output & Format

| Flag | Description |
|------|-------------|
| `--output-format <format>` | Output format (`--print` only): `text` (default), `json` (single result), `stream-json` (realtime streaming) |
| `--input-format <format>` | Input format (`--print` only): `text` (default), `stream-json` (realtime streaming input) |
| `--include-partial-messages` | Include partial message chunks as they arrive (`--print` + `--output-format=stream-json` only) |
| `--replay-user-messages` | Re-emit user messages from stdin back on stdout (`--input-format=stream-json` + `--output-format=stream-json` only) |
| `--json-schema <schema>` | JSON Schema for structured output validation (`--print` only) |
| `--verbose` | Override verbose mode setting from config |

### Budget & Limits

| Flag | Description |
|------|-------------|
| `--max-budget-usd <amount>` | Maximum dollar amount to spend on API calls (`--print` only) |
| `--no-session-persistence` | Disable session persistence - sessions will not be saved to disk and cannot be resumed (`--print` only) |

### Plugins & Integrations

| Flag | Description |
|------|-------------|
| `--plugin-dir <paths...>` | Load plugins from directories for this session only (repeatable) |
| `--ide` | Automatically connect to IDE on startup if exactly one valid IDE is available |
| `--chrome` | Enable Claude in Chrome integration |
| `--no-chrome` | Disable Claude in Chrome integration |

### Debugging

| Flag | Description |
|------|-------------|
| `-d`, `--debug [filter]` | Enable debug mode with optional category filtering (e.g. `"api,hooks"` or `"!1p,!file"`) |
| `--debug-file <path>` | Write debug logs to a specific file path (implicitly enables debug mode) |
| `--betas <betas...>` | Beta headers to include in API requests (API key users only) |

### Info

| Flag | Description |
|------|-------------|
| `-h`, `--help` | Display help for command |
| `-v`, `--version` | Output the version number |

---

## 3. Slash Commands (Interactive REPL)

### Session Management

| Command | Description |
|---------|-------------|
| `/clear` | Clear conversation history and free up context |
| `/exit` | Exit the REPL |
| `/fork` | Create a fork of the current conversation at this point |
| `/rename <name>` | Rename the current conversation |
| `/resume [session]` | Resume a previous conversation |
| `/rewind` | Restore code and/or conversation to a previous point |

### Settings & Config

| Command | Description |
|---------|-------------|
| `/config` | Open config panel |
| `/extra-usage` | Configure extra usage to keep working when limits are hit |
| `/fast` | Toggle fast mode (Opus 4.6 only) |
| `/hooks` | Manage hook configurations for tool events |
| `/model` | Set the AI model for Claude Code |
| `/output-style` | Set the output style directly or from a selection menu |
| `/permissions` | Manage allow & deny tool permission rules |
| `/privacy-settings` | View and update your privacy settings |
| `/sandbox` | Configure sandbox settings |
| `/status` | Show version, model, account, API connectivity, tool statuses |
| `/statusline` | Set up Claude Code's status line UI |
| `/terminal-setup` | Install Shift+Enter key binding for newlines |
| `/theme` | Change the theme |
| `/vim` | Toggle between Vim and Normal editing modes |

### Context & Memory

| Command | Description |
|---------|-------------|
| `/compact [instructions]` | Clear history but keep summary. Optional focus instructions |
| `/context` | Visualize current context usage as a colored grid |
| `/init` | Initialize a new `CLAUDE.md` file with codebase documentation |
| `/memory` | Edit Claude memory files |

### Analysis & Debugging

| Command | Description |
|---------|-------------|
| `/debug [description]` | Debug current session by reading the session debug log |
| `/doctor` | Diagnose and verify Claude Code installation and settings |
| `/insights` | Generate a report analyzing your Claude Code sessions |
| `/stats` | Show usage statistics and activity |
| `/usage` | Show plan usage limits |

### Tools & Integration

| Command | Description |
|---------|-------------|
| `/add-dir` | Add a new working directory |
| `/agents` | Manage agent configurations |
| `/chrome` | Claude in Chrome (Beta) settings |
| `/copy` | Copy Claude's last response to clipboard as markdown |
| `/desktop` | Continue the current session in Claude Desktop |
| `/export [filename]` | Export the current conversation to a file or clipboard |
| `/help` | Show help and available commands |
| `/ide` | Manage IDE integrations and show status |
| `/mcp` | Manage MCP servers |
| `/mobile` | Show QR code to download the Claude mobile app |
| `/plan` | Enable plan mode or view the current session plan |
| `/plugin` | Manage Claude Code plugins |
| `/remote-env` | Configure the default remote environment for teleport sessions |
| `/skills` | List available skills |
| `/tasks` | List and manage background tasks |
| `/todos` | List current todo items |

### GitHub & Code Review

| Command | Description |
|---------|-------------|
| `/install-github-app` | Set up Claude GitHub Actions for a repository |
| `/install-slack-app` | Install the Claude Slack app |
| `/pr-comments` | Get comments from a GitHub pull request |
| `/review` | Review a pull request |
| `/security-review` | Complete a security review of pending changes on current branch |

### Account

| Command | Description |
|---------|-------------|
| `/feedback` | Submit feedback about Claude Code |
| `/login` | Sign in with your Anthropic account |
| `/logout` | Sign out from your Anthropic account |
| `/release-notes` | View release notes |
| `/stickers` | Order Claude Code stickers |
| `/upgrade` | Upgrade to Max for higher rate limits and more Opus |

### User-Invocable Skills

| Command | Description |
|---------|-------------|
| `/generate-tests` | Generate comprehensive test suite with unit, integration, and edge case coverage |

### Special Prefixes

| Prefix | Description |
|--------|-------------|
| `!command` | Run bash command directly, add output to context |
| `@path` | File path autocomplete/mention |
| `/mcp__<server>__<prompt>` | Use MCP server prompts |

---

## 4. Keyboard Shortcuts

| Shortcut | Description |
|----------|-------------|
| `Ctrl+C` | Cancel current input/generation |
| `Ctrl+D` | Exit session |
| `Ctrl+G` | Open in text editor |
| `Ctrl+L` | Clear terminal screen |
| `Ctrl+O` | Toggle verbose output |
| `Ctrl+R` | Reverse search history |
| `Ctrl+V` | Paste image from clipboard |
| `Ctrl+B` | Background running tasks |
| `Ctrl+T` | Toggle task list |
| `Shift+Tab` / `Alt+M` | Toggle permission modes |
| `Option+P` / `Alt+P` | Switch model |
| `Option+T` / `Alt+T` | Toggle extended thinking |
| `Esc+Esc` | Rewind or summarize |
| `\` + `Enter` | Newline in input |
