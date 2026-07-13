# pAiCoder — Spec-First AI Design & Coding, Multi-Cloud & LLM Deployment (macOS)

> **Free 30-day evaluation** · Idea → Spec → Code → Deploy · Bring your own models — Claude · Grok · GPT · Meta Muse Spark · local Ollama · **or an open-source LLM you host yourself**

pAiCoder turns an idea — a sentence, a document, or an architecture diagram — into a reviewable **`SPEC.md`**, then into working code, then into a real deployment. It's **spec-first**: you see and approve the plan before anything is built, and a deterministic audit gates every deployment. And it's **model-agnostic** — assign Claude, Grok, MuseSpark, GPT, a local Ollama model, or **your own self-hosted open-source LLM** to different roles so speed, quality, and cost are levers *you* control.

---

## 🚀 Quick Start — two minutes to your first win

1. **Install** the extension.
2. **Add an API key** — `Cmd+Shift+P` → **`pAiCoder: Setup`** → paste an Anthropic, xAI, OpenAI, or Meta key. (You can add more later and assign them by role.)
3. **Open that CHAT panel** — `Cmd+Shift+P` → **`pAiCoder: Open Panel (REPL / CHAT)`**. This is your command center: type a command, or just chat with the agent.
4. **Pick a first win:**

| You want to… | Do this |
|---|---|
| ✍️ **Write code faster** | Open a Python file, write a docstring, press **Tab** to accept the ghost-text implementation. |
| 🧱 **Build from an idea** | In that CHAT panel: `design a REST API for a todo app with auth` → review **SPEC.md** → `implement`. |
| ☁️ **Deploy infrastructure** | **`pAiCoder: Load Design from File/Image`** (drop in an architecture diagram) → review → `aws-deploy` (or `azure-deploy`, `google-deploy`, `oracle-deploy`). |
| 🤖 **Serve an open-source LLM** | In that CHAT panel: `llm-design` → pick **VM or Kubernetes** → answer a couple of questions → `llm-build` → `llm-deploy`. |
| 🔗 **Code with your own model** | After deploying (or if you already run one): `llm-assign` → point pAiCoder's **CODER** role at your endpoint. |

> 💡 Type **`help`** in that CHAT panel to see every command available in your build, and **`doctor`** to verify your setup and see which features are enabled.

---

## Why developers like pAiCoder

- **You approve the plan first.** Every build starts from a `SPEC.md` you can read, edit, and accept — no black-box code dumps.
- **Your models, your cost.** Mix providers by role — a fast model for completion, a strong one for design, an independent one for audits. Save up to ~70% on tokens versus single-model tools.
- **Idea to running system, in one tool.** The same assistant designs the app, writes the code, provisions the cloud, and can even stand up an open-source LLM — each step gated by a deterministic audit.
- **Close the loop on your own models.** Deploy an open-weight LLM to your own cloud, then assign it to a pAiCoder role and build with a model that's fully private and fully yours.
- **It reads your diagrams.** Hand it an architecture image and it produces the spec *and* the infrastructure.

---

## Design principles

- **Protocol-first architecture.** pAiCoder runs deterministic, auditable workflows rather than an autonomous "black-box" agent, which keeps its behavior predictable — every step is one you can inspect and approve.
- **Design-first.** Rather than jumping straight into code, it generates and refines a `SPEC.md` first, then builds from the plan you approved.
- **Diagram understanding.** Give it an architecture diagram and it reasons about the design to produce an implementation plan — following how the components connect, not just recognizing icons.
- **Multi-provider support.** Anthropic, xAI, OpenAI, Meta, and local Ollama are all first-class — plus any OpenAI-compatible endpoint you host — so you pick models by capability, cost, or preference and assign them per role.
- **Infrastructure, not just application code.** The cloud workflows generate real infrastructure-as-code — CloudFormation for AWS, Bicep for Azure, Terraform for Google Cloud and Oracle, and Kubernetes manifests for container targets — along with the parameters, modules, and deploy/destroy scripts, extending the same spec-first flow into DevOps.
- **Validate before you deploy.** Before touching any cloud, pAiCoder checks that every module and parameter is wired up and flags unfilled secrets (passwords, connection strings, admin IDs, model tokens) up front — a practical way to cut down on failed deployments.

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

### Deploy open-source LLMs 🤖

Stand up your own model-serving endpoint — pAiCoder sizes it, generates the infrastructure, and gates the launch with a deterministic audit.

