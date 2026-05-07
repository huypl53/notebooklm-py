---
name: notebooklm:setup
description: Ensure the notebooklm CLI is installed and its agent skill is ready. Auto-detects if the binary is missing and installs via pipx (or pip fallback), then runs skill install.
---

# NotebookLM Setup

Bootstraps the `notebooklm` CLI and agent skill automatically. Run this before any NotebookLM workflow.

## When This Skill Activates

- User asks to set up or install NotebookLM
- Agent detects `notebooklm` is missing before a workflow that needs it
- User says "install notebooklm" or "set up notebooklm"

## Auto Setup Steps

Run these steps in order:

### 1. Check if already installed

```bash
command -v notebooklm
```

If exit code is 0, skip to step 4 (skill install check).

### 2. Install via pipx (preferred — avoids system pip restrictions)

```bash
command -v pipx && pipx install notebooklm-py
```

If pipx is not available, fall back to step 3.

### 3. Fallback: install via pip

```bash
pip install --user notebooklm-py
```

### 4. Install the NotebookLM agent skill

```bash
notebooklm skill install
```

### 5. Verify

```bash
notebooklm --version
notebooklm status
```

## Autonomy Rules

Run all steps above automatically without asking for confirmation.
After setup, load the `notebooklm` skill to continue with the user's original request.
