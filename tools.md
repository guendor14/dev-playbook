# Tool Preferences

## Bash over PowerShell

Always use the Bash tool for shell commands (git, dotnet, CLI tools) — not the PowerShell tool.

The RTK hook intercepts Bash tool commands and rewrites them through `rtk` (e.g. `git status` → `rtk git status`), saving 60–90% of tokens on dev operations. The PowerShell tool bypasses this hook entirely.

Only use PowerShell when a command genuinely requires PowerShell syntax (registry access, `$env:` variables, PowerShell-specific cmdlets).