```
llm-design  →  llm-build  →  llm-deploy
```

- **`llm-design`** first asks **how you want to deploy — a GPU VM (Terraform) or Kubernetes** — then how many concurrent users you expect and your use case (chat, RAG, coding, batch). From that it recommends an open-weight model (e.g. Qwen, Mistral, Llama), the right GPU, and a monthly cost estimate, and writes a reviewable `SPEC.md` you can tweak.
- **`llm-build`** generates everything needed to serve it: for **VM** targets, Terraform plus a startup script that installs the NVIDIA driver and serving engine (vLLM / SGLang / Ollama); for **Kubernetes**, plain manifests (a GPU `Deployment`, a `LoadBalancer` Service, and a `Secret`) — each with ready-to-run deploy/destroy scripts.
- **`llm-deploy`** runs the audit, confirms the cost, and provisions it; **`llm-status`** shows the live endpoint; **`llm-destroy`** tears it all down.

**Ten targets, one OpenAI-compatible endpoint:**

- **GPU VM (Terraform):** AWS · Azure · Google Cloud · Oracle Cloud · DigitalOcean · Nebius · Vultr · Scaleway · Lambda Cloud
- **Kubernetes:** CoreWeave (CKS)

Every deployment exposes an **OpenAI-compatible** `/v1` endpoint you can point any client at — including pAiCoder itself.

### Bring your model back into pAiCoder 🔗 *(new)*

The loop closes: once you've deployed an open-source LLM — or if you already run one — register it and build with it.

```
llm-assign      # register a deployed / external OpenAI-compatible LLM + assign it to a role
llm-providers   # list your registered custom providers and the roles they hold
llm-unassign    # remove one and revert its role to the default
```

`llm-assign` auto-detects an endpoint you just deployed (or lets you enter any OpenAI-compatible URL + model), then assigns it to a role — **PLANNER, CODER, AUDITOR, or AUTO_AUDITOR** — persisting it to `~/.paicoder/.env`. Deploy Qwen or Llama on your own GPU, set it as your `CODER`, and you're coding with a model that's fully private, fully yours, and free of per-token cost.

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

# Or point a role at a model you host yourself (set up via `llm-assign`):
# CODER=myqwen
# MYQWEN_BASE_URL=http://<your-endpoint>/v1
# MYQWEN_MODEL=Qwen/Qwen3-Coder-32B
```

**Recommended:** `PLANNER=anthropic`, `CODER=xai` — the best balance of speed, quality, and cost. Prefer a different coder? Set `CODER=meta` (Muse Spark) or `CODER=anthropic`. Want fully local and free? Point a role at **Ollama** — or at your own deployed open-source LLM.

### More in that CHAT panel

A full coding-agent **Project Chat**, **parallel implementation** across a whole spec, code and security **audits** with one-shot fixes, safe **refactors**, and resource checks — all from **`pAiCoder: Open Panel`**. Type `help` to explore, `doctor` to check your setup.

---

## 🧭 Command reference

Type these in the CHAT panel. `help` lists everything available in your build; `doctor` shows which features are enabled.

**Build from an idea**
- `design <description>` — generate a `SPEC.md` · `implement` — build it · `plan` — add a feature
- `audit` · `security` · `refactor` — quality passes with one-shot fixes

**Deploy app infrastructure** — AWS · Azure · Google · Oracle
- `aws-deploy` · `azure-deploy` · `google-deploy` · `oracle-deploy`
- each pairs with `…-status` and `…-destroy`

**Serve open-source LLMs**
- `llm-design` → `llm-build` → `llm-deploy` — size, generate, and launch a serving endpoint (VM or Kubernetes)
- `llm-status` · `llm-destroy` — inspect or tear down a deployment

**Use your own models**
- `llm-assign` · `llm-providers` · `llm-unassign` — register a self-hosted / external LLM and assign it to a role

> Cloud and LLM-deployment commands appear only when enabled in your build — run `doctor` to confirm.

---

## Evaluation License

pAiCoder is free to use for **30 days** from first download. See [LICENSE](https://github.com/dachuyn/paicoder/blob/main/LICENSE) for details.

## Links

- [GitHub](https://github.com/dachuyn/paicoder)
- [Issues](https://github.com/dachuyn/paicoder/issues)
- [Website](https://www.paicoder.com)
- Contact: supports@paicoder.com
