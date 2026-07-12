# pAiCoder — Spec-First AI Coding, Multi-Cloud & LLM Deployment (macOS)

> **Free 30-day evaluation** · Idea → Spec → Code → Deploy · Bring your own models — Claude · Grok · GPT · Meta Muse Spark · local Ollama

pAiCoder turns an idea — a sentence, a document, or an architecture diagram — into a reviewable **`SPEC.md`**, then into working code, then into a real deployment. It's **spec-first**: you see and approve the plan before anything is built, and a deterministic audit gates every deployment. And it's **model-agnostic** — assign Claude, Grok, or GPT to different roles so speed, quality, and cost are levers *you* control.

---

## 🚀 Quick Start — two minutes to your first win

1. **Install** the extension.
2. **Add an API key** — `Cmd+Shift+P` → **`pAiCoder: Setup`** → paste an Anthropic, xAI, OpenAI, or Meta key. (You can add more later and assign them by role.)
3. **Open the panel** — `Cmd+Shift+P` → **`pAiCoder: Open Panel (REPL / Chat)`**. This is your command center: type a command, or just chat with the agent.
4. **Pick a first win:**

| You want to… | Do this |
|---|---|
| ✍️ **Write code faster** | Open a Python file, write a docstring, press **Tab** to accept the ghost-text implementation. |
| 🧱 **Build from an idea** | In the panel: `design a REST API for a todo app with auth` → review **SPEC.md** → `implement`. |
| ☁️ **Deploy infrastructure** | **`pAiCoder: Load Design from File/Image`** (drop in an architecture diagram) → review → `aws-deploy` (or `azure-deploy`, `google-deploy`, `oracle-deploy`). |
| 🤖 **Serve an open-source LLM** | In the panel: `llm-design` → answer a couple of questions → `llm-build` → `llm-deploy`. |

> 💡 Type **`help`** in the panel to see every command available in your build, and **`doctor`** to verify your setup and see which features are enabled.

---

## Why developers like pAiCoder

- **You approve the plan first.** Every build starts from a `SPEC.md` you can read, edit, and accept — no black-box code dumps.
- **Your models, your cost.** Mix providers by role — a fast model for completion, a strong one for design, an independent one for audits. Save up to ~70% on tokens versus single-model tools.
- **Idea to running system, in one tool.** The same assistant designs the app, writes the code, provisions the cloud, and can even stand up an open-source LLM — each step gated by a deterministic audit.
- **It reads your diagrams.** Hand it an architecture image and it produces the spec *and* the infrastructure.

---

## Design principles

- **Protocol-first architecture.** pAiCoder runs deterministic, auditable workflows rather than an autonomous "black-box" agent, which keeps its behavior predictable — every step is one you can inspect and approve.
- **Design-first.** Rather than jumping straight into code, it generates and refines a `SPEC.md` first, then builds from the plan you approved.
- **Diagram understanding.** Give it an architecture diagram and it reasons about the design to produce an implementation plan — following how the components connect, not just recognizing icons.
- **Multi-provider support.** Anthropic, xAI, OpenAI, Meta, and local Ollama are all first-class, so you pick models by capability, cost, or preference and assign them per role.
- **Infrastructure, not just application code.** The cloud workflows generate real infrastructure-as-code — Bicep for Azure, Terraform for Google Cloud and Oracle — along with the parameters, modules, and deploy/destroy scripts, extending the same spec-first flow into DevOps.
- **Validate before you deploy.** Before touching any cloud, pAiCoder checks that every module and parameter is wired up and flags unfilled secrets (passwords, connection strings, admin IDs) up front — a practical way to cut down on failed deployments.

---

## ✨ Features

### Spec-first workflow

```
description / doc / diagram  →  SPEC.md  →  code  →  deployment
```

Describe it, sketch it, or drop in a diagram — pAiCoder writes a reviewable spec, you approve it, then it implements. Add features later with `plan`, build with `implement`, and keep quality high with `audit` and `security` (each offers one-shot fixes).

### Inline & docstring completion

Ghost-text suggestions as you type, powered by *your* chosen model. Write a docstring and let pAiCoder fill in the function.

```python
def multiply(a, b):
    """Multiply two numbers and return the result."""
    # → press Tab to accept:  return a * b
```

- **Tab** or **Alt+\\** to accept a suggestion.
- For the cleanest experience, quiet the built-in dropdown: `"editor.quickSuggestions": { "other": "off" }`.

### Deploy to any major cloud

Turn a diagram or a description into production-ready infrastructure — then ship it.

**AWS · Azure · Google Cloud · Oracle Cloud**

- AWS generates a CloudFormation stack + GitHub Actions pipelines; Azure generates Bicep; Google and Oracle generate Terraform.
- `aws-deploy` · `azure-deploy` · `google-deploy` · `oracle-deploy` — each pairs with a `-status` and a `-destroy`.
- A broad library of deployment patterns (serverless APIs, containers, event-driven, data pipelines, AI/ML, and more).
- A deterministic audit validates the templates and **blocks the deploy until secrets and placeholders are filled** — no half-configured launches.

### Deploy open-source LLMs 🤖 *(new)*

Stand up your own model-serving endpoint — pAiCoder sizes it for you.

```
llm-design  →  llm-build  →  llm-deploy
```

- **`llm-design`** asks how many concurrent users you expect and your use case (chat, RAG, coding, batch), then recommends an open-weight model (e.g. Qwen, Mistral, Llama), the right GPU, and a monthly cost estimate — and writes a `SPEC.md` you can review and tweak.
- **`llm-build`** generates the GPU-VM infrastructure as Terraform, a startup script that installs the NVIDIA driver + serving engine (vLLM / SGLang / Ollama), and ready-to-run deploy/destroy scripts.
- **`llm-deploy`** runs the audit, confirms the cost, and provisions the VM; **`llm-status`** shows the live endpoint; **`llm-destroy`** tears it all down.
- Runs on **nine clouds** — AWS, Azure, Google Cloud, Oracle Cloud, **DigitalOcean, Nebius, Vultr, Scaleway, and Lambda Cloud** — and exposes an **OpenAI-compatible** endpoint you can point any client at.

### Your choice, your cost

Most AI coding tools lock you into one model. pAiCoder lets you assign providers by role:

```bash
# ~/.paicoder/.env
CODER=xai                          # fast & cost-effective — implementation + inline completion
XAI_MODEL=grok-4.5
PLANNER=anthropic                  # deep reasoning — design, spec, orchestration
ANTHROPIC_MODEL=claude-opus-4-8
AUDITOR=openai                     # an independent second opinion on audits
OPENAI_MODEL=gpt-5.4
META_MODEL=muse-spark-1.1          # key: MODEL_API_KEY (from dev.meta.ai)
```

**Recommended:** `PLANNER=anthropic`, `CODER=xai` — the best balance of speed, quality, and cost. Prefer a different coder? Set `CODER=meta` (Muse Spark) or `CODER=anthropic`. Want fully local and free? Point a role at **Ollama**.

### More in the panel

A full coding-agent **Project Chat**, **parallel implementation** across a whole spec, code and security **audits** with one-shot fixes, safe **refactors**, and resource checks — all from **`pAiCoder: Open Panel`**. Type `help` to explore, `doctor` to check your setup.

---

## Evaluation License

pAiCoder is free to use for **30 days** from first download. See [LICENSE](https://github.com/dachuyn/paicoder/blob/main/LICENSE) for details.

## Links

- [GitHub](https://github.com/dachuyn/paicoder)
- [Issues](https://github.com/dachuyn/paicoder/issues)
- [Website](https://www.paicoder.com)
- Contact: supports@paicoder.com
