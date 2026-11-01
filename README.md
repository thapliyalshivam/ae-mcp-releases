# AE MCP Releases

Installers for AE MCP, which lets Claude Code read and edit the active After Effects comp.

This repo holds releases only. Download the installer from the **Releases** page.

## Requirements

- A Mac with After Effects. AE MCP is tested on After Effects 2025 on macOS (arm64 and x86_64).
- [Claude Code](https://claude.com/claude-code)
- Node.js

## Install

1. Download `AE-MCP-<version>.pkg` from the newest release.
2. Open the pkg. macOS blocks it the first time because it's unsigned, so allow it in **System Settings > Privacy & Security**, then open it again.
3. Restart After Effects and open **Window > Extensions > AE MCP**.
4. Run the two commands the panel shows in a terminal, then start `claude`.

The installer does the following:

- Installs the AE MCP panel for all users.
- Copies the AE MCP Bridge plugin into every installed version of After Effects.
- Turns on `PlayerDebugMode` for the signed-in user, because the panel is unsigned. This lets Adobe apps load any unsigned CEP extension, not just this one.

## Update

Install the newer pkg and restart After Effects. If the Claude Code plugin changed, also run:

```bash
claude plugin marketplace update ae-plugins
claude plugin update after-effects@ae-plugins
```

## Use

With a comp open in After Effects, ask Claude Code to read or change it. Claude Code has these tools:

| Tool | Changes the project? |
|---|---|
| `ae_get_context` | No. Reads the comp. |
| `ae_preview_ops` | No. Previews edits. |
| `ae_apply_ops` | Yes. It runs as one undo group, and ops that fail preview are skipped. |
| `ae_run_script` | Yes. It runs any ExtendScript with no preview, for edits the ops can't express. It runs as one undo group. |
| `ae_status` | No. Reports whether the bridge is reachable, paused or active, and how many sessions are connected. |

## The panel

**Window > Extensions > AE MCP** shows the connection status, the connected Claude Code sessions and recent calls.

| Status | Meaning |
|---|---|
| **Active · N sessions** | Claude Code is connected. |
| **Idle · no sessions** | The bridge is running, but no Claude Code session is connected. |
| **Paused** | Claude Code can't read or change anything in After Effects until you resume. |
| **Offline** | The bridge plugin isn't loaded. |
| **Port error** | The bridge couldn't open its port. See Troubleshooting. |

Use **Pause** to block Claude Code at any time, including `ae_run_script`. Use **Test round-trip** to check the connection.

## Troubleshooting

- **The panel is missing from Window > Extensions:** restart After Effects. If it's still missing, reinstall the pkg.
- **The panel shows Offline:** the panel shows **Install bridge** if it can install the bridge into the running After Effects, which asks for an admin password. Otherwise, reinstall the pkg and restart After Effects.
- **The panel shows Port error:** the bridge uses `127.0.0.1:7391`. Check whether another app is using that port. To use a different port, set `AE_MCP_PORT` for both After Effects and Claude Code.
- **Claude Code doesn't have the tools:** the panel shows **Connect Claude Code** when it can't find the plugin. Run the commands it lists, using **Copy commands** to copy them, then restart `claude`.

## Release notes

Each release lists the changes since the previous one. New versions are published automatically.
# ae-mcp-releases
