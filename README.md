# pAiCoder — Your Autonomous Engineering Team, on macOS

> **Free 30-day evaluation** · Hand off the build — or write code yourself · Bring your own models — Claude · Grok · GPT · Meta Muse Spark · local Ollama · **or an open-source LLM you host yourself**

pAiCoder gives you **one or more autonomous engineers you can hand a project to** — and a **manager** who takes
your biggest idea, breaks it down, dispatches the pieces to those engineers, and keeps orchestrating until the
whole thing is assembled and audited. You direct them by chat, by voice, or **from
your inbox**; you approve every plan before a line is written; and a deterministic audit gates every deployment.

It is **spec-first** — nothing is built until you have seen and approved `SPEC.md`. It is **model-agnostic** —
assign Claude, Grok, GPT, MuseSpark, a local Ollama model, or your own self-hosted LLM to different roles, so
speed, quality and cost are levers *you* control.

**And when you want to do the work yourself**, the same engine is a spec-first coding assistant in your editor:
ghost-text completion, `design` → `implement`, multi-cloud deployment, LLM hosting, even RTL. That is all
[further down](#-the-coding-assistant--when-you-want-to-drive).

---

## 🚀 Two minutes to your first hand-off

```
manager-deploy            # 1. start Aria, the manager
engineer-deploy Ada       # 2. start your engineers — TWO is the sweet spot
engineer-deploy Ava
manager-recruit all       # 3. Aria adopts them — AFTER they are running
engineer-status           # 4. who is up, and their private panel URLs
```

Each command prints a `127.0.0.1` URL protected by a one-time token. Open Aria's, describe what you
want, and she plans it, splits it into components, and dispatches them. Open an engineer's and you
are talking to her directly. **`/help` in either panel** lists everything they accept.

**No setup needed.** The first `manager-deploy` writes a working manager — and an engineer, if you
have none — and starts them.

> `manager-recruit` adopts the engineers it can *find*, so it goes last. `engineer-deploy all`
> starts the ones on this machine and skips any you have dismissed — name her to bring her back.

**Two engineers is usually right.** They share one LLM quota, so a third mostly competes with the
other two rather than finishing sooner. When many autonomous engineers are needed at the same time, use "/engineer-coder <anthropic|meta|openai|xai>" and/or "/engineer-planner <anthropic|meta|openai|xai>" to assign different LLM providers so that they don't complete on a single provider's LLM quota.

---

## 🤖 Autonomous Engineer — hand off the build, stay in control

An engineer takes a project end to end: `design` → review → `implement` → `audit` → `fix-audit`,
then packages the result. She works in her own directory, on her own port, with her own panel.

**She writes code and never runs it.** Automated passes may read and write files — no shell, no
package installs, no test runs. What she produces is yours to run.

**Talk to her however suits you:**

- **her panel** — chat, watch the task list, answer questions, enter secrets safely;
- **email** — put the command in the SUBJECT as `/<command>(<argument>)`, for example
  `/new-project(url-shortener)` or `/zip-project()`. She replies with progress and artifacts, so you
  can start work from a phone and read the result later.

**Several at once, each on her own panel.** Open as many as you like in one browser — each holds her
own session.

---

## 🧑‍💼 Autonomous Manager — one idea, a whole system

Aria takes a description, asks a planner to split it into components, writes a portfolio `SPEC.md`,
and sends it to you for review. On approval she dispatches each component to a free engineer,
collects the artifacts, assembles them into one tree and audits the result.

Pieces with no free engineer are **queued** and go out as soon as one finishes. She reaches local
engineers directly, and remote ones by email.

**Start a BIG project with the manager, not an engineer.** An engineer plans one SPEC in a single
pass — directory tree, file names and phases all at once — and that gets thin when the project is
large or spans several stacks. Aria splits it first, so each engineer plans a component she can hold
in her head. A small, single-stack project is fine handed straight to an engineer.

Type **`/help`** in her panel — or an engineer's — for everything they accept.

`manager-status` · `manager-roster` · `manager-inbox` — what she is doing, who she has, what arrived.
`manager-design` reconfigures her; it is not needed to start.

> **Both ship DORMANT.** Nothing runs until you deploy it, and everything stays on `127.0.0.1`.
> Full details: `agent/manager/README.md` and `agent/engineer/README.md`.

---

## 📋 Common workflows

Eight things people actually do, start to finish. Commands are typed in the pAiCoder panel
(`Cmd+Shift+P` → **pAiCoder: Open Panel (REPL / Chat)**) unless a step says otherwise.

### 1 · Install the extension

```bash
git clone <your pAiCoder checkout> && cd coding-agent-v16
./build-binary.sh              # builds dist/pAiCoder (Nuitka, 3–5 min)
./install-vscode-extension.sh  # installs the VS Code extension
```

Reload VS Code. `Cmd+Shift+P` → type `pAiCoder` — you should see nine commands.

### 2 · Add or change your API keys

`Cmd+Shift+P` → **pAiCoder: Setup — Configure API Keys & Roles**.

One place for all of them, and for which model plays which ROLE (planner, coder, auditor). Keys are
written to `~/.paicoder/.env` and never leave your machine. In the panel, `llm-providers` lists what
is registered and `llm-status` shows the current assignment.

### 3 · Your first project, from a design

**From the Explorer:** right-click an architecture diagram, a screenshot or a written brief →
**pAiCoder: Load Design from this File**.

**Or in the panel:**

```
load-design ./docs/architecture.png
load-design(claude) ./docs/architecture.png    # Claude Vision — better on images
```

pAiCoder reads the design, classifies the stack, writes `SPEC.md`, and shows it for review before
anything is built. Approve, and it implements against that spec.

### 4 · Drive it yourself — the coding assistant

Open the panel and talk to it. It reads your workspace, edits files and runs commands, asking before
each write unless `AUTO_APPROVE=true` is set in `~/.paicoder/.env`.

```
implement SPEC.md          build what the spec describes
audit-code                 what is wrong with this codebase
fix-audit                  fix what the audit found
doctor                     health check — providers, tools, config
```

### 5 · Hand a whole project to Ada — the autonomous engineer

```
engineer-design       one wizard: her name, channels, contacts, safety
engineer-deploy       starts her and prints her web panel URL
engineer-status       running? her URL, mode, budgets
engineer-stop         kill switch
```

Open her URL. Give her a project in her panel and she plans, builds, audits and fixes it on her own,
reporting as she goes. `/help` in her panel lists what she understands.

### 6 · A bigger system — Aria and a team of engineers

```
manager-design        configure Aria (identity, channels, the engineers she manages)
manager-deploy        starts her and prints her panel URL
manager-recruit --all enrol the engineers on this machine
manager-status        running? her URL and current project
```

Give Aria one idea in her panel. She splits it into tech-stack sub-projects, sends each to an
engineer, collects the artifacts and assembles them. `/status` shows every component and who holds
it; `/audit-code` and `/fix-code` work on the assembled tree.

**One engineer, one transport.** An engineer configured with email is not recruited locally — that
is what stops duplicate requests and duplicate deliveries.

### 7 · Serve your own model

```
llm-design      describe users, budget and latency → a serving SPEC
llm-build       generate the GPU-VM IaC and startup script
llm-deploy      provision it (audit-gated; this one bills)
llm-status      endpoint URL and IP
llm-destroy     tear it down
llm-assign      point a ROLE at the deployed model
```

### 8 · Hardware — SystemVerilog

```
verilog-design    an HDL SPEC from a description
verilog-build     generate the RTL
```

**Off by default.** Enable `hdl_design.enable_verilog` in `agent/config.py` first; the commands tell
you so if it is not.

---

## 🧹 Housekeeping

```
purge-logs 30            delete logs older than 30 days (projects untouched)
purge-logs 30 --dry-run  show what would go, delete nothing
reset-system soft        the agents forget their work — configs, .env, projects all stay
reset-system agents      the agents are REMOVED; pAiCoder is the coding agent it started as
reset-system hard        agents, and the project registry too
```

**`.env` and every project FILE survive all three resets.** Each asks you to type `I understand`
three times, and refuses while an agent is running.

## 🧠 Models — including local ones

Set these in `~/.paicoder/.env`. Roles are assigned separately, so a fast local model can code while
a stronger one reviews.

```bash
ANTHROPIC_MODEL=claude-opus-5
XAI_MODEL=grok-4.6
OPENAI_MODEL=gpt-5.6-luna
META_MODEL=muse-spark-1.2-contributor
OLLAMA_MODEL=muse-glimmer:30b-mlx      # local, via Ollama
```

**Local models via Ollama.** Install Ollama, pull a model, name it above — chat, streaming and tool
calling work with no further setup:

```bash
ollama pull muse-glimmer               # Meta's open-source agentic model, ~18 GB quantized
```

Use **`muse-glimmer:30b-mlx`** on Apple Silicon — the same model on Ollama's MLX engine.
`llama3.1:8b` is the smaller default. Ollama is expected at `http://localhost:11434`.

**Local vision.** `muse-glimmer` reads images, so **`load-design` works entirely on your machine** —
drop in an architecture diagram and it never leaves the network. That matters when privacy outranks
raw capability, which for many teams it does. JPEG, PNG and WebP; convert a GIF first.

Models without vision (`llama3.1`, most coder models) still handle text and tools — a diagram is
simply skipped, with a note. `load-design` images also work with Anthropic, OpenAI, xAI, Meta, and
any `llm-assign` endpoint.

**Changing a model, live.** `set-anthropic-model`, `set-xai-model`, `set-openai-model` and
`set-meta-model` take effect in the REPL immediately — no restart.

A running engineer or manager is a **separate process**, so those do not reach her. Change hers from
her own panel instead:

```
/engineer-coder meta        # in an engineer's panel — her CODER, right now
/engineer-planner openai    # her PLANNER (writes SPEC.md and the phases)
/manager-planner anthropic  # in Aria's panel — the planner that splits a portfolio
```

Each affects **only that engineer or manager**, takes effect on her next call, and lasts **until she
restarts** — nothing is written to your `.env`. Ideal for trying a model on one engineer without
disturbing the others. To make a change permanent, edit `~/.paicoder/.env`.

**A short command palette.** `Shift+Cmd+P` → "pAiCoder" lists the nine commands you actually reach
for from there — the toggles, `Open Panel`, `Setup`, `Checkpoint`, `Load Design from this File` and
`Download / Update Binary`. The rest are terminal-CLI commands and stay hidden. Nothing is removed;
set `show_vscode_menus: True` in `agent/config.py` to list them all again.

**A short REPL `help`.** The provider-key and model setters (`set-anthropic-key`,
`set-openai-model`, …) and the `parallel*` family are hidden from `help`, because the VS Code panel
and the TUI config screen already do all of it — and eight one-per-provider setters grow the list
with every provider added. **The commands still work when you type them.** Set
`agent.show_repl_advanced: True`, or `PAICODER_REPL_ADVANCED=on`, to list them again. `setup` is
the one entry point that replaces all eight, and every `llm*` command stays listed.

**Big codebases.** pAiCoder reads up to **400,000 characters** of your workspace into an audit or a
design pass — enough for a multi-component project whole. Raise or lower it for your setup:

```bash
PAICODER_CONTEXT_BUDGET=1200000   # a large monorepo on a model with a big window
PAICODER_MAX_FILE_CHARS=300000    # one very large generated file
```

Lower it if you run a small local model — an 8K-token window holds roughly 32,000 characters, and
overflowing it fails rather than costing money.

**Any other model — `llm-assign`.** Register a self-hosted or external OpenAI-compatible endpoint and
point a role at it:

```bash
CUSTOM_PROVIDERS=myllm
MYLLM_BASE_URL=http://your-endpoint/v1
MYLLM_MODEL=your-model
```

Then `llm-assign` → choose the role. `llm-providers` lists what is registered; `llm-unassign` undoes
it.

**Want to host one yourself?** `llm-design` → `llm-build` → `llm-deploy` sizes, generates and launches
a serving endpoint — twelve clouds as a GPU VM, six as managed Kubernetes — then `llm-assign` points
pAiCoder at it.

---

## 🧰 The coding assistant — when you want to drive

Everything above is the team working for you. The rest of this page is pAiCoder as a **spec-first coding
assistant in your editor** — the same engine, driven by you, one command at a time. The engineer and the manager
run *these* commands on your behalf, so anything here is also something you can ask them to do.

### Quick Start — two minutes to your first win (solo mode)

1. **Install** the extension.
2. **Add an API key** — `Cmd+Shift+P` → **`pAiCoder: Setup`** → paste an Anthropic, xAI, OpenAI, or Meta key. (You can add more later and assign them by role.)
3. **Open that CHAT panel** — `Cmd+Shift+P` → **`pAiCoder: Open Panel (REPL / CHAT)`**. This is your command center: type a command, or just chat with the agent.
4. **Pick a first win:**

| You want to… | Do this |
|---|---|
| ✍️ **Write code faster** | Open a Python file, write a docstring, press **Tab** to accept the ghost-text implementation. |
| 🧱 **Build from an idea** | In that CHAT panel: `design a REST API for a todo app with auth` → review **SPEC.md** → `implement`. |
| ☁️ **Deploy infrastructure** | right-click your diagram in the Explorer → **`pAiCoder: Load Design from this File`** → review → `aws-deploy` (or `azure-deploy`, `google-deploy`, `oracle-deploy`). |
| 🤖 **Serve an open-source LLM** | In that CHAT panel: `llm-design` → pick **VM or Kubernetes** → answer a couple of questions → `llm-build` → `llm-deploy`. |
| 🔗 **Code with your own model** | After deploying (or if you already run one): `llm-assign` → point pAiCoder's **CODER** role at your endpoint. |
| 🔧 **Design hardware (RTL)** | In that CHAT panel: `verilog-design` → answer a few questions → review the hardware **SPEC.md** → `verilog-build` writes modern SystemVerilog + a testbench for your own sim/synth flow. |

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

### One idea, twelve stacks 🌐

Describe what you want — pAiCoder picks the language that fits, or you just name it (*"an iPhone game in Swift,"* *"a Go CLI,"* *"a Spring Boot API"*). It recognizes the stack from your description and **tells you what it chose**, then scaffolds a **modern, production-shaped project** — a package-by-feature layout, an adapter layer for external systems, idiomatic tests in that language's own framework, and an explicit **`DEPLOYMENT.md`**. Not a toy scaffold you outgrow in a week — a structure built to scale to a real project.

| Language | Great for | Tests | Ship it |
|---|---|---|---|
| 🐍 **Python** | data & ETL pipelines, ML/AI, backends, automation, glue | pytest | wheel / container |
| 🍎 **Swift / SwiftUI** | native iOS · iPhone · iPad · macOS apps & games | swift-testing | App Store · TestFlight · binary |
| 🟦 **TypeScript** | Node.js services, CLIs, tooling | vitest | process manager / container |
| 💜 **C# / .NET** | Windows & cross-platform services, Web APIs | xUnit | `dotnet publish` |
| ☕ **Java / Spring Boot** | JVM services & REST APIs | JUnit 5 | bootJar / container |
| 🐹 **Go** | services, CLIs, single static binaries | go test | cross-compiled binary |
| 🦀 **Rust** | systems, performance-critical, memory-safe | cargo test | cross-compiled binary |
| ⚙️ **C++** | high-performance & embedded | GoogleTest | host binary · **flash to device** |
| 🟪 **Kotlin** | JVM services & Android | Kotest | shadowJar / container |
| 🔴 **Scala** | JVM, functional, data-heavy | MUnit | sbt assembly |
| 🔵 **F# / .NET** | functional-first .NET (records, unions) | Expecto | `dotnet publish` |
| ⚛️ **React** | browser front-ends (TypeScript + Vite) | Vitest + jsdom | static `dist/` — any host or CDN |

**Building a full-stack app?** React and the service behind it are two components — pAiCoder builds
each in the stack that suits it and keeps the type contract between them consistent.

Every project is designed the same spec-first way — you approve the `SPEC.md` before a line is written — and audited the same way, in whichever language fits the job. Not sure which stack? Just describe the project and let pAiCoder choose; name a language explicitly and it honors your call.

### Inline & docstring completion

Ghost-text suggestions as you type in **any language**, powered by *your* chosen model. Write a docstring and let pAiCoder fill in the function.

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
- **`llm-build`** generates everything needed to serve it: for **VM** targets, Terraform plus a startup script that installs the NVIDIA driver and serving engine (vLLM / SGLang / Ollama); for **Kubernetes**, plain manifests (a GPU `Deployment`, a `LoadBalancer` Service, and a `Secret`) tailored to your provider's GPU classes and node pools — each with ready-to-run deploy/destroy scripts.
- **`llm-deploy`** runs the audit, confirms the cost, and provisions it; **`llm-status`** shows the live endpoint; **`llm-destroy`** tears it all down.

**Twelve targets, one OpenAI-compatible endpoint:**

- **GPU VM (Terraform):** AWS · Azure · Google Cloud · Oracle Cloud · DigitalOcean · Nebius · Vultr · Scaleway · Lambda Cloud · Crusoe · Hyperstack · CoreWeave
- **Managed Kubernetes:** AWS **EKS** · Google **GKE** · Azure **AKS** · Oracle **OKE** · DigitalOcean **DOKS** · CoreWeave **CKS**

Pick Kubernetes on any of those six and you get plain manifests for that provider — the right GPU node
selector, the right cluster CLI, the right node-pool commands — not a generic template you have to
translate.

Every deployment exposes an **OpenAI-compatible** `/v1` endpoint you can point any client at — including pAiCoder itself.

### Bring your model back into pAiCoder 🔗 *(new)*

The loop closes: once you've deployed an open-source LLM — or if you already run one — register it and build with it.

```
llm-assign      # register a deployed / external OpenAI-compatible LLM + assign it to a role
llm-providers   # list your registered custom providers and the roles they hold
llm-unassign    # remove one and revert its role to the default
```

`llm-assign` auto-detects an endpoint you just deployed (or lets you enter any OpenAI-compatible URL + model), then assigns it to a role — **PLANNER, CODER, AUDITOR, or AUTO_AUDITOR** — persisting it to `~/.paicoder/.env`. Deploy Qwen or Llama on your own GPU, set it as your `CODER`, and you're coding with a model that's fully private, fully yours, and free of per-token cost.

### Design hardware, too — idea → synthesizable SystemVerilog 🔧 *(new)*

Not just software. Describe a hardware block and pAiCoder turns it into a reviewable **hardware `SPEC.md`**, then into **modern, synthesizable SystemVerilog** with a self-checking testbench — ready for your own simulation and synthesis flow.

```
verilog-design  →  verilog-build
```

- **`verilog-design`** runs a short wizard — target device (**AMD**, **Intel**, **Lattice**, or portable), clock + reset scheme, and one of **13 hardware block types**:
  - **Memory** — FIFO, RAM, direct-mapped cache, on-chip SRAM controller
  - **Compute** — ALU, SIMD engine, systolic MAC / GEMM tile, DSP datapath
  - **Control & glue** — FSM controller, arbiter, AXI4-Lite / AXI4-Stream / APB / Wishbone SoC peripheral
  - **Reference blocks** — a SHA-256-style hash core and an educational RV32I CPU subset

  From your answers it writes a **deterministic `SPEC.md`** that pins every module's ports, parameters, clocking, and interface contracts up front — plus a rough resource + timing estimate so you catch an over-budget design *before* you build it.
- **`verilog-build`** generates the RTL to that spec: **IEEE-1800 SystemVerilog**, synthesizable subset — `always_ff` / `always_comb`, `logic`-typed, `` `default_nettype none ``, no inferred latches, clean reset / CDC discipline — plus a **self-checking testbench**, a `README`, and an exact, **device-aware `DEPLOYMENT.md`** with the precise lint / simulate / synthesize commands for your part. A fast, read-only static audit flags anti-patterns before you ever open a tool.

**You verify — on your toolchain, your way.** pAiCoder writes clean, review-ready RTL and hands you the exact commands; it never runs a simulator or synthesizer itself, so nothing surprising happens to your environment. Lint with **Verilator** or **Verible**, simulate with **Verilator** / **Icarus**, synthesize with **Vivado**, **Quartus**, or **Yosys + nextpnr** — the generated `DEPLOYMENT.md` spells out each command for your device.

> **Honestly scoped.** Each block is bounded to what a generator can produce *correctly*. The two reference blocks say so up front, right at the top of their spec: the hash core is a **learning implementation** to check against the standard test vectors (not production crypto, not side-channel hardened), and the RISC-V core is an **educational RV32I subset** (not a conformant CPU — no CSRs, traps, or pipeline). No block oversells what it is.

> `verilog-design` writes the spec, then *offers* to build (`[y/N]`) — nothing is generated until you say so.

### Your choice, your cost

Most AI coding tools lock you into one model. pAiCoder lets you assign providers by role:

```bash
# ~/.paicoder/.env
PLANNER=anthropic                  # deep reasoning — design, spec, orchestration
ANTHROPIC_MODEL=claude-opus-5
CODER=openai                       # implementation + inline completion
OPENAI_MODEL=gpt-5.6-luna
AUDITOR=anthropic                  # an independent second opinion on audits
META_MODEL=muse-spark-1.2-contributor   # key: MODEL_API_KEY (from dev.meta.ai)
OLLAMA_MODEL=muse-glimmer:30b-mlx  # local — reads diagrams too (see below)

# Or point a role at a model you host yourself (set up via `llm-assign`):
# CODER=myqwen
# MYQWEN_BASE_URL=http://<your-endpoint>/v1
# MYQWEN_MODEL=Qwen/Qwen3-Coder-32B
```

**Recommended:** `PLANNER=anthropic` (claude-opus-5) and `CODER=openai` (gpt-5.6-luna) — planning quality matters most, and this pairing has been the most reliable in practice. `CODER=meta` (muse-spark-1.2-contributor) is a strong alternative and reads architecture diagrams. Want fully local and free? Point a role at **Ollama** — or at your own deployed open-source LLM.

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
- `llm-design` → `llm-build` → `llm-deploy` — size, generate, and launch a serving endpoint
- twelve clouds as a **GPU VM**, six of them as **managed Kubernetes** (EKS · GKE · AKS · OKE · DOKS · CKS)
- `llm-status` · `llm-destroy` — inspect or tear down a deployment

**Use your own models**
- `llm-assign` · `llm-providers` · `llm-unassign` — register a self-hosted / external LLM and assign it to a role

**Design hardware (SystemVerilog)**
- `verilog-design` → `verilog-build` — idea → reviewable hardware `SPEC.md` → modern synthesizable SystemVerilog + a self-checking testbench, with device-aware lint/sim/synth commands you run yourself

**Hand work to an autonomous engineer, or a manager**
- `engineer-deploy` · `engineer-status` · `engineer-inbox` · `engineer-stop` — one engineer, or several by name
- `manager-deploy` · `manager-status` · `manager-roster` · `manager-purge` — a manager who plans a whole product and dispatches the pieces
- `engineer-design` · `manager-design` — change any of it; neither is needed to start
- In their own panels: `/engineer-coder <provider>` · `/engineer-planner <provider>` · `/manager-planner <provider>` — swap a model live, for that one, until she restarts

> Cloud, LLM-deployment, hardware-design, engineer and manager commands appear only when enabled in your build — run `doctor` to confirm.

---

## Evaluation License

pAiCoder is free to use for **30 days** from first download. See [LICENSE](https://github.com/dachuyn/paicoder/blob/main/LICENSE) for details.

## Links

- [GitHub](https://github.com/dachuyn/paicoder)
- [Issues](https://github.com/dachuyn/paicoder/issues)
- [Website](https://www.paicoder.com)
- Contact: supports@paicoder.com

---

