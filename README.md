# 🤖 pAiCoder v14

A production-grade AI design and coding agent — CLI + VS Code extension

**Design from anything. Build completely. Ship with confidence.**

> *"Do no wrong"* — pAiCoder is deliberate, structured, and fully reversible.  
> Every action is intentional. No surprises.

---

## Table of Contents

- [Configuration](#configuration)
- [VS Code Extension](#vs-code-extension)
- [Terminal UI (TUI)](#terminal-ui-tui)
- [Providers & Roles](#providers--roles)
- [Contact](#contact)

---

## Configuration

All config lives in `~/.paicoder/.env`. Edit directly, use the VS Code Setup panel,
or use `set-*` CLI commands.

```bash
# ~/.paicoder/.env
# API Keys
ANTHROPIC_API_KEY=sk-ant-...
XAI_API_KEY=xai-...
OPENAI_API_KEY=                     # optional
OLLAMA_HOST=http://localhost:11434  # optional

# Models
ANTHROPIC_MODEL=claude-opus-4-8
XAI_MODEL=grok-4.3
OPENAI_MODEL=gpt-5.4

# Roles
PLANNER=anthropic      # design, spec, architecture
CODER=xai              # implementation, file writing
AUDITOR=anthropic      # audit, security reports
AUTO_AUDITOR=xai       # quick hallucination guard

# Behavior
PARALLEL_MODE=false
MAX_WORKERS=3
AUTO_AUDIT=true
AUTO_APPROVE=false

# VS Code completion
INLINE_COMPLETION=true
DOCSTRING_COMPLETION=true
```

---

## VS Code Extension

Search and install pAiCoder from VS Code Marketplace 

---

## Terminal UI (TUI)

pAiCoder v14 ships with a full-featured Textual TUI — a keyboard-driven
terminal interface for managing projects without leaving the terminal.

### Launch

# From the built binary (requires rebuild after v14 upgrade)
~/.paicoder/pAiCoder 

---

## Providers & Roles

| Role | Default | Phase mapping |
|---|---|---|
| `PLANNER` | anthropic | spec, design, plan, refactor |
| `CODER` | xai | patch (write_file steps), chat, test |
| `AUDITOR` | anthropic | audit, security |
| `AUTO_AUDITOR` | xai | review, eval (quick post-delivery check) |

### Failover

| Role fails | Retries with | Affected commands |
|---|---|---|
| PLANNER | CODER | design, load-design, master-prompt |
| CODER | PLANNER | implementation steps |
| AUDITOR | CODER | audit-code |

**Offline with Ollama:**
```bash
PLANNER=ollama
CODER=ollama
OLLAMA_HOST=http://localhost:11434
OLLAMA_MODEL=llama3.1:8b
```
> Vision (load-design with images) requires anthropic, openai, or xai.

---

## Contact

  GitHub:  https://github.com/dachuyn/paicoder
  Email:   supports@paicoder.com
