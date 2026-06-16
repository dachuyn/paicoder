# 🤖 pAiCoder v13

A production-grade AI design & coding agent — CLI + VS Code extension.  
**Design from anything. Build in parallel. Ship with confidence.**

> *"Do no wrong"* — pAiCoder is deliberate, structured, and fully reversible.  
> Every action is intentional. No surprises.

---

## Table of Contents

- [Quick Install](#quick-install)
- [Configuration](#configuration)
- [VS Code Extension](#vs-code-extension)
- [CLI Commands](#cli-commands)
- [Build from Source](#build-from-source)
- [Publish Binary + Extension](#publish-binary--extension)
- [Project States](#project-states)
- [Providers & Roles](#providers--roles)
- [Troubleshooting](#troubleshooting)

---

## API Keys

pAiCoder strongly recommends two API keys for the best experience:

| Key | Role | Why |
|---|---|---|
| `ANTHROPIC_API_KEY` | **PLANNER** (recommended) | Claude is the best model for structured thinking, nuanced requirements, and architecture decisions |
| `XAI_API_KEY` | **CODER** + AI images (recommended) | Grok is fast and cost-effective for implementation. Required for AI image generation (v13) |

```bash
# ~/.paicoder/.env
ANTHROPIC_API_KEY=sk-ant-...    # required
XAI_API_KEY=xai-...             # strongly recommended

PLANNER=anthropic               # Claude thinks best
CODER=xai                       # Grok executes fast
AUDITOR=anthropic               # Claude reviews carefully
```

Without `XAI_API_KEY`: pAiCoder works using Claude for all roles,
but AI image generation (v13) will be unavailable.

The combination is intentional — **Claude thinks, Grok executes.**
Together they cover the full lifecycle from design to deployed assets.

**Automatic failover:** if a role's provider call fails (e.g. an
invalid or expired API key), pAiCoder automatically retries ONCE with
a fallback provider — PLANNER↔CODER, and AUDITOR→CODER. See
[Providers & Roles](#providers--roles) for the full failover table.

---

### Install from VS Code Marketplace
```
Extensions panel → search "pAiCoder" → Install
→ binary downloads automatically for your platform (~30 sec)
→ setup panel opens for API keys
→ ready
```

---

## Configuration

All personal config lives in `~/.paicoder/.env`:

```bash
# API Keys
ANTHROPIC_API_KEY=sk-ant-...
XAI_API_KEY=...
OPENAI_API_KEY=          # optional
OLLAMA_HOST=http://localhost:11434  # optional

# Models
ANTHROPIC_MODEL=claude-opus-4-8
XAI_MODEL=grok-4.3
OPENAI_MODEL=gpt-5.4-mini
OLLAMA_MODEL=llama3.1:8b

# Roles — who does what (one-step failover on auth errors:
# PLANNER<->CODER, AUDITOR->CODER)
PLANNER=anthropic      # design, spec, refactor, orchestration, master-prompt
CODER=xai              # implementation, execution, parallel workers,
                       # AND auto-audit (hallucination guard after each patch)
AUDITOR=anthropic      # deep audit, security → full reports

# Behavior
PARALLEL_MODE=false
MAX_WORKERS=3
AUTO_AUDIT=true
AUTO_APPROVE=false

# VS Code completion
INLINE_COMPLETION=true     # Mode 1: ghost-text inline suggestions
DOCSTRING_COMPLETION=true  # Mode 2: implement function from docstring
```

### Priority (highest wins)
```
VS Code Cmd+, settings    ← explicit override
~/.paicoder/.env          ← personal config
```

### Configure roles from VS Code
```
Cmd+,  → search "paicoder roles"
→ PLANNER / CODER / AUDITOR dropdowns
```

Or:
```
Cmd+Shift+P → "pAiCoder: Setup — Configure API Keys & Roles"
```

---

## VS Code Extension

### Project States

| Files present | State | Menu shown |
|---|---|---|
| Nothing | Not adopted | Create / Adopt / Chat |
| `MASTER_PROMPT.md` | NEW | Plan from MASTER / Plan New / Chat |
| `SPEC.md` | SPEC_READY | Implement / Checkpoint / Chat |
| `SPEC.md` + `CHANGELOG.md` | DELIVERED | Plan Feature / Audit / Security / Refactor / Chat |

### Context menu commands

**Always (source files):**

| Command | What it does |
|---|---|
| ⚡ Implement from Docstring | Generate implementation from docstring |
| Explain Selected Code | Chat explains selected code |
| Fix Selected Code | Chat fixes selected code |
| Audit this File | Code quality audit on specific file |
| Refactor this File | Analysis-first refactor of specific file |

**By state:**

| State | Commands |
|---|---|
| Not adopted | Create Project, Adopt Project, Open Chat |
| NEW | Plan from MASTER_PROMPT, Plan New Project, Open Chat |
| SPEC_READY | Implement SPEC.md, Checkpoint, Open Chat |
| DELIVERED | Plan Feature, Audit Code, Audit Security, Refactor, Checkpoint, Open Chat |

### Status bar
Click the `$(robot) project-name` item in the status bar for quick actions:
- Open Project Chat
- Refresh Status
- Configure Roles & Models
- All Projects

---

## AWS Deployment

> **Full guide:** See [README_AWS.md](README_AWS.md) for complete AWS workflow,
> all deployment types, hybrid architecture, prerequisites, IAM permissions,
> cost guide, and troubleshooting.

pAiCoder can generate a complete AWS deployment for any project it owns or adopted.

```bash
# Interactive dialogue — auto-detects project type
pAiCoder --project my-app --aws-deploy

# Or from REPL
📝 Task> aws-deploy

# With a hint
📝 Task> aws-deploy use lambda
📝 Task> aws-deploy container
📝 Task> aws-deploy serverless
```

### Supported deployment types

| Type | Architecture | Best for |
|---|---|---|
| `static_site` | S3 + CloudFront + Route53 | HTML/CSS/JS, React, Vue SPAs |
| `lambda_api` | API Gateway + Lambda + DynamoDB | REST APIs, microservices, bots |
| `container` | ECS Fargate + ALB + RDS | Docker apps, complex backends |
| `webapp_ec2` | EC2 + ALB + RDS + CloudFront | Traditional web apps |
| `data_pipeline` | Glue + S3 + Athena | ETL, data lakes, analytics |
| `data_warehouse` | Glue + S3 + Redshift | Large-scale analytics, BI |
| `ml_pipeline` | SageMaker + S3 + Lambda | ML training + inference |
| `streaming` | Kinesis + Lambda + S3 | Real-time data processing |
| `event_driven` | SQS/EventBridge + Lambda | Async processing, queues |
| `hybrid_*` | On-prem + VPN + Cloud | Legacy system integration |

### Generated files

```
aws/
  cloud/
    stack.yaml          CloudFormation infrastructure
    parameters.json     Stack parameters
    deploy.yml          GitHub Actions (auto-deploy on push)
    destroy.yml         Teardown workflow
    deploy.sh           Local deploy script
  AWS-DEPLOYMENT.md     Architecture overview + instructions
```

### Secrets

AWS credentials are appended to your project `.env`:
```bash
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=us-east-1
STACK_NAME=my-project-prod
```

---

## CLI Commands

### Starting pAiCoder
```bash
pAiCoder                           # project picker
pAiCoder --project my-app          # open specific project
pAiCoder --path /path/to/folder    # open by path
pAiCoder --new my-app              # create new project
pAiCoder --project my-app --chat   # open in Chat mode
pAiCoder --version                 # show version
pAiCoder doctor                    # health check
```

### REPL commands

**Design & Planning**
```
design(claude) <desc>      design from description → SPEC
load-design(claude) <file> design from image/PDF/URL
master-prompt              load MASTER_PROMPT.md → design
plan <desc>                plan a sub-feature
```

**Implementation**
```
implement                  build from SPEC.md
implement #N               implement sub-feature N
parallel implement all     all features in parallel
```

**Code Quality**
```
audit                      code quality audit → AUDIT_REPORT.md
audit(claude) <file>       audit specific file
fix-audit                  fix critical issues
security                   security audit → SECURITY_REPORT.md
fix-security               fix security issues
refactor                   analysis-first refactor
refactor <file>            refactor specific file
```

**Chat**
```
chat                       conversational mode (full tools)
chat <message>             open with starting message
exit                       return to Task> from Chat
```

**Checkpointing**
```
checkpoint <name>          save named git checkpoint
restore <name>             restore to checkpoint
checkpoints                list all checkpoints
```

**Project**
```
status                     project dashboard
projects                   list all projects
features                   list sub-features
eval                       verify vs SPEC.md
docs                       generate docs
update-spec                reverse-engineer SPEC from code
```

**Meta**
```
setup                      configure API keys + roles
doctor                     health check
stats                      usage statistics
version                    version info
tips                       contextual suggestions
?  or  help                show all commands
exit                       quit
```

---

## Project States

```
🆕 NEW                     📐 SPEC_READY
No SPEC                    SPEC.md exists
→ design / plan            → implement
→ master-prompt                ↓
                       ✅ DELIVERED
                       SPEC.md + CHANGELOG.md
                       → plan feature
                       → audit / security / refactor
```

---

## Providers & Roles

| Role | Default | Used for |
|---|---|---|
| `PLANNER` | anthropic | design, spec, refactor, orchestration, master-prompt (+ aliases), load-design |
| `CODER` | xai | implementation, execution, parallel workers, **and auto-audit** (hallucination guard) |
| `AUDITOR` | anthropic | deep audit, security reports (audit-code) |

Change any role in `~/.paicoder/.env` or via `Cmd+,` in VS Code.

### Automatic failover

If a role's provider call fails with an authentication error (e.g. an
invalid or expired API key), pAiCoder automatically retries **once**
with a fallback provider — no manual intervention needed:

| Primary role | Fails over to | Commands affected |
|---|---|---|
| `PLANNER` | `CODER` | master-prompt (+ aliases), design, load-design, refactor* |
| `CODER` | `PLANNER` | general implementation work, auto-audit |
| `AUDITOR` | `CODER` | audit-code |

Exactly one failover step — if the fallback also fails, the original
error is shown. In the default config (`PLANNER=anthropic`,
`CODER=xai`, `AUDITOR=anthropic`), this also gives you automatic
cross-provider resilience without any extra setup.

\* **refactor is the one exception.** Because refactoring must
preserve codebase integrity, if the provider fails partway through a
multi-step refactor (after some files have already been edited),
pAiCoder does **not** switch providers mid-task. Instead, it
automatically restores the workspace to the pre-refactor checkpoint
(`git reset --hard` + `git clean -fd`) and prints a warning so you can
fix the provider issue and re-run `refactor` cleanly. The initial
analysis step (before any files are touched) still uses the normal
PLANNER→CODER failover.

**Use local Ollama (fully offline):**
```bash
PLANNER=ollama
CODER=ollama
AUDITOR=ollama
OLLAMA_HOST=http://localhost:11434
OLLAMA_MODEL=llama3.1:8b
```

> Note: `load-design` (image-based design input) requires
> `anthropic`, `openai`, or `xai` for the vision step — Ollama vision
> is not currently supported.

---

## Troubleshooting

| Problem | Fix |
|---|---|
| Bridge not connected | `View → Output → "pAiCoder Bridge"` for error details |
| "Installation failed" in status bar | Ignore — extension updated fine, just reload VS Code |
| Wrong project in status bar | `Cmd+Shift+P → "pAiCoder: Refresh Status"` |
| Model mismatch (404 from API) | Check `~/.paicoder/.env` — ANTHROPIC_MODEL must be claude-*, XAI_MODEL must be grok-* |
| projects shows "planning" | Update to v11 — now reads from filesystem |
| sessions.db lost | `pAiCoder` → `adopt /path/to/project` for each project |
| Trial expired | Re-install |
| `pAiCoder: command not found` | `source ~/.zshrc` or `export PATH="$HOME/.local/bin:$PATH"` |

### Diagnostic commands
```bash
pAiCoder doctor              # full health check
pAiCoder --version           # verify version
curl localhost:6839/health   # check bridge running
```
---

*pAiCoder - Helping developers develop better software faster*

*Plan with Claude. Implement with Grok. Refined through use. Designed to last.*

