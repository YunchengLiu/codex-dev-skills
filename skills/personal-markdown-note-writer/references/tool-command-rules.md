# Tool Note: Command Rules

Tool notes often fail because commands are either too specific (only works on your machine) or too generic (all placeholders).

## Defaults

- Prefer a **recommended path** (the one you want future-you to follow).
- Use placeholders only for values that truly vary across machines/accounts.

### Placeholder policy

Preferred placeholder format: `<UPPER_SNAKE_CASE>`.

Common placeholders:

- `<HOST>`, `<USER>`, `<PORT>`, `<PATH>`, `<FILE>`, `<DIR>`, `<TOKEN>`

Rules:

- Every placeholder must have a one-line “how to decide it”.
- Allow other `<UPPER_SNAKE_CASE>` placeholders only when necessary; keep the set small and define each once in the note.
- Do not replace everything with placeholders. If `~/.ssh/config` is stable, write it as-is.
- Avoid “over-defensive templates”: the goal is speed and correctness, not universal coverage.

## Secrets / sensitive data

- Never include real secrets (tokens, passwords, private keys) in the note text. Use placeholders like `<TOKEN>`.
- Explain where to obtain the secret (password manager / env var / admin portal) instead of pasting it.
- If the input contains a secret, redact it in the output even for self-notes.
- If the input contains clearly sensitive identifiers (internal domains, account names, machine-specific private paths) and they are not essential to reproduce the steps, prefer placeholders.

## Write commands for the stated environment

- If the note targets `zsh`/`bash`, use `bash` blocks and POSIX-friendly syntax.
- If the note targets PowerShell, use `pwsh` blocks and PowerShell idioms.
- If OS/shell is unclear and affects commands, stop and ask.
- If commands require elevated privileges, a remote host, a container/WSL, or a specific working directory and that context is unclear, stop and ask before drafting steps.
- When a step needs elevated privileges, annotate that step with the required privilege and why (e.g., 需 `sudo`：写入 `/etc/hosts`), instead of adding a long global warning block.
- For each `<PATH>`/`<DIR>`, state whether it is absolute or relative to the declared working directory; quote paths with spaces using shell-appropriate quoting.
- If the note must support multiple environments, split by subsections (e.g., “macOS/Linux (bash)” vs “Windows (pwsh)”) and do not mix syntaxes in one step.

## Include verification

Every tool note should include at least one verification:

- A command to check status
- A quick manual check (“open file X and confirm …”)
- A small smoke test (run a minimal command, expected output)
- Whenever possible, include expected output or a crisp success criterion.

## Safety guidance

When a command is destructive or changes system-level settings:

- Call it out explicitly.
- Keep the warning close to the relevant step; do not add a separate “注意事项/安全” section.
- If there is a safe dry-run or backup step, include it.
- Do not suggest `rm -rf`, registry edits, broad permission changes (e.g. `chmod -R`, `chown -R`), or destructive deletions unless the user asked for it and the context is clear.
- If a small permission fix is required (e.g. `chmod 600` on a key file), state the exact file and why.
