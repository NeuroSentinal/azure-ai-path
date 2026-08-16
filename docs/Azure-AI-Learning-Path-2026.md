# Azure AI Engineer Learning Path — 2026 Edition

**Learner:** Experienced Systems Administrator → AI/Cloud Solutions Architect, targeting **AI Engineering / Forward-Deployed Engineer (FDE)** roles
**Commitment:** 15+ hrs/week · **Python:** starting from zero (ramp built in) · **Budget target:** $0 Azure spend for classic services, low-single-digit dollars for GenAI tokens, exam fees minimized
**Plan generated:** August 15, 2026 · All facts verified against official Microsoft pages on this date

---

## ⚠ READ FIRST — What changed in 2026 (this plan is corrected for it)

The original three-exam plan (AI-900 → AI-102 → AI-103) is no longer executable. Microsoft overhauled its entire AI certification line effective **June 30, 2026**:

| Original plan | Status (verified Aug 15, 2026) | What replaces it |
|---|---|---|
| **AI-900** Azure AI Fundamentals | **RETIRED June 30, 2026.** [Exam page](https://learn.microsoft.com/en-us/credentials/certifications/exams/ai-900/) | **AI-901** — same *Azure AI Fundamentals* certification, redesigned around Microsoft Foundry |
| **AI-102** Azure AI Engineer Associate | **RETIRED June 30, 2026** — exam, certification, *and* its renewal assessment. Banner on the [exam page](https://learn.microsoft.com/en-us/credentials/certifications/exams/ai-102/): "This certification and the renewal assessment are retired." | **AI-103** — new certification: *Azure AI Apps and Agents Developer Associate* |
| **AI-103** Develop AI apps and agents on Azure | **LIVE.** Beta April 2026, GA June 2026. [Study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-103) | This is now your one associate-level exam |

Three consequences that reshape the plan:

- **Your path is now two exams, not three: AI-901 → AI-103.** The AI-102 skill set did not disappear — vision, text analysis, and information extraction survive as three 10–15% domains inside AI-103. You still learn the classic services; you just take one associate exam instead of two, and save ~US$165 doing it.
- **Everything is Foundry-first and Python-first.** AI-901 is 55–60% "Implement AI solutions by using Microsoft Foundry," and its study guide expects Python syntax familiarity *at the fundamentals level*. An official MCT statement confirms the AI-103 labs and exam are [Python only](https://learn.microsoft.com/en-us/answers/questions/5905251/ai-103t00-a-develop-ai-apps-and-agents-on-azure-do). Your Python ramp is Phase 0 for a reason.
- **Two free-lab pillars from the original brief are dead.** The Microsoft Learn embedded 4-hour sandbox was retired (~Oct 2025): ["Sandboxes are no longer available"](https://learn.microsoft.com/en-us/training/support/faq?pivots=sandbox). GitHub Models (free inference API) was [fully retired July 30, 2026](https://docs.github.com/en/github-models). Section 7 rebuilds the zero-cost methodology around what actually exists today: Applied Skills lab environments, F0 free tiers, Foundry Local, containers on your own hardware, Codespaces, and a hard-stop trial subscription.

Also relevant: the classic Applied Skills credentials (Vision, Language/NLP, Document Intelligence, Knowledge Mining, Azure OpenAI) were **all retired between June 2025 and July 2026** and replaced by a new Foundry/agents-focused catalog — the new ladder is built into Phase 3. Older blog posts and Udemy courses referencing the sandbox, AI-102, or those Applied Skills are describing a world that no longer exists. Trust the study guides and this document's verified links.

---

## 0 · Start here — how this kit works

Three artifacts, one rule each:

| Artifact | What it owns | When you open it |
|---|---|---|
| **This playbook** | Strategy and everything from Week 3 onward: the exam map (§1), Phases 1–4 taught in full (§3–6), the zero-cost playbook (§7), supplements (§8), the FDE career layer (§9), the master schedule (§10), the homelab & local kit (Appendix A), and the link registry (Appendix B) | Sunday planning every week; then daily through Phases 1–4 |
| **Phase-0-Python-Curriculum** (`.md` / `.html`) | Weeks 1–2, day by day — the Python course itself, fully taught | Every study session Aug 17–30 |
| **Cowork sidebar artifacts** | Live rendered copies of both documents | Anytime — they are kept in sync with the folder copies |

**Precedence:** for Weeks 1–2 the curriculum is authoritative and this playbook's §2 is only its summary. For everything else, this playbook is authoritative. If any two of these documents ever disagree, that is a defect to report, not a puzzle to solve.

**The reading rule this kit is built on:** each phase section *teaches* — concepts first, then exact steps, then the exam angle, then measurable "good." External links are enrichment and lab entry points, never load-bearing; you should never have to leave a section to find out what you were supposed to learn from it.

**The operating loop, every topic from Week 3 on:** (1) read the phase section here — it is the content, not a pointer to content; (2) do the named lab hands-on; (3) Thursday lens: the named Savill video or architecture doc, asking "how would I run this at work — identity, network, cost?"; (4) one paragraph of notes and a commit. Reading without labbing doesn't count; labbing without the architecture pass wastes your sysadmin advantage.

### Where you are right now — weekend of Aug 16–17, the setup checklist and nothing else

- [ ] Homebrew toolchain: `brew install python@3.12 uv git azure-cli`, then `brew tap azure/azd && brew install azd`
- [ ] Docker Desktop for Mac installed (or plan to use the homelab per Appendix A)
- [ ] Foundry Local working: `brew tap microsoft/foundrylocal && brew install foundrylocal`, then `foundry model list` and `foundry chat phi-4-mini` *(June-2026 CLI — the older `foundry model run` syntax is gone; Appendix A.6 has the full command map)*
- [ ] The tracker repo created and pushed — **full walkthrough in §0.1 below** (account, `gh` auth, structure, first commit, the daily habit)
- [ ] [Exercism](https://exercism.org/tracks/python) account registered on the Python track
- [ ] [Virtual Training Days](https://www.microsoft.com/en-us/events/category/microsoft-virtual-training-days) checked tonight for an AI-fundamentals event before ~Sep 8 — §3.4 explains why the voucher timing works this way
- [ ] **No Azure signup yet.** That is deliberately Day 1 of Week 3 (Mon Aug 31) — §3.1 explains the 30-day clock

Then Monday evening, Aug 17: open the curriculum at **Day 1** and start typing. That's the whole instruction.

### 0.1 The tracker repo — exact setup (~20 minutes, once)

**Why this repo exists.** Three jobs: (1) it is your **progress tracker** — the gate checklists live in the Markdown copies, and every ticked box is a commit; (2) it is where all your path work accumulates — Phase 0 code, lab notes, the Phase 2 hardening notes; (3) it is the **portfolio signal** — 16 weeks of steady commits is the activity graph an AI-engineering hiring manager actually scrolls, and FDE screeners in particular look for evidence of consistent shipping. The capstone deliberately gets its **own separate repo** in Week 12, because it's a product, not a notebook.

**Step 1 — GitHub account.** Use a **personal** account, not anything tied to the HYLIFE tenant — this repo follows you between jobs, and your cert transcript, Codespaces quota, and portfolio all hang off it. If you don't have one: [github.com/signup](https://github.com/signup), then turn on 2FA (Settings → Password and authentication).

**Step 2 — install and authenticate the GitHub CLI.** `gh` wires up git credentials so you never juggle tokens or SSH keys by hand:

```bash
brew install gh
gh auth login
```

Answer the prompts exactly: **GitHub.com** → **HTTPS** → **Yes** (authenticate Git with your GitHub credentials) → **Login with a web browser**, then type the one-time code it prints into the browser window it opens. Verify:

```bash
gh auth status
```

```text
github.com
  ✓ Logged in to github.com account <your-username> (keyring)
  ✓ Git operations protocol: https
```

**Step 3 — tell git who you are** (first time on this Mac):

```bash
git config --global user.name  "Shawn Vermette"
git config --global user.email "<the email on your GitHub account>"
git config --global init.defaultBranch main
```

**Watch out:** if you'd rather not expose your real email in public commits, GitHub gives you a no-reply address — Settings → Emails → tick *Keep my email addresses private*, then use the `<id>+<username>@users.noreply.github.com` address it shows as your `user.email`. **If you hit this:** a push rejected with `GH007: Your push would publish a private email address` means exactly that mismatch — switch `user.email` to the no-reply address, re-commit (`git commit --amend --reset-author`), and push again.

**Step 4 — create the folder, the structure, and the first commit:**

```bash
mkdir -p ~/code/azure-ai-path && cd ~/code/azure-ai-path
git init
mkdir -p docs python-ramp notes hardening

# the two documents come in from the Cowork project folder (quotes matter — the folder name has spaces)
cp "/Users/Shawn.Vermette/Ai Engineer Learning Path/Azure-AI-Learning-Path-2026.md"  docs/
cp "/Users/Shawn.Vermette/Ai Engineer Learning Path/Phase-0-Python-Curriculum.md"   docs/

cat > README.md <<'EOF'
# Azure AI Path — tracker

Working repo for my AI-901 → AI-103 certification path (Aug–Dec 2026).

- `docs/` — the playbook + Phase 0 curriculum; gate checkboxes get ticked here
- `python-ramp/` — Phase 0 code (Weeks 1–2)
- `notes/` — one short note per lab/topic from Week 3 on
- `hardening/` — enterprise hardening designs (Phase 2+)

Capstone lives in its own repo (created Week 12). Progress = the commit history.
EOF

cat > .gitignore <<'EOF'
.venv/
.env
__pycache__/
*.pyc
logs/
transcripts/
.DS_Store
EOF

git add -A
git commit -m "Init: Azure AI path tracker + docs"
```

The `.gitignore` matters more than it looks: `.env` is where Week 2 puts secrets and it must never be committed; `.DS_Store` is macOS Finder noise; `.venv/` is rebuildable and huge. After any `git add -A`, glance at `git status` — if you ever see `.env` staged, stop and fix the ignore before committing.

**Step 5 — publish it:**

```bash
gh repo create azure-ai-path --public --source=. --push
```

```text
✓ Created repository <your-username>/azure-ai-path on GitHub
✓ Pushed commits to https://github.com/<your-username>/azure-ai-path.git
```

`gh repo view --web` opens it in the browser to confirm. **Public vs private:** public, deliberately — nothing sensitive can land in it (that's what the ignore file enforces), and a visible body of work is the point. If that ever feels wrong, `gh repo edit --visibility private` flips it in one command.

**Step 6 — the habit that makes it a tracker.** End of every study session, three commands:

```bash
git add -A
git commit -m "Day 3: lists/slicing done + day3.py"
git push
```

Tick the gate checkboxes by editing the Markdown in `docs/` (VS Code renders the boxes clickable in preview mode: `Cmd-Shift-V`) — a ticked box plus a commit is a timestamped record of the gate you passed. Write commit messages like log lines ("Week 5: CLU model trained, hardening note #1"), not "update."

**How the copies relate (so nothing drifts):** the repo's `docs/` copies are **yours** — tick, annotate, scribble. The Cowork project folder and the sidebar artifacts stay the clean reference copies, and they're what Claude updates. If the documents get revised later, you'll be told which file changed — re-copy that one file into `docs/` and carry your ticks forward; don't edit the reference copies in the Cowork folder by hand.

**Where the curriculum work goes:** all Phase 0 code paths in the curriculum live under `~/code/azure-ai-path/python-ramp/` — the curriculum's commands use that path throughout, so Day 1 starts inside the repo and your first Python file is also your first green square.


---

## 1. The 2026 certification map

| | **Exam AI-901** | **Exam AI-103** |
|---|---|---|
| Certification | Microsoft Certified: **Azure AI Fundamentals** (never expires) | Microsoft Certified: **Azure AI Apps and Agents Developer Associate** (annual free online renewal) |
| Domains (weight) | Identify AI concepts and capabilities **40–45%** · Implement AI solutions by using Microsoft Foundry **55–60%** | Plan and manage an Azure AI solution **25–30%** · Implement generative AI and agentic solutions **30–35%** · Computer vision **10–15%** · Text analysis **10–15%** · Information extraction **10–15%** |
| Skills measured as of | April 15, 2026 | April 16, 2026 |
| Format | Online proctored (Pearson VUE) or test center; passing score 700 | Same; **120 minutes**; passing score 700 |
| List price | US$99 (CAD shown at scheduling; ~C$130 range) | US$165 (CAD shown at scheduling; ~C$220 range) |
| Free practice assessment | [AI Skills Navigator](https://aiskillsnavigator.microsoft.com/credentials/cert-83587e0a0754cfee561ade3e27d9fa1cdaf15ae03be52d2413b2b858d1b4eda4) | [AI Skills Navigator](https://aiskillsnavigator.microsoft.com/credentials/cert-3fb198f57997226a824aa5f52a1a22af9a4597941b2288ed39371c7a9e6bd7c9) |
| Study guide | [aka.ms/AI901-StudyGuide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-901) | [aka.ms/AI103-StudyGuide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-103) |
| Official course | Self-paced paths on the [exam page](https://learn.microsoft.com/en-us/credentials/certifications/exams/ai-901/) | [AI-103T00: Develop AI apps and agents on Azure](https://learn.microsoft.com/en-us/training/courses/ai-103t00) (4-day ILT; self-paced equivalents free) |

**After AI-103 (your growth path):** the new expert tier — **Microsoft Certified: [Multi-Agent AI Solutions Expert](https://learn.microsoft.com/en-us/credentials/certifications/multi-agent-ai-solutions-expert/)** (beta) — requires the AI-103 certification plus Exam **AI-500** *Designing and Implementing Multi-Agent AI Solutions*. It maps directly onto multi-agent orchestration work and is the natural 2027 target for an AI Engineer/FDE trajectory. Park it; know it exists.

**Renewals:** associate certs renew **free** — an unproctored, open-book online assessment on Microsoft Learn, unlimited attempts, available in a 6-month window before expiry ([policy](https://learn.microsoft.com/en-us/credentials/certifications/renew-your-microsoft-certification)). Fundamentals certs never expire. Note the cautionary tale: AI-102 holders lost their renewal path entirely when the cert retired — plan to keep certs current in the year you earn them.

### Why this order (AI-901 → bridge → AI-103)

1. **AI-901 is no longer a trivia exam — it's a guided on-ramp to the exact surface AI-103 tests.** At 55–60% "implement with Foundry," preparing for it forces the portal, project model, model deployments, and first SDK calls. Passing it two weeks in gives you a credential, exam-process reps (proctoring, question styles), and momentum — for US$99 or less.
2. **The bridge phase (old AI-102 muscle) is 30–45% of AI-103.** Vision + text analysis + information extraction are worth 30–45% combined, and "plan and manage" leans on knowing the classic services. Skipping straight to agents leaves half the exam uncovered — and FDE work is mostly *integrating* these services into real systems.
3. **GenAI + agents last, as the deepest block.** The 30–35% agentic domain plus plan/manage (25–30%) rewards accumulated hands-on maturity: SDK fluency, cost/quota awareness, network/identity hardening. It's also where the portfolio capstone lives.

### Pacing at 15+ hrs/week (16 weeks total)

| Phase | Weeks | Dates (starting Mon Aug 17, 2026) | Outcome |
|---|---|---|---|
| 0 — Python ramp + optional foundations | 1–2 | Aug 17 – Aug 30 | Python working fluency for labs |
| 1 — AI-901 | 3–4 | Aug 31 – Sep 13 | **AI-901 exam ~Sep 15–18** → Azure AI Fundamentals |
| 2 — Applied services bridge | 5–8 | Sep 14 – Oct 11 | Vision/Language/Speech/Doc Intelligence/Search labs done + hardened |
| 3 — GenAI, RAG & agents core | 9–14 | Oct 12 – Nov 22 | Applied Skills ladder + capstone repo |
| 4 — AI-103 closing | 15–16 | Nov 23 – Dec 6 | **AI-103 exam ~Dec 2–6** → Azure AI Apps and Agents Developer Associate |

Realistic for an IT professional at 15 hrs/week: certified by **early December 2026**. If Python clicks fast, Phase 0 can compress to 1 week and everything shifts left; if work explodes, the phases degrade gracefully — each has a hard gate, so slipping a week never means losing the thread. At ~10 hrs/week this same plan runs ~22–24 weeks (certified ~February 2027).

### Suggested weekly cadence (15 hrs)

| Slot | Time | Mode |
|---|---|---|
| Mon evening | 2 hrs | Lab (hands on keyboard) |
| Wed evening | 2 hrs | Lab |
| Thu evening | 1 hr | Savill video / architecture reading — the "lens" pass |
| Sat morning | 4 hrs | Deep lab block (the week's main build) |
| Sun morning | 2 hrs | Review, notes, portfolio commit, **cost-cleanup ritual** (§7.4) |
| Flex | 4 hrs | Practice assessments, Exercism drills, overflow |

The operating loop for every topic, in order: **(1) MS Learn module → (2) hands-on lab from the official repo → (3) Savill or Architecture Center pass ("how would I deploy this at an enterprise: identity, network, cost?") → (4) one paragraph of notes + a commit.** Reading without labbing doesn't count; labbing without the architecture pass wastes your sysadmin advantage.

---

## 2. Phase 0 — Foundations ramp (Weeks 1–2)

> **📘 This section is the map; the course itself is `Phase-0-Python-Curriculum.md` / `.html`.** Every concept below is fully taught there — explanations, code with expected output, worked solutions, error-fix notes, and daily checkpoints. Open the curriculum Monday and work top to bottom; come back here only to see how the two weeks fit the larger plan.

**Goal:** enough Python that no lab in this path is bottlenecked by the language. Core, not optional — both 2026 exams now assume Python, and everything runs free against Foundry Local on your own machine.

### 2.1 The day map (identical to the curriculum)

| Day | Slot | Topic | You build |
|---|---|---|---|
| **Week 1 — Python Foundations** | | *(Aug 17–23)* | |
| 1 | Mon 2h | Running Python, values, strings, f-strings | `day1.py` — F0 quota reporter |
| 2 | Wed 2h | Control flow: if/elif, loops, truthiness, break/continue | `day2.py` — HTTP status classifier + retry simulator |
| 3 | Thu 1h | Lists, tuples, slicing, sorting, unpacking | `day3.py` — confidence-score analysis |
| 4 | Sat 4h | **Functions, modules, dictionaries** — the pivotal day | `day4.py` — fleet health report |
| 5 | Sun 2h | Nested data, comprehensions, sets | `inventory_report.py` (includes a deliberate bug to find) |
| 6–7 | Flex 4h | Files, pathlib, exceptions, tracebacks | `log_triage.py` + the 10 listed Exercism drills |
| **Week 2 — The AI Developer Toolkit** | | *(Aug 24–30)* | |
| 8 | Mon 2h | Virtual environments, uv/pip, `.env` secrets | `check_env.py` + proper project skeleton |
| 9 | Wed 2h | HTTP/REST with httpx, status-code literacy | `raw_chat.py` — call Foundry Local with no SDK |
| 10 | Thu 1h | JSON mastery, defensive response parsing | `inspect_json.py` — recursive structure explorer |
| 11 | Sat 4h | **The OpenAI SDK** — messages, roles, streaming, tool calling | `chat.py` — full streaming chatbot with history |
| 12 | Sun 2h | Classes and async at SDK-reading depth | `ChatSession` class + `async_demo.py` concurrency benchmark |
| 13–14 | Flex 4h | Sysadmin drills (CSV, poller) + capstone | `log_assistant.py` — deterministic aggregation + LLM narration |

The capstone's division of labor — **Python computes the numbers, the model only writes prose about them** — is the single most important architectural idea in the whole phase; it recurs in every RAG and agent system in Phase 3.

### 2.2 Foundry Local — the free playground everything runs against

Installed during weekend setup (Appendix A.6 has the current June-2026 CLI: `foundry model list`, `foundry run <alias>`, `foundry chat <alias>`, `foundry status`). It serves an OpenAI-compatible endpoint on localhost, which is what makes Week 2's SDK work free: iterate locally, then in Phase 1 change only `base_url` and credentials to hit Azure. Don't ask it factual questions — small local models are a practice endpoint, not a knowledge source; the docs are the knowledge source.

### 2.3 [OPTIONAL] Side units — only if the skip-tests say so

- **GenAI concepts primer.** Skip-test: explain in one sentence each — token, embedding, vector similarity, context window, temperature, system prompt, RAG, agent-vs-chatbot, tool calling, hallucination + grounding. Given your Foundry platform work you likely pass; the curriculum also teaches each of these in context as they arise. If several are shaky, one evening with [Microsoft's generative-AI fundamentals modules](https://learn.microsoft.com/en-us/training/browse/?terms=generative%20AI%20fundamentals) — no more.
- **Azure resource-model primer.** For learners without Azure administration exposure (subscriptions → resource groups → resources, ARM at a glance, RBAC scopes, regions/SKUs/quotas). You administer Entra daily — skim only what you don't live in.

### ✅ Phase 0 gate — do not start Phase 1 until:

- [ ] Curriculum Days 1–14 complete, every daily checkpoint honestly ticked
- [ ] `log_triage.py` and the capstone `log_assistant.py` run end to end on generated sample data
- [ ] `chat.py` works against Foundry Local: streaming, history that survives a follow-up question, `/commands`, error handling
- [ ] The 10 Exercism exercises from the Days 6–7 list completed
- [ ] **The curriculum's 90-minute blank-file self-test passed — all 10 items, no references, no AI assistance**
- [ ] Toolchain verified: VS Code + Homebrew Python 3.12/uv/git + Azure CLI + azd + Docker + Foundry Local

---

## 3 · Phase 1 — AI-901: Azure AI Fundamentals, Foundry edition (Weeks 3–4)

**Goal:** pass AI-901 inside two weeks — but treat the exam as the excuse, not the point. AI-901 is the only place in this path where someone hands you a complete, ordered map of the AI vocabulary (tokens, embeddings, grounding, responsible AI) *and* a guided tour of every square inch of the Microsoft Foundry portal you will live in for the next twelve weeks. You are a sysadmin walking into a new tenant: you learn the console before you automate it. That's what these two weeks are.

AI-900 is dead — retired June 30, 2026, along with the cert and its renewal. If a blog, Udemy course, or YouTube video says "AI-900," it predates the Foundry rename and roughly half of its Azure AI Studio screenshots no longer match the portal. AI-901 replaced it with skills measured as of **April 15, 2026**, two domains only, pass mark 700, US$99.

| Domain | Weight | What it really covers |
|---|---|---|
| Identify AI concepts and capabilities | 40–45% | The vocabulary and the mental model: ML types, deep learning, language models, tokens/embeddings, generative AI behavior, the workload categories, and responsible AI |
| Implement AI solutions by using Microsoft Foundry | 55–60% | The portal: projects, model catalog, deployments, playgrounds, Foundry Tools, agents, and the shape of the Python SDK |

Note the split. More than half the exam is *the tool*, not *the theory*. That is unusual for a fundamentals exam and it is why hands-on time in ai.azure.com beats re-reading notes.

---

### 3.1 Week 3, Day 1 — Stand up the subscription and set the money rules

#### What you're actually learning

The Azure free account is three offers stapled together, and confusing them is how people end up with a surprise bill:

1. **US$200 credit, usable for 30 days.** Starts the moment you sign up. Unused credit evaporates on day 31. This is the only "real money" you get.
2. **12 months of free amounts** of ~20 popular services (certain VM hours, blob storage, etc.). Not very relevant to you.
3. **Always-free tiers** of 65+ services — this *is* the relevant one. Every F0 AI service tier (Language, Speech, Vision, Document Intelligence, Translator) and the AI Search Free tier live here. They cost nothing forever, credit or no credit.

The mechanism that makes this zero-risk is the **spending limit**. On a free-trial subscription it is ON by default and cannot be exceeded: when the $200 is gone or day 30 passes, Azure *disables* your paid services rather than charging your card. Your card is on file only for identity verification (a temporary US$1 authorization; prepaid cards are rejected). Nothing bills while the spending limit is on. That's your guarantee.

**The timing trap, and why day 1 of week 3 specifically.** The 30-day credit window is 30 calendar days from signup — it does not stretch. If you sign up today (week 3) it expires around the middle of week 7. Phases 1 and 2 (weeks 3–8) are the *free-tier* phases: F0 services and the Search Free tier, which barely touch the credit. Phase 3 (weeks 9–14) is where you deploy language models, and **there is no free tier for model inference** — but it costs cents, not dollars, if you deploy only nano/mini serverless models. So do not try to "save" the credit for Phase 3; it will be gone regardless. Sign up now, run the free tiers, and around day 30 convert to pay-as-you-go (§7.3 of the main doc) with a budget alert.

**The other reason to convert:** trial subscriptions frequently have **zero quota for model deployments**. You will hit "You have exceeded the token rate limit / no quota available for this model in this region" or find the Deploy button greyed out entirely on a trial sub. That is a subscription-type restriction, not a mistake you made. Converting to pay-as-you-go (which does not itself charge anything) is what unlocks default TPM quota.

#### Do this

1. **Sign up.** azure.microsoft.com → "Start free". Use a Microsoft account you control long-term (this becomes your Entra tenant and your cert transcript identity later). Verify by phone and card. You land in a subscription usually named "Azure subscription 1" — rename it to something like `sub-learn` in the portal (Subscriptions → your sub → Rename) so screenshots and CLI output are unambiguous.

2. **Install the CLI locally on the Mac.** You will use Cloud Shell for labs that demand it, but local is faster and teaches you the auth model:
   ```bash
   brew update && brew install azure-cli
   az version
   az upgrade            # run this monthly; the AI commands move fast
   ```

3. **Log in and pin the context.**
   ```bash
   az login                      # opens a browser; pick the right account
   az account list --output table
   az account set --subscription "sub-learn"
   az account show --output jsonc
   ```
   **Watch out:** if your Microsoft account is a guest in other tenants (extremely likely for you — every vendor demo tenant you've ever been invited to), `az login` may land you in the wrong directory and `az group create` will then fail with an authorization error against a tenant you don't own. Force it: `az login --tenant <tenant-guid>`. Confirm with `az account show --query "{sub:name, tenant:tenantId, user:user.name}"`. On a headless shell or if the browser handoff misbehaves, use `az login --use-device-code`.

4. **Register resource providers.** A brand-new subscription has most providers unregistered; the first `create` of a service type otherwise fails with `MissingSubscriptionRegistration`. Do it once, up front:
   ```bash
   az provider register --namespace Microsoft.CognitiveServices
   az provider register --namespace Microsoft.Search
   az provider register --namespace Microsoft.Storage
   az provider register --namespace Microsoft.KeyVault
   az provider show -n Microsoft.CognitiveServices --query registrationState -o tsv
   ```
   Registration takes 1–3 minutes; poll until it says `Registered`.

5. **Create your resource-group skeleton.** One RG per workstream, because `az group delete` is your entire teardown story and you never want a delete to be ambiguous:
   ```bash
   az group create -n rg-learn-ai901  -l eastus2
   az group create -n rg-learn-lang   -l eastus
   az group create -n rg-learn-vision -l eastus
   az group create -n rg-learn-docs   -l eastus
   az group create -n rg-learn-search -l eastus
   az group create -n rg-learn-genai  -l eastus2
   ```
   Region choice matters more in Azure AI than in core Azure: model availability, Content Understanding availability, and Document Intelligence feature parity are all region-gated. **East US** and **East US 2** have the broadest AI coverage; **Sweden Central** and **West US 3** are common fallbacks when a model or preview feature isn't offered in East US. Keep a service and the project that consumes it in the same region unless a lab says otherwise.

6. **Set a budget you'll actually see.** Portal → Cost Management + Billing → Cost Management → Budgets → **+ Add**: scope = subscription, amount **US$10**, monthly, reset today, alerts at **50 / 80 / 100%** to your email. This is not because you expect to spend $10 — it's because a budget alert is the only thing that will tell you a forgotten Code Interpreter session or a Basic-tier AI Search service is quietly running.

7. **Learn the teardown ritual on day 1, not day 60.** AI service resources (`Microsoft.CognitiveServices`) **soft-delete for 48 hours**. A deleted resource still holds its name *and its F0 slot*. So the full ritual is:
   ```bash
   az group delete -n rg-learn-lang --yes --no-wait
   # then, to actually free the name and the F0 quota slot:
   az cognitiveservices account purge -n ai-lang-shawn -g rg-learn-lang -l eastus
   ```
   **If you hit this:** `Account name is already in use` or `The subscription already has an F0 account for this kind` after you deleted things — that's soft-delete. Purge it. You can also list what's pending: `az cognitiveservices account list-deleted -o table`.

#### What good looks like

- `az account show` returns your subscription in your own tenant, and you can explain the difference between the *subscription* (billing boundary) and the *tenant* (identity boundary) without hedging.
- Six empty resource groups exist; Cost Analysis shows $0.00.
- A $10 budget with three alert thresholds is armed.
- You can recite the teardown ritual: delete the RG, then purge the cognitive accounts.

---

### 3.2 The 40–45% domain, actually taught — AI concepts and capabilities

Read this section as the content, not as a pointer to content. The Learn modules restate it with nicer pictures; you should already know it before you open them.

#### Machine learning is curve-fitting on labeled history

Classical machine learning does one thing: it takes historical examples, finds a mathematical function that maps inputs to outputs on those examples, and then applies that function to inputs it has never seen. The inputs are **features**; the known answer is the **label**. Fitting the function is **training**; applying it is **inference** (or scoring). You always split your data — **training set** to fit, **validation set** to tune, **test/holdout set** to get an honest score — because a model that memorizes its training data (**overfitting**) looks brilliant and performs terribly in production. The opposite failure, a model too simple to capture the pattern, is **underfitting**.

The exam wants you to sort problems into families:

- **Supervised learning** — you have labeled examples.
  - **Regression** predicts a *number* on a continuous scale. "How many support tickets will we get next Tuesday?" "What will this laptop's resale value be?" Evaluated with **MAE** (mean absolute error — average miss in the same units as the label), **RMSE** (root mean squared error — same idea but punishes big misses harder), and **R²** (coefficient of determination — 0 to 1, how much of the variance the model explains).
  - **Classification** predicts a *category*. Binary ("will this user churn: yes/no") or multi-class ("which of 12 ticket queues does this belong to"). Evaluated with **accuracy** (fraction correct — misleading on imbalanced data), **precision** (of the things I flagged positive, how many really were — the metric you care about when false positives are expensive, like quarantining email), **recall** (of the real positives, how many did I catch — the metric you care about when misses are expensive, like malware detection), and **F1** (harmonic mean of the two). The **confusion matrix** is the 2×2 table of TP/FP/FN/TN those come from.
- **Unsupervised learning** — no labels.
  - **Clustering** groups similar items by distance in feature space. "Segment these 40,000 devices into behavioral cohorts." K-means is the canonical algorithm; you choose *k*, the model finds the groups, and nobody tells it what the groups mean.
- Also on the map: **anomaly detection** (find the outliers — think a login-pattern spike, which is exactly your day job), **forecasting** (regression over time series), **reinforcement learning** (an agent learns by reward — mentioned, not tested deeply).

**Exam framing:** you will be given a business sentence and asked which type it is. The tell is the output. A number on a scale → regression. A label from a fixed set → classification. "Group these without predefined categories" → clustering. "Which of these transactions is unusual" → anomaly detection.

#### Deep learning and the transformer are why any of this got interesting

A **neural network** stacks layers of weighted sums plus a nonlinearity; **deep learning** just means many layers. The practical consequence is **feature learning**: you stop hand-engineering features ("edge detector," "word count") and let the network derive its own representations from raw pixels or raw text, given enough data and GPU time. That's why deep learning took over vision and language while classical ML still wins on small tabular datasets.

The **transformer** architecture (2017, "Attention Is All You Need") added **self-attention**: when processing each token, the model computes how much every other token in the input matters to it, in parallel across the whole sequence. Before that, models processed text sequentially and lost the thread over long spans. Attention gave models long-range context *and* GPU-friendly parallelism, which is precisely what made scaling to billions of parameters economical. Every model you will touch in this path — GPT-5 class, Phi, Llama, embedding models — is a transformer.

#### Tokens, embeddings, vectors, context windows

**Tokens** are the units a language model actually reads and writes. Not words, not characters — subword fragments produced by a tokenizer. "unhappiness" might be `un` + `happi` + `ness`. Rule of thumb for English: **1 token ≈ 4 characters ≈ 0.75 words**; 1,000 tokens ≈ 750 words ≈ 1.5 pages. This matters because **you are billed per token, in and out**, and because limits are expressed in tokens.

The **context window** is the maximum number of tokens the model can consider in one request — *your prompt plus the model's response plus any retrieved documents plus the conversation history you resend*. Modern models are 128K–1M+ tokens. When people say "the model forgot what I said," they mean the conversation exceeded the window and older turns were dropped, or the app truncated them. Context is not memory: an LLM is stateless between calls, and "chat history" is just text your app re-sends every turn.

An **embedding** is a fixed-length list of floats — a **vector** — that represents the *meaning* of a piece of text (or an image) as a point in high-dimensional space. `text-embedding-3-small` produces 1,536 numbers; `text-embedding-3-large` produces 3,072. The useful property: semantically similar inputs land near each other. "How do I reset my password?" and "I forgot my login credentials" are far apart as strings and close together as vectors. Closeness is measured by **cosine similarity** (the cosine of the angle between the two vectors, from −1 to 1; 1 = identical direction). This single idea is the foundation of vector search, which is the retrieval half of RAG in Phase 3. Note that embedding models are *different models* from chat models, deployed separately, priced separately, and much cheaper.

#### What a language model mechanically does

It predicts the next token. That's it. Given a sequence of tokens, it produces a probability distribution over the entire vocabulary for what comes next, samples one, appends it, and repeats until it emits a stop token or hits the length limit. This is **autoregressive generation**. Everything else — reasoning, summarizing, writing code, "understanding" your question — is emergent behavior from doing that extremely well at scale.

Consequences you must be able to articulate:

- **Prompt** = the input you send. **Completion** (or response) = the tokens it generates. Both cost money; output tokens usually cost 3–8× input tokens.
- **Temperature** controls sampling randomness. **0** = always take the highest-probability token (near-deterministic, repeatable, right for classification, extraction, and JSON output). **~0.7–1.0** = sample more freely (varied, creative, right for brainstorming and marketing copy). **Top-p / nucleus sampling** is an alternate knob: sample only from the smallest set of tokens whose probabilities sum to p. Adjust one or the other, not both. **Watch out:** even at temperature 0 you are not *guaranteed* byte-identical output across calls — floating-point nondeterminism and backend routing can vary the result. "Deterministic" in this context means "as reproducible as it gets," and the exam-safe answer to "how do I make output more consistent/focused" is **lower the temperature**.
- **Hallucination** is the model producing fluent, confident, false content. It is not a bug you can patch out; it is the direct consequence of next-token prediction with no notion of truth. The model has no way to know it doesn't know.
- **Grounding** is the mitigation: put authoritative facts *into the prompt* and instruct the model to answer only from them, with citations. Retrieval-Augmented Generation (RAG) is grounding automated — retrieve relevant documents at query time, inject them, generate. Phase 3 builds this for real. At fundamentals level, know that grounding reduces hallucination, enables freshness (the model's training cutoff no longer limits it), and gives you citations for auditability.
- **Three ways to change model behavior**, in ascending order of cost and descending order of how often you should reach for them: **prompt engineering** (free, instant), **RAG/grounding** (cheap, gives the model facts it lacks), **fine-tuning** (expensive, retrains weights on your examples, changes *style, format, and task behavior* — not a way to teach it new facts, and it incurs hosting cost for the fine-tuned deployment). The exam loves the distinction: *"the model needs current internal policy documents"* → RAG, not fine-tuning. *"the model must always reply in our clipped support-ticket format"* → fine-tuning (or, honestly, a good system prompt).
- **SLM vs LLM**: small language models (Phi class, gpt-5-nano) trade breadth for cost, latency, and the ability to run at the edge or on-device. Your Talos cluster with NVIDIA GPUs is exactly the sort of place an SLM runs.
- **Multimodal** means one model accepts and/or produces more than one modality — text plus images, audio, or video. A multimodal chat model can take a screenshot and answer questions about it. This is why "vision" is no longer only a separate Vision API; a multimodal chat deployment does image understanding directly, and the exam now expects you to know both routes exist.

#### The workload categories (the sorting hat question)

Fundamentals exams test *which service for which scenario* relentlessly. Learn the boundaries:

- **Computer vision** — pixels in, structure out: captions and dense captions, tags, object detection with bounding boxes, people detection, OCR/Read (printed and handwritten text extraction), background removal, face detection/attributes, and custom-trained image classification or object detection.
- **Speech** — audio ↔ text: speech-to-text (transcription), text-to-speech (synthesis, neural voices), speech translation, speaker features, and voice agents.
- **Natural language / text analysis** — text in, structure out: sentiment, key phrases, named entities, PII detection, language detection, summarization, translation, intent recognition, question answering.
- **Information extraction** — documents in, fields out: Document Intelligence (invoices, receipts, IDs, forms, layout), Content Understanding (multimodal), and knowledge mining (indexing a corpus so it's searchable).
- **Generative AI** — content out: chat, code, images, and agents that take actions.

The classic trap: **"extract the total and vendor from a scanned invoice"** is **Document Intelligence**, not Vision OCR. OCR gives you *text and where it sits on the page*; Document Intelligence gives you *labeled key-value pairs, tables, and confidence scores* for a known document type. Similarly, **"determine whether this review is positive"** is Language sentiment analysis, not a generative model — even though a generative model could do it, the exam wants the purpose-built service.

#### Responsible AI: six principles, each with a real Azure feature

This is guaranteed exam content and it is always scenario-matched: they describe a situation and ask which principle applies, or ask which Azure feature implements a named principle. Memorize the six and anchor each to something concrete.

1. **Fairness** — the system should treat all groups equitably and not encode historical bias. *Concrete:* balanced/representative training data, disaggregated evaluation across demographic slices, the Responsible AI dashboard and Fairlearn tooling in Azure ML, and the hate/unfairness risk evaluator in Foundry evaluations. *Scenario tell:* "the loan model approves one group at a lower rate," "the recruiting model prefers one gender."
2. **Reliability and safety** — the system should perform consistently and fail safely, including under unexpected input. *Concrete:* content filters on prompts and completions, groundedness detection, evaluation runs before release, red-teaming, human-in-the-loop approval for consequential actions, staged rollout. *Scenario tell:* anything about an autonomous or physical system, or "what if a user tries to trick the model."
3. **Privacy and security** — protect data throughout its lifecycle. *Concrete:* PII detection and redaction in Azure AI Language, private endpoints and Private Link so traffic never touches the public internet, Entra ID + managed identity instead of API keys, customer-managed keys, data residency via region/deployment-type choice, and Microsoft's commitment that your prompts are not used to train the base models. *Scenario tell:* "customer records," "must not leave the EU," "must not traverse the public internet."
4. **Inclusiveness** — the system should work for everyone, including people with disabilities and speakers of other languages. *Concrete:* text-to-speech and speech-to-text for accessibility, live captioning, Translator and speech translation, image captioning/alt text generation, Immersive Reader. *Scenario tell:* "users with visual impairments," "employees in 14 countries."
5. **Transparency** — people should understand what the system is, how it decides, and its limitations. *Concrete:* Transparency Notes and model cards on Microsoft's AI systems, citations in RAG responses, surfacing confidence scores, disclosing that a user is talking to an AI, tracing that shows which tools an agent invoked. *Scenario tell:* "users should know why it made that recommendation," "must disclose."
6. **Accountability** — humans stay responsible; governance and audit exist. *Concrete:* RBAC and least-privilege on AI resources, Azure Policy, diagnostic logs to Log Analytics, the Foundry Control Plane for org-level governance of models and agents, defined ownership, human review gates. *Scenario tell:* "who is responsible," "we need an audit trail," "compliance requires oversight."

**The distinction people fumble:** privacy/security vs accountability. Encrypting and isolating the data is *privacy and security*. Being able to prove who did what and having a human answerable for outcomes is *accountability*. And transparency is about *explaining*, not about *permissions*.

---

### 3.3 The 55–60% domain, actually taught — Microsoft Foundry

#### What Foundry is, and why every tutorial you find is named wrong

The product has been renamed twice in two years: **Azure AI Studio** → **Azure AI Foundry** (Ignite 2024) → **Microsoft Foundry** (Ignite 2025). Portal is **ai.azure.com** throughout. Anything referring to "Azure AI Studio" is at least two UI generations old.

Foundry is the single plane where you pick a model, deploy it, test it, ground it, wrap it in an agent, secure it, and watch it run. Its pieces, as the exam names them:

- **Foundry Models** — the model catalog and the deployments you create from it. Includes Azure OpenAI models (GPT-5 family, embeddings, image models), Microsoft's Phi family, and partner/open models (Llama, Mistral, Cohere, DeepSeek, and others).
- **Foundry Agent Service** — the managed runtime for agents: an agent definition (model + instructions + tools), conversation **threads**, and **runs**. Microsoft hosts the state and the tool-execution loop.
- **Foundry Tools** — the renamed **Azure AI services** (what you knew as Cognitive Services): Language, Speech, Vision, Translator, Document Intelligence, Content Understanding, Content Safety. They are both standalone Azure resources *and* things an agent can call.
- **Foundry Control Plane** — the governance layer: which models are allowed, policy, quota and cost visibility, agent inventory. This is the part that will matter to you professionally more than to the exam.
- **Foundry IQ** — knowledge bases and **agentic retrieval**: you register knowledge sources once and agents query them with an LLM-driven, multi-query retrieval strategy instead of a single vector lookup. Phase 3 covers this properly.

#### Foundry resource vs Foundry project vs the classic hub

This is the single most confusing thing in the portal and it is examinable.

- A **Microsoft Foundry resource** is a normal Azure resource (of kind `AIServices`) in a resource group. It is the billing and security boundary: it holds the model deployments, the keys, the Entra RBAC assignments, the network settings, and the endpoint (`https://<name>.services.ai.azure.com`).
- A **Foundry project** is a child of that resource — a workspace for one effort. It gives you an endpoint of the form `https://<resource>.services.ai.azure.com/api/projects/<project>`, and it's what the SDK connects to. Projects share the parent resource's model deployments and connections. Creating one is fast and creates no extra dependent Azure resources.
- A **hub-based project** — now labeled **"Foundry (classic)"** — is the older model. A **hub** is a shared team-level resource that provisions dependent Azure resources with it: a Storage account, a Key Vault, sometimes Container Registry and Application Insights, plus hub-level connections and compute. Hubs are what you need for the older Prompt Flow experience, managed compute for open models, and managed VNet isolation.

**Choose:** a Foundry project for everything in this path. Choose a hub only if you specifically need managed compute, Prompt Flow, or the hub's managed network. **Exam tell:** "lightweight, agents and models, one endpoint, minimal dependent resources" → Foundry project. "Shared team resources, Key Vault and Storage provisioned with it, managed compute" → hub.

**Watch out:** many older tutorials (and some Learn modules that haven't been re-shot) walk you through hub creation. If a lab's screenshots show "Hub" and "AI Services connection," you're in the classic path — you can usually still complete it, but the SDK client construction differs (`AIProjectClient.from_connection_string()` with a connection string, versus the newer endpoint-based constructor).

#### The model catalog and how to actually choose a model

The catalog lists hundreds of models. Choosing is a five-question process, and the exam asks it as a scenario:

1. **Task and modality** — chat/completion, embeddings, image generation, speech, or reasoning? An embedding model cannot chat; a chat model cannot produce vectors for your index.
2. **Capability vs cost** — bigger models reason better and cost 10–50× more. For labs, coursework, classification, and extraction, a nano/mini model is not a compromise, it's correct.
3. **Context window** — will you stuff 40 pages of retrieved documents in? Check the token limit.
4. **Hosting type** — *serverless / standard* (pay per token, no infrastructure, instant) vs *managed compute* (you rent GPU VMs by the hour to host an open model — never do this in this path; it bills whether you call it or not).
5. **Region and quota** — models are not available everywhere, and your quota is per subscription, per region, per model.

The catalog UI gives you filters for exactly these, plus model cards with benchmarks, context length, and the license. **Filter on "Deployment options: Serverless / Standard"** to avoid accidentally selecting something that requires managed compute.

#### What "deploying a model" actually creates

Deploying does not copy a model anywhere. It creates a **named endpoint binding** in your resource: a deployment name (you choose it — e.g. `gpt-5-nano`), pointed at a model version, with a **deployment type** and an allocated **quota in TPM (tokens per minute)**. Three things follow, and all three are exam material:

- **You call the deployment name, not the model name.** Your code says `model="gpt-5-nano-dev"` if that's what you named it. Mismatched deployment names are the #1 cause of 404s from the SDK.
- **Authentication is either an API key or Microsoft Entra ID.** Keys are two per resource (so you can rotate one while the other serves), simple, and a liability — they're bearer credentials with no identity, no expiry, and no audit trail beyond "someone with the key." Entra ID auth uses your identity or a **managed identity** with an RBAC role (e.g. **Cognitive Services User** / **Azure AI User** to call inference, higher roles to manage). In code, `DefaultAzureCredential()` from `azure-identity` tries a chain of sources — environment variables, managed identity, Azure CLI login, VS Code login — which is why `az login` on your Mac is enough to authenticate local scripts with no secrets in the repo. As a PKI-and-Entra person: keys are shared secrets, Entra is per-principal auth with conditional access and revocation. The exam's preferred answer is always managed identity + RBAC.
- **Quota is a rate limit, not a budget.** TPM is tokens per minute; RPM (requests per minute) is derived from it. Exceeding it returns **HTTP 429**. Quota is allocated per subscription per region per model family, and you distribute it across deployments yourself. **If you hit this:** "InsufficientQuota" or a greyed-out Deploy button → you are on a trial subscription (no quota), or the model isn't available in that region, or your regional quota is fully assigned to another deployment you forgot about. Fix by converting to PAYG, changing region, or reducing an existing deployment's TPM.

**Deployment types** get taught properly in Phase 3, but at fundamentals level know that **Global Standard** is the cheapest, highest-quota, pay-per-token option that routes your request to any Microsoft datacenter with capacity, and that **Provisioned (PTU)** reserves dedicated capacity billed hourly whether you use it or not. You will only ever use Global Standard.

#### Playgrounds

Each capability has a playground: **Chat** (system prompt, user turns, temperature, max tokens, "Add your data" for quick grounding), **Images**, **Audio/Speech**, and **Agents**. The chat playground has a **"View code"** button that emits working Python for the exact configuration you just tested — this is the fastest bridge from clicking to coding, and you should use it every time. The playground is also the fastest way to *see* what temperature does: run the same prompt at 0 and at 1 three times each.

#### Foundry Tools (the former Azure AI services)

These are the pretrained, task-specific APIs. You provision them as Azure resources — either as **individual services** (kind `TextAnalytics`, `SpeechServices`, `ComputerVision`, `FormRecognizer`, `TextTranslation`) or as a **multi-service AI Services resource** that exposes many capabilities behind one endpoint and one key. The tradeoff, and it's examinable: **multi-service = one endpoint, one bill, simpler ops; single-service = independent scaling, separate keys/isolation, and — crucially for you — the free F0 tier.** The multi-service resource has no F0. Every zero-cost lab in Phase 2 therefore uses single-service F0 resources.

#### Agents, at fundamentals depth

An **agent** = a model + instructions + tools + the loop that lets it decide to call those tools. The distinction from a chatbot is *action*: a chatbot answers, an agent looks things up, calls APIs, runs code, and takes steps toward a goal. In Foundry Agent Service you define the agent (model, instructions, tools), open a **thread** for a conversation, add messages, and start a **run**; the service handles the tool-calling loop and stores thread state for you. Built-in tools at this level: **File Search** (upload docs, get vector-based grounding), **Code Interpreter** (sandboxed Python for math/data/charts), **grounding with web search**, and **function calling** (the model asks your code to run a function you defined).

#### The SDK path

```bash
pip install azure-ai-projects azure-identity
```

`azure-ai-projects` v2.x is the umbrella package — it bundles the `openai` client and `azure-identity`, and surfaces agent operations (from `azure-ai-agents`) as `AIProjectClient.agents`. The shape is always the same:

```python
from azure.identity import DefaultAzureCredential
from azure.ai.projects import AIProjectClient

project = AIProjectClient(
    endpoint="https://<resource>.services.ai.azure.com/api/projects/<project>",
    credential=DefaultAzureCredential(),
)

client = project.get_openai_client()          # OpenAI-compatible client, Entra-authenticated
resp = client.responses.create(model="gpt-5-nano", input="Explain TPM quota in one sentence.")
print(resp.output_text)
```

Three ideas to carry forward: **credential → project client → capability client**; you never put a key in the code; and the inner client is OpenAI-compatible, so the vast body of OpenAI-library examples on the internet mostly applies. **Watch out:** helper names shift between v2 minor releases. If `get_openai_client()` doesn't exist in your installed version, check `pip show azure-ai-projects` and the package README — the pattern is stable even when the method name isn't.

---

### 3.4 Do this — Week 3

Roughly 15 hours. Order matters.

1. **(Day 1, ~2 hrs)** Complete §3.1 end to end: signup, CLI, login, providers, resource groups, budget, teardown ritual.
2. **(Day 1, 30 min)** Take the **free AI-901 practice assessment** on AI Skills Navigator *cold*, before studying. You'll score somewhere in the 50s. The point is the per-domain breakdown — it tells you whether your gap is concepts or Foundry. Screenshot the result.
3. **(Days 2–3, ~5 hrs)** Work the **concepts** learning paths linked from the AI-901 exam page, using §3.2 above as your outline. As you go, keep a single `ai901-notes.md` with one line per term. If a module explains something you already read here, skim it at 2× and do the knowledge check.
4. **(Days 2–4, ~4 hrs)** Run the hands-on exercises from **`mslearn-ai-fundamentals`** (hosted at `microsoftlearning.github.io/mslearn-ai-fundamentals/`). The index groups them by module — work the Foundry portal tour, the text/language exploration, the speech exercise, the vision/image analysis exercise, the document-extraction exercise, and the generative-AI playground exercise. These are portal-driven, not code-driven; the goal is that no screen in ai.azure.com is unfamiliar.
5. **(Day 4, ~2 hrs)** Run the **`mslearn-ai-concepts`** exercises — the newer concept-level labs that pair with the 40–45% domain.
6. **(Day 5, ~1 hr)** Build one thing unaided, no lab instructions: create a Foundry project in `rg-learn-ai901`, deploy **gpt-5-nano** as Global Standard with a small TPM allocation, test it in the chat playground with a system prompt of your choosing, click **View code**, paste that code into a local `.py`, swap the auth to `DefaultAzureCredential`, and run it from your Mac terminal. This exact sequence is the practical core of the 55–60% domain.
7. **(End of Week 3, ~1 hr)** Watch **John Savill's AI-901 Study Cram** (May 2026, ~1 hr) as consolidation — after the labs, not before. His framing of deployments/endpoints/auth and the Entra angle is the part that maps to your existing knowledge. If the concepts domain still feels thin, his legacy AI-900 Study Cram v2 remains the cleanest explanation of classical ML/vision/NLP.
8. **(Any evening)** Register for a **Microsoft Virtual Training Day** in the AI fundamentals track. Attendance currently earns a **50% discount voucher** for fundamentals exams, bringing AI-901 to ~US$50. The voucher lands ~5–10 business days after the event and is typically valid ~90 days. **Timing rule: do not book the exam until the voucher is in your inbox** — you can't apply it retroactively. If no event falls inside your window, pay the $99 rather than delaying the schedule.

### 3.5 Do this — Week 4

1. **(Day 1)** Re-take the practice assessment. Expect 70s. Every miss gets the same treatment: find the Microsoft Learn doc that covers it, read the whole page, write one line in your notes. Do not re-roll the assessment to "get a better number."
2. **(Days 1–3)** Finish the **Foundry implementation** learning paths from the exam page. Cross-check line by line against the **AI-901 study guide** — literally open it and tick each bullet. Anything you can't demonstrate in the portal, go demonstrate.
3. **(Day 3)** Responsible AI drill: for each of the six principles, write two sentences — the principle in your own words and one Azure feature that implements it. Then have a scenario quiz run against you: given "our chatbot must tell customers it's a bot," name the principle. This exact question style is on the exam.
4. **(Day 4)** Service-selection drill: write 15 one-line scenarios ("transcribe recorded support calls," "pull the invoice total from a PDF," "detect whether a photo contains a hard hat," "group customers by purchase behavior," "answer HR policy questions from our handbook") and answer each with the service *and* why not the near-miss alternative. This is the highest-yield hour of the whole two weeks.
5. **(Day 5)** Practice assessment until you hit **≥ 80% on two consecutive runs**. Then book and sit the exam — ideally end of Week 4, absolute latest the start of Week 5.
6. **(Ongoing)** Tear down everything in `rg-learn-ai901` when you're done with it, purge the accounts, and confirm Cost Analysis is still flat.

### 3.6 Exam angle

- **Format:** ~40–60 items, multiple choice, multiple response, drag-and-drop matching, and drop-down "complete the sentence" items. Fundamentals exams do **not** include case studies and do **not** give you Microsoft Learn documentation access during the exam. Pass mark 700 on a scaled 1–1000 range — that is *not* 70% of questions.
- **The dominant question type is scenario → service.** They describe a business need in one sentence and offer four Azure services. Practice the boundaries that overlap:
  - **Vision OCR/Read vs Document Intelligence** — Read gives you text and its location; Document Intelligence gives you *structured fields* (vendor, total, line items) with confidence scores from a known form type.
  - **Language vs a generative model** — for sentiment, key phrases, entities, PII, and language detection, the answer is Azure AI Language even though GPT could do it.
  - **CLU vs Custom Question Answering** — CLU maps an utterance to an *intent plus entities* so your app can take an action ("book a meeting for 3pm"); Custom Question Answering returns an *answer from a knowledge base* ("what's the PTO policy"). Intent + action → CLU. FAQ → CQA.
  - **Speech translation vs Translator** — audio in, translated speech/text out → Speech translation. Text in, text out → Translator.
  - **Custom Vision vs Image Analysis** — off-the-shelf tags/captions/objects → Image Analysis. "Recognize *our* product SKUs / *our* defect types" → Custom Vision (train it).
  - **Classification vs object detection in Custom Vision** — "what is in this image" (one label per image) → classification. "where is it and how many" (bounding boxes) → object detection.
- **Foundry vs the services underneath.** A recurring trap: the question asks what *Foundry* provides (a unified portal/SDK for model catalog, deployment, playgrounds, agents, evaluation, governance) versus what the *individual services* provide (the actual task-specific inference). Foundry is not "the thing that does OCR"; Vision is. Foundry is where you find, deploy, test, and govern.
- **Responsible AI principle matching** appears in nearly every form of the exam. See §3.2.
- **Token/context questions** are usually practical: which knob reduces randomness (temperature), what counts against the context window (prompt + history + retrieved content + completion), why an embedding model is used for search rather than chat.
- **Cost/quota literacy:** know that TPM is a rate limit, that 429 means throttled not broken, and that F0 exists for AI services but *not* for model inference.

### 3.7 What good looks like

- From a blank resource group, in under 20 minutes with no instructions: create a Foundry project, deploy a nano model, test in the playground, call it from local Python with `DefaultAzureCredential`, then delete and purge.
- You can explain to a colleague, without notes: what a token is, why embeddings enable semantic search, what grounding fixes and what it doesn't, and why key auth is worse than managed identity.
- Fifteen scenario→service answers correct, with the near-miss alternative named for each.
- Two consecutive practice runs ≥ 80%, with a written trail of every miss and the doc you read.

### ✅ Phase 1 gate — do not start Phase 2 until:

- [ ] Practice assessment ≥ 80% on two consecutive runs, with every wrong answer traced back to a doc you then read
- [ ] You can, unaided: create a Foundry project, deploy a model, test it in the playground, and call it from Python via the SDK — and then tear it all down cleanly (delete **and** purge)
- [ ] You can explain each responsible-AI principle with a concrete Azure feature that implements it
- [ ] You can sort 15 business scenarios to the correct service and name why the near-miss is wrong
- [ ] You can explain tokens, context window, embeddings, temperature, hallucination, and grounding in plain language
- [ ] Subscription hygiene proven: providers registered, budget alert armed, teardown ritual practiced, `az account show` returns the right tenant
- [ ] **AI-901 exam PASSED** (booked for end of Week 4 / start of Week 5 at the latest — a scheduled exam is a forcing function)
- [ ] Cost Analysis shows $0 unexpected spend; no orphaned resources outside your lab resource groups

---

## 4 · Phase 2 — Applied AI services bridge (Weeks 5–8)

**Goal:** own the three "narrow AI" domains that make up 30–45% of AI-103 (computer vision 10–15%, text analysis 10–15%, information extraction 10–15%) plus the retrieval foundation that Phase 3's RAG work sits on — built entirely on free tiers, and hardened with the enterprise lens that is your actual differentiator over bootcamp graduates.

**The framing that matters:** these services are not "the old stuff before generative AI." In real architectures they are the *deterministic, cheap, auditable* layer around the model. You use Document Intelligence to get reliable fields off an invoice and a language model to reason about them — not a language model to squint at the PDF. You use PII redaction *before* text reaches a model. You use AI Search to retrieve, and the model only to phrase. Every one of those is an exam answer and a job interview answer.

### 4.0 The week map and the free-tier ground rules

| Week | Workstream | Repo · hosted labs | Free tier you'll stand up |
|---|---|---|---|
| 5 | Text analysis + Speech | `mslearn-ai-language` · microsoftlearning.github.io/mslearn-ai-language/ | Language **F0** (5,000 text records/mo, pooled) + Speech **F0** (5 audio hrs STT, 0.5M chars TTS) |
| 6 | Computer vision | `mslearn-ai-vision` · microsoftlearning.github.io/mslearn-ai-vision/ | Vision **F0** (5,000 transactions, 20/min) + Custom Vision training/prediction **F0** |
| 7 | Information extraction | `mslearn-ai-information-extraction` · microsoftlearning.github.io/mslearn-ai-information-extraction/ | Document Intelligence **F0** (500 pages, **first 2 pages per request only**) |
| 8 | AI Search / RAG foundations + hardening catch-up | AI Search **Free** tier + week 5–7 backlog | Search Free (50 MB, 3 indexes / 3 indexers / 3 data sources, 1 per subscription) |

**The F0 rules that will bite you, stated once:**

- **One F0 resource per service *kind* per subscription.** You cannot have two Language F0s. Plan names accordingly.
- **The multi-service "AI Services" resource has no F0.** Labs that say "create an Azure AI Services resource" will default you to S0 (paid). Create the *single-service* resource of the right kind instead and paste its endpoint/key into the lab. Kinds: `TextAnalytics` (Language), `SpeechServices`, `ComputerVision`, `FormRecognizer` (Document Intelligence), `TextTranslation`, `CustomVision.Training`, `CustomVision.Prediction`.
- **Soft-delete is 48 hours.** Delete a Language F0 and try to make another with the same name — or *any* name, since the F0 slot is still consumed — and it fails. `az cognitiveservices account purge -n <name> -g <rg> -l <region>` is mandatory, and note it takes the *region*, not just the RG.
- **F0 throttles, it doesn't bill.** Exceeding the free allowance returns 429, not a charge. That's your safety net.
- **Custom features need a custom subdomain.** Any resource you intend to use with Entra auth, private endpoints, or the custom-model studios needs `--custom-domain <unique-name>` at creation time. Add it up front; retrofitting is `az cognitiveservices account update -n <name> -g <rg> --custom-domain <name>` and it can't be undone.

**Standard creation pattern (memorize it, you'll type it eight times):**
```bash
az cognitiveservices account create \
  -n ai-lang-shawn -g rg-learn-lang -l eastus \
  --kind TextAnalytics --sku F0 \
  --custom-domain ai-lang-shawn --yes
az cognitiveservices account show -n ai-lang-shawn -g rg-learn-lang --query properties.endpoint -o tsv
az cognitiveservices account keys list -n ai-lang-shawn -g rg-learn-lang --query key1 -o tsv
```

**Cloud Shell vs local.** The labs default to Azure Cloud Shell because it has the CLI, Python, and an authenticated session pre-baked. Use it when a lab explicitly depends on it. Prefer local VS Code otherwise — you'll learn the auth model properly, and `DefaultAzureCredential` picking up your `az login` on the Mac is exactly how you'll run code in Phase 3. **If you hit this:** local runs failing with `DefaultAzureCredential failed to retrieve a token` almost always means you're logged into the wrong tenant or you never assigned yourself an RBAC role on the resource (owner of the subscription ≠ data-plane permission on a Cognitive Services account — you still need **Cognitive Services User** or higher). Fix:
```bash
az role assignment create --assignee <your-upn> \
  --role "Cognitive Services User" \
  --scope $(az cognitiveservices account show -n ai-lang-shawn -g rg-learn-lang --query id -o tsv)
```
RBAC propagation takes a minute or two. Always pick the **Python** variant when a lab offers C#.

**The hardening note ritual (every week, non-negotiable).** For each service you stand up, write a one-page `hardening-<service>.md` in a public `azure-ai-notes` repo. Not prose about how security is important — a design. Each note answers, concretely:

1. **Private networking:** which private endpoint sub-resource, which **private DNS zone**, and what breaks without the DNS zone. (Zones: `privatelink.cognitiveservices.azure.com` for AI services, `privatelink.services.ai.azure.com` for Foundry/AI Services endpoints, `privatelink.openai.azure.com` for Azure OpenAI endpoints, `privatelink.search.windows.net` for AI Search, `privatelink.blob.core.windows.net` for the Storage the indexers read.) Include the public-access setting you'd flip: `az cognitiveservices account update ... --public-network-access Disabled` (or network ACLs with selected VNets/IPs).
2. **Key auth off:** `az resource update --ids <resource-id> --set properties.disableLocalAuth=true`. Note that this *requires* a custom subdomain, and that there is an Azure Policy to enforce it tenant-wide.
3. **Identity:** system-assigned vs user-assigned managed identity, and why user-assigned wins when multiple app instances or a redeploy would otherwise churn the principal ID.
4. **RBAC role choice:** name the *least* privileged role that works (e.g. Cognitive Services User for inference; Search Index Data Reader for query-only; Search Service Contributor only for the identity that creates indexes) and the scope you'd assign it at.
5. **Secrets and config:** what would live in Key Vault, what would be app config, and why with managed identity there should be almost no secrets left.
6. **Data residency and logging:** region choice, diagnostic settings to Log Analytics, what those logs do and don't contain (they don't contain prompt content unless you enable it).
7. **Cost guardrails:** which SKU you'd pick in production and why, what the runaway-cost failure mode is for this service, and the budget/alert you'd set.

You are already fluent in six of these seven for other products. Writing them for AI services is what converts "sysadmin who did some labs" into "engineer who can take this to a change advisory board." Savill's evergreen **Managed Identity Deep Dive**, **Private Link Deep Dive**, and **RBAC Deep Dive** are the Thursday-slot inputs; the **Azure OpenAI security baseline** doc gives you the control IDs to cite.

---

### 4.1 Week 5 — Text analysis and Speech

#### What you're actually learning: Azure AI Language

Language is a bundle of capabilities behind one endpoint. The exam's core question is always **"pretrained or custom?"** — so learn each capability *and* which side of that line it sits on.

**Pretrained (call it, no training, works day one):**

- **Sentiment analysis** returns positive/negative/neutral with confidence scores at both document and sentence level. **Opinion mining** is a flag on the same call that goes further: it extracts *aspect → opinion* pairs, so "the room was clean but the staff were rude" yields `room: clean (positive)` and `staff: rude (negative)`. Exam tell: "which aspects of the product do customers complain about" → sentiment **with opinion mining**, not plain sentiment.
- **Key phrase extraction** pulls the main talking points out of unstructured text. Cheap way to tag or cluster a corpus. It does *not* summarize and it does *not* classify.
- **Named entity recognition (NER)** identifies and categorizes entities — person, location, organization, datetime, quantity, and many subcategories. **Entity linking** goes one step further and resolves an entity to a Wikipedia URL, which disambiguates "Mars" the planet from "Mars" the company.
- **PII detection** is NER tuned for sensitive data (names, SSNs, phone numbers, credit cards, and a separate health/PHI mode) and it can **redact** — return the text with entities masked. Architecturally this is the thing you put *in front of* a model call so customer data never reaches the LLM. Exam tell: "must remove customer identifiers before processing" → Language PII with redaction.
- **Language detection** returns the ISO language and a confidence score; on ambiguous or mixed input it returns `(Unknown)` with a score of 0 rather than guessing. Know that behavior — it's a favorite detail question.
- **Summarization** comes in two flavors and the distinction is guaranteed exam content. **Extractive** summarization selects the most important *existing* sentences and returns them verbatim with rank scores — nothing is invented, so it's the safe choice for legal/medical text. **Abstractive** summarization generates *new* sentences that paraphrase the content — more readable, but it's generation, so it can drift. There are also conversation-specific summarization modes (issue/resolution) for call transcripts.

**Custom (you bring data and train a model):**

- **Custom text classification** — you label documents with your own categories and train. **Single-label** (each document gets exactly one class) vs **multi-label** (a document can carry several). Exam tell: routing incoming tickets to one of eight queues → single-label; tagging a research paper with all applicable topics → multi-label.
- **Conversational Language Understanding (CLU)** — the successor to LUIS. You define **intents** (what the user wants: `BookFlight`, `CheckStatus`), supply **utterances** (example phrasings, 15–30 per intent minimum for anything decent), and label **entities** inside those utterances (`destination`, `date`). Entity types: **learned** (the model infers them from your labels), **list** (an explicit enumeration with synonyms), **prebuilt** (Azure's own — datetime, number, person), and **regex**. You train, review the evaluation (per-intent precision/recall/F1, plus a confusion matrix that shows which intents bleed into each other), then **deploy** to a named deployment slot, and your app calls that deployment. The runtime returns the top intent with a confidence score plus extracted entities — *your* code decides what action to take. **Orchestration workflow** is the related concept: one top-level model that routes an utterance to the right child CLU model, custom QA knowledge base, or LUIS app, for when a single bot spans several domains.
- **Custom Question Answering (CQA)** — you build a **knowledge base** by ingesting FAQ URLs, PDFs, or manuals; the service extracts question/answer pairs; you add alternate phrasings ("chit-chat" personality packs are optional), test in the studio, and **publish**. At runtime, a user question is matched against the KB and the stored answer is returned with a confidence score, plus optional **multi-turn prompts** (follow-up buttons that disambiguate). **Architecturally important:** CQA is backed by **Azure AI Search** under the hood — creating a CQA-enabled Language resource requires linking a Search service, which is why it consumes one of your three free-tier indexes.

**When pretrained vs when custom — the answer the exam wants:** use pretrained when the categories are universal (sentiment, entities, PII, language). Use custom when the categories are *yours* and no general model could know them (your eight ticket queues, your product taxonomy, your app's intents). Custom costs training time, labeled data, and a deployment lifecycle; don't reach for it when a pretrained capability already covers the need.

#### What you're actually learning: Azure AI Speech

- **Speech to text (STT)** — two modes, and the difference is examinable. **Real-time** transcription streams audio over a websocket and returns interim + final results, used for live captioning and voice agents; audio length per request is limited (short-form). **Batch transcription** takes a set of audio files in blob storage via a REST job, runs asynchronously at scale, and is the right answer for "transcribe 10,000 recorded support calls overnight." **Watch out: batch transcription is not available on the F0 tier.** You will learn it conceptually and lab it in real time only. That gap is worth noting in your Phase 4 self-audit because the exam does ask about batch.
- **Text to speech (TTS)** — **neural voices** are the modern ones (hundreds of voices across 140+ locales); the old "standard" voices are retired. Multilingual voices can speak several languages from one voice identity.
- **SSML** (Speech Synthesis Markup Language) is the XML you send instead of plain text to control delivery: `<voice name="en-US-AvaMultilingualNeural">`, `<prosody rate="+10%" pitch="-2st">`, `<break time="500ms"/>`, `<say-as interpret-as="telephone">`, `<lang xml:lang="fr-FR">`, `<mstts:express-as style="cheerful">`. Exam tell: "control pronunciation / insert a pause / change speaking style" → SSML.
- **Speech translation** — audio in, translated text or synthesized speech out, in one call. Different from Translator (text→text).
- **Custom speech** — you adapt the base STT model to your domain by supplying audio+transcripts or just domain text, to fix recognition of jargon, product names, and accents. "The model keeps mis-hearing our SKU codes" → custom speech.
- **Custom neural voice** — a brand voice trained from recordings of a specific speaker. **Limited Access**: gated behind an application and a responsible-AI review, because voice cloning is an impersonation risk. That gating is itself examinable (it's the responsible AI story made concrete).
- **Voice Live** — the current low-latency voice-agent path: a single API that wires speech in, a model, and speech out into one conversational loop with interruption/barge-in handling, instead of you manually chaining STT → LLM → TTS. This is the modern answer to "build a voice assistant."
- **Speaker recognition** (verification/identification) exists and is also limited-access.

**Keys, regions, and the detail people miss:** the Speech SDK is initialized with a **key + region** (not a full endpoint URL) in most samples, and the region string must match exactly (`eastus`, not `East US`). Custom endpoints override that.

#### Do this — Week 5

1. Stand up the resources:
   ```bash
   az cognitiveservices account create -n ai-lang-shawn -g rg-learn-lang -l eastus \
     --kind TextAnalytics --sku F0 --custom-domain ai-lang-shawn --yes
   az cognitiveservices account create -n ai-speech-shawn -g rg-learn-lang -l eastus \
     --kind SpeechServices --sku F0 --custom-domain ai-speech-shawn --yes
   ```
   Grab endpoints and keys; put them in a local `.env` that is in `.gitignore` (and note in your hardening doc that in production this is a managed identity instead).
2. Clone the repo and work the hosted lab index at `microsoftlearning.github.io/mslearn-ai-language/`, Python variants, in this order: text analytics (sentiment/key phrases/entities/language), custom text classification, conversational language understanding, custom question answering, the text-analysis agent lab, then the speech labs (STT/TTS) and the Voice Live agent lab.
3. For the CLU lab, deliberately break it: add a ninth utterance that's ambiguous between two intents, retrain, and read the confusion matrix. Understanding *why* intents bleed is worth more than a clean pass.
4. For summarization, run the same paragraph through extractive and abstractive and diff the output. You want the difference to be visceral, not memorized.
5. Run one PII-redaction call and feed the redacted output into the chat playground. That two-step is a production pattern and a great interview anecdote.
6. **Hardening note #1:** `hardening-language-speech.md`. Private endpoint on `privatelink.cognitiveservices.azure.com`; disable local auth; managed identity; **Cognitive Services User** at resource scope for the app identity; note that CQA drags in an AI Search dependency that *also* needs private networking and its own RBAC; note that Speech SDK key+region auth is the awkward one to convert to Entra (it supports Entra tokens, but the SDK setup differs — say so).
7. **Watch out:** custom features (custom text classification, CLU, CQA) require the Language resource to be in a region that supports them and, for the custom-model studios, a linked Storage account for training data. F0 permits limited custom training. **If you hit this:** training refuses to start or the studio can't see your resource → check region support first, storage linkage second, tier third. Free-tier training may queue behind paid tenants; be patient rather than re-clicking.
8. **(Optional, high value for you)** Language, Speech, Vision-Read, and Document Intelligence ship as **Docker containers** with `Eula=accept`, `Billing=<your F0 endpoint>`, `ApiKey=<key>` and 443 egress for metering. Run one on your Talos cluster: local inference, cloud metering, F0-billed, $0. Containerized/disconnected deployment is examinable under plan-and-manage, and running one is a differentiator almost nobody has.

#### Exam angle — Week 5

- Extractive vs abstractive summarization (verbatim selection vs generated paraphrase).
- CLU vs Custom Question Answering vs custom text classification: **intent + entities for an action** vs **answer from a KB** vs **assign a category to a document**.
- Single-label vs multi-label classification.
- Sentiment vs opinion mining (document-level polarity vs aspect-level).
- NER vs entity linking vs PII detection.
- Real-time vs batch transcription, and that batch is a REST job over blob storage.
- SSML for pronunciation, pauses, and speaking style.
- Which capabilities are Limited Access and why (custom neural voice, speaker recognition) — this is a responsible-AI question wearing a technical costume.
- Language detection returning `(Unknown)` on ambiguous input.

#### What good looks like — Week 5

- All `mslearn-ai-language` Python labs green.
- A CLU model you built from scratch (not the lab's) with 3 intents and 2 entity types, trained, evaluated, deployed, and called from Python.
- A CQA knowledge base answering questions from a PDF you supplied.
- A working two-stage script: PII-redact → send to a model.
- `hardening-language-speech.md` committed.
- Both F0 resources deleted and purged at week's end (or kept if you'll reuse them — but know which you chose and why).

---

### 4.2 Week 6 — Computer vision

#### What you're actually learning

**Image Analysis** (the current Vision API, v4.0) is one call that can return several *visual features* at once:

- **Caption** — one natural-language sentence describing the whole image. **Dense captions** — up to ten captions, each tied to a region of the image. Exam tell: "generate alt text for accessibility" → caption (and that's also an *inclusiveness* answer).
- **Tags** — a flat list of content labels with confidence.
- **Objects** — labels *with bounding boxes*.
- **People** — bounding boxes for people specifically.
- **Smart crops** — the best crop region for a target aspect ratio, so thumbnails don't decapitate people.
- **Read (OCR)** — extracts printed and handwritten text with per-line and per-word bounding polygons and confidence. Works across many languages, handles rotation and mixed layouts.

**The OCR boundary you must hold:** Read tells you *what text appears and where*. It does not tell you that the number in the lower right is the invoice total. The moment the question involves *fields, key-value pairs, tables, or a document type*, the answer is **Document Intelligence** (week 7). "Digitize handwritten notes" → Read. "Extract the total from receipts" → Document Intelligence prebuilt receipt.

**Face** — detection (bounding box, head pose, occlusion, blur, glasses, mask), and, gated behind **Limited Access** approval, **verification** (are these two faces the same person), **identification** (who is this, against an enrolled group), and **liveness** detection. Facial *recognition* capabilities require an application describing your use case; some capabilities (emotion inference, gender/age attribute prediction) were **retired outright** on responsible-AI grounds. Know this story cold: it is the single most concrete example of Microsoft's responsible AI principles constraining a product, and the exam uses it.

**Custom Vision** — when the off-the-shelf tags don't include *your* categories, you train. Two project types, and this is a guaranteed question:

- **Classification** — one or more labels for the *whole* image. Multiclass (exactly one label) or multilabel (several). "Is this weld good or defective?"
- **Object detection** — labels *plus bounding boxes*, so you get position and count. "How many hard hats are in this photo and where?"

Workflow: create a project (choose a domain — General, Food, Landmarks, Retail, or a **compact** domain if you intend to export the model to run offline on edge/mobile/containers), upload and tag images (minimum ~15 per tag, realistically 50+, and *balanced* across tags), **Train**, read the evaluation metrics — **precision**, **recall**, and **mAP** (mean average precision, object detection only) — then **Publish** the **iteration** to a prediction resource and call the published endpoint. Every retrain creates a new iteration; publishing is what makes one live, and you can roll back by publishing a previous iteration. Note the two separate resources: `CustomVision.Training` and `CustomVision.Prediction`, each with its own key, each with an F0.

**Image generation** — text-to-image models (DALL·E class and successors) deployed from the Foundry catalog and driven from the Images playground: prompt, size, quality, count. Understand that generated images carry provenance metadata and are subject to content filtering, and that the responsible-AI concerns here are deepfakes and copyright.

**Multimodal chat models for vision** — the modern alternative to calling the Vision API: send an image directly to a GPT-class multimodal deployment and ask questions about it in natural language ("does this screenshot show an error dialog, and what does it say?"). Choose the *service* when you need structured, cheap, deterministic output at scale; choose the *multimodal model* when you need open-ended reasoning about the image. The exam asks this as a cost/latency/flexibility tradeoff.

**Video and multimodal understanding** — analyzing video for scenes, objects, transcript, faces, and moments; increasingly handled by Content Understanding and by multimodal models with video input rather than a separate legacy Video Indexer path.

**Content Understanding** — this is new, it is examinable, and almost nobody's study notes cover it. It is a **multimodal information-extraction service in Foundry**: you define an **analyzer** by declaring a schema of the fields you want, and point it at **documents, images, audio, or video**. It returns those fields as structured JSON with confidence, plus grounding back to the source region/timestamp. Think of it as "Document Intelligence's idea, generalized past documents, and driven by a schema you describe rather than a prebuilt model you pick." Use it when your input is mixed media or when you want one extraction pipeline across formats. **Watch out:** it's newer and therefore available in a limited set of regions — check the region dropdown when you create the Foundry project, and if Content Understanding doesn't appear in the portal's left nav, your project's region is the reason.

#### Do this — Week 6

1. Stand up the resources:
   ```bash
   az cognitiveservices account create -n ai-vision-shawn -g rg-learn-vision -l eastus \
     --kind ComputerVision --sku F0 --custom-domain ai-vision-shawn --yes
   az cognitiveservices account create -n cv-train-shawn -g rg-learn-vision -l eastus \
     --kind CustomVision.Training --sku F0 --yes
   az cognitiveservices account create -n cv-pred-shawn -g rg-learn-vision -l eastus \
     --kind CustomVision.Prediction --sku F0 --yes
   ```
2. Work `mslearn-ai-vision` (hosted index, Python): image analysis, OCR/Read, custom vision (do **both** classification and object detection projects — don't skip one), the vision-enabled chat app (multimodal), image generation, video/multimodal understanding, and the Content Understanding lab.
3. Build one custom vision model on **your own** images — photograph 40 objects from your homelab or office in three categories, train, evaluate, and notice how the metrics move when you add 10 more images of the weakest class. This is how you learn that data quality beats model choice.
4. Do the same image through both paths — Vision Image Analysis and a multimodal chat deployment — and write three sentences on which you'd ship and why.
5. **Hardening note #2:** `hardening-vision.md`. Same seven headings. Add: where the images live (blob storage with private endpoint on `privatelink.blob.core.windows.net`), whether images are retained, the Limited Access posture for Face and what your approval justification would say, and the cost failure mode (a retry loop against a paid tier at 5,000 transactions/hour).
6. **Watch out:** Vision F0 is rate-limited to **20 transactions per minute**. A `for` loop over 200 images will 429 partway through. Add `time.sleep(3)` or a retry-with-backoff — and note in your hardening doc that production code needs exponential backoff on 429 regardless of tier.

#### Exam angle — Week 6

- Image Analysis features by name and output shape: caption vs dense captions vs tags vs objects (boxes) vs people vs smart crop.
- **OCR/Read vs Document Intelligence** — the most reliably tested boundary in the vision domain.
- **Custom Vision classification vs object detection**, and multiclass vs multilabel.
- Custom Vision lifecycle: tag → train → evaluate (precision/recall/mAP) → publish iteration → predict; and that a **compact domain** is what lets you export for edge/offline.
- Face: which capabilities are Limited Access, which were retired, and why — mapped to responsible AI.
- When to use a multimodal chat model instead of the Vision service.
- Content Understanding: schema-defined analyzers across documents/images/audio/video.
- Minimum image counts and the need for balanced, representative training data (which is also the *fairness* principle in disguise).

#### What good looks like — Week 6

- All `mslearn-ai-vision` Python labs green.
- Two Custom Vision projects of your own — one classification, one object detection — trained, published, and called from Python by iteration name.
- One image analyzed both ways with a written recommendation.
- A Content Understanding analyzer you defined, run against at least two media types.
- `hardening-vision.md` committed. Resources deleted and purged.

---

### 4.3 Week 7 — Information extraction

#### What you're actually learning: Azure AI Document Intelligence

Document Intelligence (formerly Form Recognizer — old docs, and the `FormRecognizer` CLI kind, still use that name) turns documents into structured data. Three model families:

**1. Prebuilt models** — trained by Microsoft, zero setup, call and go:

- **Read** — text extraction (OCR) plus language detection; the base layer.
- **Layout** — text *plus document structure*: tables (with cell row/column spans), selection marks (checkboxes, ticked or not), paragraph roles (title, section heading, page header/footer), and reading order. Layout is the workhorse for **RAG preprocessing**, because it gives you markdown-ish structure to chunk on instead of a wall of text. Remember this — it reappears in Phase 3.
- **General document / key-value pairs** — extracts generic key:value pairs from arbitrary forms.
- **Domain models** — **invoice** (vendor, customer, invoice ID, dates, line items, subtotal, tax, total), **receipt**, **identity document** (passports, driver's licenses), **business card**, **health insurance card**, **US tax forms (W-2, 1098, 1099)**, **bank statement**, **pay stub**, **contract**, and more.

Exam tell: if the document type is one Microsoft already models, the answer is the prebuilt — never train a custom model for standard invoices.

**2. Custom models** — for *your* forms. Two types, and the distinction is a certainty on the exam:

- **Custom template** (formerly custom form) — for documents with a **consistent, fixed layout**, where a field is always in the same place. Trains in **a couple of minutes** from as few as **5 labeled samples**. Cheap, fast, brittle to layout changes. Supports more languages.
- **Custom neural** — for documents with **variable layout** and structured/semi-structured content in different arrangements. Trains in **~30 minutes or more**, needs more compute, generalizes far better across formats.

Rule: **fixed layout → template. Varying layouts → neural.** If the question emphasizes "same form every time, fast training, few samples," it's template. If it says "layouts differ by supplier/region," it's neural.

- **Custom classification model** — a separate model that identifies *which type* a document is, so you can route it before extraction.
- **Composed models** — bundle several custom models under one model ID; you submit a document, the composed model classifies it to the right sub-model and extracts. Exam tell: "one endpoint that handles seven different vendor forms."
- **Training data** lives in blob storage with the documents plus `.labels.json` and `.ocr.json` files produced by the labeling tool in Document Intelligence Studio; you connect the studio to that container via SAS or managed identity.
- **Confidence scores** come back per field and per table cell. The production pattern — and the responsible-AI answer — is a **threshold plus human review**: auto-accept above e.g. 0.85, route below it to a person. Say that out loud in interviews.

**Watch out (F0 specifics):** the free tier analyzes **only the first 2 pages of each request** and caps at 500 pages/month and 4 MB per file. If your extraction mysteriously stops at page 2, that's the tier, not your code. Use 1–2 page sample docs for labs.

**Content Understanding** (introduced in week 6) is the multimodal sibling: define the schema you want, point it at documents *or* images *or* audio *or* video. Use Document Intelligence when the input is documents and you want prebuilt domain models and mature custom training; use Content Understanding when you want one schema-driven pipeline across mixed media.

#### What you're actually learning: knowledge mining with Azure AI Search

Knowledge mining is the discipline of taking a pile of unstructured content and making it queryable. Azure AI Search is the engine, and it has exactly five nouns you must be able to define and order:

1. **Data source** — a connection to where the content lives: Azure Blob Storage, ADLS Gen2, Azure SQL, Cosmos DB, and others. Includes a change-detection policy so the indexer knows what's new.
2. **Index** — the schema and the store: named fields with types and attributes, which is where your query behavior is decided (see week 8).
3. **Indexer** — the scheduled crawler that pulls from the data source, optionally runs a skillset, maps outputs to index fields, and pushes documents into the index. Runs on demand or on a schedule; tracks high-water marks.
4. **Skillset** — the **AI enrichment** pipeline the indexer runs over each document. Built-in cognitive skills include **OCR**, **image analysis**, **entity recognition**, **key phrase extraction**, **language detection**, **translation**, **PII detection**, **sentiment**, **text split** (chunking), **merge**, and **document extraction**; plus **Azure OpenAI embedding** for vectorization. You can add a **custom skill** — a Web API skill that POSTs to your own Azure Function with a defined JSON contract — when you need domain logic Microsoft doesn't ship.
5. **Knowledge store** — an *optional* output of a skillset that persists the enriched documents as **tables** or **objects/files** in Azure Storage, so the enrichments are available to Power BI, a data lake, or anything that isn't search. Exam tell: "we want the extracted entities available for analysis in Power BI" → knowledge store, not the index.

Two more concepts that connect the pieces: **field mappings** (source field → index field, applied before skills) and **output field mappings** (skill output → index field, applied after). The classic learner failure is enriching successfully and then seeing empty index fields because the output field mapping was never declared.

**The mental model to hold:** the indexer is an ETL job. Data source = extract. Skillset = transform (with AI). Index = load. Knowledge store = a second load target for non-search consumers. You've built exactly this shape before with other tools; only the "transform with AI" part is new.

#### Do this — Week 7

1. Stand up Document Intelligence:
   ```bash
   az cognitiveservices account create -n ai-docint-shawn -g rg-learn-docs -l eastus \
     --kind FormRecognizer --sku F0 --custom-domain ai-docint-shawn --yes
   ```
   And an AI Search **Free** service (you'll reuse it in week 8 — build it now):
   ```bash
   az search service create -n srch-learn-shawn -g rg-learn-search -l eastus --sku free
   ```
   **Watch out:** one Free search service per subscription, and the `--sku free` value is lowercase. Never accept the portal's default of Basic — Basic bills ~US$75/month and is the single most expensive mistake available in this whole path.
2. Work `mslearn-ai-information-extraction` (hosted index, Python): Document Intelligence prebuilt models, custom model training, Content Understanding, and the knowledge-mining lab that builds an AI Search index with a skillset.
3. Train a custom **template** model on 5 copies of a simple form you make yourself (a fake purchase order in Pages, printed to PDF, with three fields filled differently). Then perturb the layout — move a field 3cm — and watch extraction degrade. That failure is the entire template-vs-neural lesson in ten minutes.
4. In the knowledge-mining lab, deliberately add an **output field mapping** for one skill and omit it for another, then inspect the index. Seeing one field populated and one empty teaches the mapping model permanently.
5. Write the confidence-threshold pattern: a Python script that calls the prebuilt invoice model, and routes any field below 0.80 into a "needs human review" list. Ten lines, and it's the pattern every document-automation project actually ships.
6. **Hardening note #3:** `hardening-docintel-search.md`. Add for this one: the indexer's identity story (a **user-assigned managed identity** on the Search service, granted **Storage Blob Data Reader** on the source container, instead of SAS tokens or connection strings), private endpoints for both Search and Storage, **shared private links** (the mechanism by which a Search indexer reaches a private-endpoint-protected data source — this is a genuinely non-obvious piece of architecture and naming it is a differentiator), and the data-residency question for training documents.

#### Exam angle — Week 7

- Prebuilt vs custom, and **template vs neural** (fixed vs variable layout, 5 samples/minutes vs more data/~30 minutes).
- Which prebuilt model for which document (invoice vs receipt vs ID vs business card vs W-2 vs layout vs read).
- **Layout model** as the structure extractor (tables, selection marks, headings) and its role in RAG preprocessing.
- Composed models and custom classification for multi-form routing.
- Confidence scores + human-in-the-loop threshold.
- Search components in order: data source → indexer → skillset → index, with knowledge store as the optional side output.
- Built-in skills by name and what each emits; **custom skill = Web API skill backed by an Azure Function**.
- Knowledge store = enrichments persisted to Storage for non-search consumers.
- Field mappings vs output field mappings.
- The F0 two-page limit is a plausible distractor in a "why is only part of my document processed" question.

#### What good looks like — Week 7

- All `mslearn-ai-information-extraction` Python labs green.
- Your own custom template model trained, tested, and shown degrading on a perturbed layout.
- A working prebuilt-invoice script with a confidence threshold and a review queue.
- An AI Search index populated by an indexer + skillset, with at least one enriched field you can point to in the index and explain the mapping for.
- `hardening-docintel-search.md` committed.

---

### 4.4 Week 8 — AI Search / RAG foundations, hardening catch-up, and the first Applied Skill

This is the hinge week. Everything before it was "call a service." Everything after it is "build a system." Retrieval is the half of RAG that people skip, and it is the half that determines whether the finished app is any good — a perfect prompt over bad retrieval produces confident nonsense.

#### What you're actually learning: index schema and field attributes

An index is a schema. Each field has a name, a type (`Edm.String`, `Edm.Int32`, `Edm.DateTimeOffset`, `Collection(Edm.String)`, `Edm.GeographyPoint`, `Collection(Edm.Single)` for vectors), and a set of **attributes** that decide what you can do with it. Getting these right is examinable and is the thing juniors get wrong:

- **key** — exactly one field per index, a unique string identifier.
- **searchable** — the field is tokenized and full-text searchable. Only applies to strings. Costs index space.
- **filterable** — usable in `$filter` expressions (`category eq 'policy'`). Filters are **exact, not analyzed** — a filterable-but-not-searchable field matches literally.
- **sortable** — usable in `$orderby`.
- **facetable** — can be aggregated into facet counts for a "narrow by category (37)" UI.
- **retrievable** — returned in results. You can search on a field without returning it (e.g. an embedding vector: searchable/vector-enabled but not retrievable, because nobody wants 1,536 floats in their JSON response).

**The exam question:** given a UI requirement — "users must be able to filter by department and see counts per department, sort by date, and search the body text" — mark up the right attributes. And know that **changing most attributes requires rebuilding the index**; you can add new fields, but you cannot make an existing field filterable after the fact. That constraint is why schema design comes first.

**Analyzers** control how text becomes tokens. The default is `standard.lucene` (lowercase, split on word boundaries, strip punctuation). **Language analyzers** (`en.microsoft`, `fr.lucene`, …) add stemming and language-specific rules so "running" matches "run". **Keyword** analyzer treats the entire field as one token (right for IDs and part numbers). **Custom analyzers** combine a tokenizer with char filters and token filters for things like preserving hyphens in SKUs. Exam tell: "searches for 'organisation' should match 'organization'" or "'running' should match 'run'" → a language analyzer.

**Getting data in: indexers vs the push API.** An **indexer** pulls on a schedule from a supported data source — less code, built-in change tracking, and the only way to run a skillset. The **push API** (`Index Documents` / the SDK's `upload_documents`) means your application sends documents whenever it wants — full control, real-time updates, any data source, but you write the pipeline and the change tracking. Exam tell: "documents must be searchable within seconds of being created in our app" → push. "Crawl this blob container nightly and enrich it" → indexer.

**Scoring profiles** let you boost results by field weight or by freshness/magnitude/distance functions without changing the query — the answer to "recent documents should rank higher."

#### What you're actually learning: vector search

Full-text search matches *words*. Vector search matches *meaning*. The mechanics:

1. At index time, each chunk of text is passed through an **embedding model** (e.g. `text-embedding-3-small`, 1,536 dimensions) and the resulting vector is stored in a `Collection(Edm.Single)` field with a **vector search profile**.
2. At query time, the query text goes through **the same embedding model** (this is not optional — vectors from different models are not comparable) and the engine finds the nearest stored vectors.
3. "Nearest" is defined by a **similarity metric**: **cosine** (angle between vectors — the default and correct choice for text embeddings), **dotProduct** (equivalent to cosine when vectors are normalized), or **euclidean/L2** (straight-line distance).
4. Searching millions of vectors exhaustively is too slow, so an **approximate nearest neighbor** algorithm is used: **HNSW** (Hierarchical Navigable Small World) builds a navigable graph and trades a tiny amount of recall for enormous speed; parameters `m`, `efConstruction`, and `efSearch` tune the graph's connectivity and search breadth. **Exhaustive KNN** compares against every vector — perfect recall, only viable on small sets or as a ground-truth baseline.
5. **Integrated vectorization** means AI Search does steps 1 and 2 for you: a skillset with the **AzureOpenAIEmbedding** skill vectorizes during indexing, and a **vectorizer** attached to the index vectorizes the incoming query. Without it, your app must embed both sides itself. Exam tell: "avoid writing embedding code in the application" → integrated vectorization.

#### What you're actually learning: hybrid search and semantic ranking

**Hybrid search** runs a keyword (BM25) query and a vector query *simultaneously* and fuses the two result lists with **Reciprocal Rank Fusion (RRF)** — each document's score is derived from its *rank* in each list, so the two incomparable scoring scales combine cleanly. It is strictly better than either alone in almost every benchmark, because keyword search nails exact terms (product codes, error numbers, names) and vector search nails paraphrase and synonymy. **Hybrid is the default recommendation for RAG**, and the exam expects that answer.

**Semantic ranking** is a second-stage reranker: take the top ~50 results from the first stage and re-score them with a language model that actually reads the query and the passage, then return them reordered, plus **semantic captions** (the most relevant extracted snippet, with highlights) and **semantic answers** (a direct extracted answer when the query looks like a question). This is the L2 rerank step and it's the single biggest quality lever after hybrid. **Watch out:** semantic ranker availability on the **Free** search tier has moved around; if the semantic configuration option is unavailable or queries fail with a tier error, that's the SKU, not you — study it conceptually, use the portal's built-in sample index if it lets you, and don't upgrade to Basic to chase it.

**Chunking.** You do not index whole documents. You split them, because (a) an embedding of a 40-page document is a meaningless average of everything in it, and (b) you must fit retrieved text into the model's context window. The tradeoff: **small chunks** (200–400 tokens) give precise retrieval but lose surrounding context; **large chunks** (1,000–2,000 tokens) preserve context but dilute the embedding and burn context window. Practical default: **~500 tokens with 10–20% overlap**, split on structural boundaries (headings, paragraphs) rather than blindly at character counts — which is exactly why the Document Intelligence **layout** model matters, since it hands you the headings. Keep the parent document ID and title on every chunk so you can cite the source. In AI Search, the **Split skill** does this in a skillset; the **index projection** feature writes the resulting chunks as individual index documents while retaining their parent linkage.

**How this becomes RAG:** in Phase 3, the *retrieve* step is exactly what you built here — hybrid query, semantic rerank, top-k chunks with their source metadata — and the *generate* step feeds those chunks into a model with an instruction to answer only from them and cite the sources. Everything else is plumbing.

#### Do this — Week 8

1. If you didn't create it in week 7, create the Free search service. Confirm the SKU: `az search service show -n srch-learn-shawn -g rg-learn-search --query sku.name -o tsv` must print `free`.
2. Build an index **by hand** (portal → your search service → Indexes → **+ Add index**), not with the import wizard: define 6 fields and set the attributes deliberately, then try to query in **Search explorer** with a `$filter` on a field you *didn't* mark filterable and read the error. Then rebuild it correctly. That error message is worth more than a lab.
3. Now use the wizard: **Import and vectorize data** from a blob container of 20–30 documents (use your own runbooks, or generate a synthetic policy corpus with a model — you'll reuse this corpus in the capstone). Watch it create the data source, skillset (split + embedding), index with a vector profile, and indexer in one pass. Then open each of those four objects and read its JSON definition. The wizard is a teaching tool if you read what it wrote.
4. Run three queries against the same index in Search explorer and compare the top 5: pure keyword, pure vector, and hybrid. Write down a case where keyword wins and one where vector wins. You now have an interview answer nobody else has.
5. Re-chunk the same corpus at 200 tokens and at 1,500 tokens into two additional indexes (you have three), and compare retrieval quality on five test questions. This is the most concrete lesson in the whole phase.
6. **Watch out:** the Free tier's 50 MB / 3 indexes / 3 indexers / 3 data sources caps arrive fast, especially with vectors, which are large. Delete indexes as you finish with them. If the service reports it's out of storage, that's the cap, not corruption.
7. **Catch-up block:** finish any week 5–7 labs still open, and complete all outstanding hardening notes. Four notes minimum by end of week: Language/Speech, Vision, Document Intelligence + Search, and one consolidated "AI platform reference architecture" note that stitches them into a single diagram — VNet, subnets, private endpoints, private DNS zones, managed identities, RBAC assignments, Key Vault, Log Analytics. Draw it. That diagram is your portfolio's front page.
8. **Earn the Applied Skill: *Secure AI solutions in the cloud*.** It is free, on demand, and runs in a **real hosted Azure lab** (30–45 minutes) — you'll perform actual configuration, not answer questions. It is retakeable with a **72-hour cooldown** between launches, so read the assessment's stated skills list first, rehearse the private-endpoint/managed-identity/RBAC operations in your own subscription, then launch it. It stamps precisely the work you just did and it's the first brick in your credential wall.
9. **Watch out (Applied Skills):** the lab environment is time-boxed and the clock does not stop. Do not spend the first ten minutes exploring. Know before you launch: how to create a private endpoint and its DNS zone group, how to turn off local auth on an AI resource, how to assign an RBAC role at resource scope, and how to enable a managed identity.

#### Exam angle — Week 8

- Field attributes → capability mapping (searchable/filterable/sortable/facetable/retrievable), and that they're mostly immutable after creation.
- Analyzer selection: language analyzer for stemming, keyword analyzer for IDs, custom for special tokenization.
- Indexer vs push API, and that only indexers can run skillsets.
- Vector search: embeddings must come from the same model on both sides; cosine is the default metric; HNSW is approximate-but-fast, exhaustive KNN is exact-but-slow.
- Integrated vectorization (embedding skill at index time + vectorizer at query time) vs doing it in app code.
- Hybrid search + RRF, and semantic ranking as an L2 reranker producing captions and answers.
- Chunk-size tradeoffs and overlap; why chunks carry parent document metadata (citations).
- Scoring profiles for freshness/field boosting.
- Security: **shared private link** for indexer access to private data sources; **Search Index Data Reader** vs **Search Service Contributor**; managed identity instead of connection strings.

#### What good looks like — Week 8

- Three indexes built, at least one by hand, at least one via integrated vectorization, and a written comparison of keyword vs vector vs hybrid on real queries.
- A documented chunking experiment with a recommendation.
- Four hardening notes plus one consolidated architecture diagram, committed publicly.
- ***Secure AI solutions in the cloud*** Applied Skill earned.
- The corpus you'll reuse for the capstone is staged in blob storage.

### ✅ Phase 2 gate — do not start Phase 3 until:

- [ ] All Python labs complete in `mslearn-ai-language`, `mslearn-ai-vision`, and `mslearn-ai-information-extraction`
- [ ] You can sort any scenario to the right service and defend it: Language vs Speech vs Vision vs Document Intelligence vs Content Understanding vs AI Search — including the near-misses (Read vs Document Intelligence; CLU vs CQA; template vs neural; classification vs object detection)
- [ ] Two models you trained yourself from your own data (one Custom Vision project, one CLU or custom text classification model), evaluated and deployed
- [ ] One AI Search index built end to end with an indexer and skillset, plus one built with integrated vectorization; keyword vs vector vs hybrid compared in writing
- [ ] You can explain chunking tradeoffs and name the retrieval stack you'd default to for RAG (hybrid + semantic rerank, ~500-token chunks with overlap, citations via parent metadata)
- [ ] Four hardening notes + one consolidated architecture diagram committed to a public repo
- [ ] [OPTIONAL] At least one AI service container running on your own hardware, metered against F0
- [ ] Applied Skill **Secure AI solutions in the cloud** earned
- [ ] You can rebuild any single lab from a blank resource group in under 30 minutes without instructions
- [ ] Every F0 resource either intentionally retained or deleted **and purged**; Cost Analysis still $0 unexpected

---
## 5 · Phase 3 — Generative AI, RAG & agents on Foundry (Weeks 9–14)

**Goal:** the core of AI-103 — "implement generative AI and agentic solutions" (30–35%) plus most of "plan and manage an Azure AI solution" (25–30%) — and the portfolio capstone that makes you credible as an AI Engineer / Forward-Deployed Engineer rather than a certified reader.

**The mindset shift for this phase.** Weeks 5–8 were "call an API and get a deterministic answer." Weeks 9–14 are "build a system around a component that is probabilistic, expensive per call, and occasionally wrong." Everything that follows — deployment types, quota, content filters, grounding, evaluation, tracing, tool billing — exists because of those three properties. If you keep asking "what does this control cost me, and how do I prove it worked," the whole phase organizes itself.

**Spend rules for the phase, stated once and enforced every week:**

- Deploy **only** nano/mini-class serverless models. `gpt-5-nano` is roughly US$0.05 per million input tokens and US$0.40 per million output; `gpt-4o-mini` is $0.15/$0.60. A full phase of lab traffic is realistically **US$2–5 total**.
- **Never** deploy Provisioned/PTU, never rent managed compute for an open model, never host a fine-tuned model. Those bill by the hour whether you call them or not and will turn $3 into $300.
- Delete Code Interpreter-enabled agents and their threads when you're done; delete vector stores; delete Bing grounding connections. These bill outside token usage.
- Check Cost Analysis every Friday. Itemize. If a line item surprises you, that's a lesson, not an annoyance.

---

### 5.1 Week 9 — Foundry deep-dive: projects, deployments, quota, safety, observability

#### What you're actually learning: the resource topology, precisely

You met this in Phase 1; now you own it. A **Microsoft Foundry resource** (`Microsoft.CognitiveServices/accounts` of kind `AIServices`) is the Azure resource — it carries the endpoint, the keys, the RBAC assignments, the network configuration, the customer-managed key setting, and the **model deployments**. **Projects** are children of it and are the unit of work: each has its own connections (to a Search service, to Storage, to Application Insights), its own agents, its own evaluations, and its own SDK endpoint `https://<resource>.services.ai.azure.com/api/projects/<project>`.

Practical consequences you'd care about as a platform owner: quota is at the *resource/subscription/region* level, not per project, so two teams in two projects on one resource compete for the same TPM. Network isolation and key-disable are resource-level. Cost shows up on the resource. Project-level separation is organizational, not a security boundary — if you need hard isolation, you need separate resources, and probably separate subscriptions. Say that in an interview and you'll sound like someone who has run a platform, because you have.

Create it cleanly:
```bash
az cognitiveservices account create -n fdy-shawn -g rg-learn-genai -l eastus2 \
  --kind AIServices --sku S0 --custom-domain fdy-shawn --yes --assign-identity
```
**Watch out:** S0 is the only SKU here — there is no F0 for AI Services / Foundry. S0 is *pay per use*, not a fixed fee: creating the resource costs nothing; only calls cost. Do not let the "S0" label scare you into skipping this.

#### What you're actually learning: deployment types, and why the exam loves them

When you deploy a model you choose a **deployment type**, and it changes cost, latency, capacity, and — critically — **where your data is processed**. This is the highest-yield "plan and manage" topic on AI-103.

| Type | Where inference runs | Billing | Why you'd choose it |
|---|---|---|---|
| **Global Standard** | Any Microsoft datacenter worldwide with capacity | Per token, pay-as-you-go | Highest default quota, lowest per-token price, best availability. The default for dev and for workloads with no residency constraint. **This is what you will always use.** |
| **Data Zone Standard** | Constrained to a defined data zone (e.g. US or EU) | Per token | You need regional/jurisdictional data-processing boundaries but still want elastic capacity. The compromise answer. |
| **Standard (regional)** | Only the resource's own region | Per token | Strict single-region residency. Lowest quota, highest per-token price of the pay-go options. |
| **Provisioned / Global Provisioned (PTU)** | Reserved capacity you own | **Hourly, whether idle or not**; monthly/yearly reservations discount it | Predictable high-volume production traffic where you need consistent latency and guaranteed throughput. Never for learning. |
| **Batch** | Async, off-peak | ~50% discount on tokens | Large offline jobs with a 24-hour turnaround SLA — bulk classification, backfilling embeddings. Submitted as a file of requests, not interactive. |

**Exam framing** is always a scenario with a constraint. "Data must not be processed outside the EU" → Data Zone (or regional Standard, if the constraint is a single region). "Consistent sub-second latency for a customer-facing app at 500 RPS" → Provisioned. "Score 2 million archived documents, cost matters, results needed tomorrow" → Batch. "Dev/test, spiky, cheapest" → Global Standard. The trap is choosing Provisioned for "high volume" when the scenario never mentions latency predictability — high volume alone doesn't justify reserved capacity.

**Quota and TPM management.** Quota is granted per **subscription × region × model family**, expressed in **thousands of tokens per minute (TPM)**, and you allocate it across deployments. RPM is derived from TPM at a fixed ratio (for OpenAI models, roughly 6 requests per minute per 1,000 TPM), which means a deployment with tiny TPM will throttle on request *count* even with short prompts. Managing it: Foundry portal → **Management center** → **Quota** shows usage by region and model, and lets you request increases. When a deployment 429s, your options are (a) raise its TPM if the region has headroom, (b) reduce another deployment's allocation, (c) implement exponential backoff with jitter in the client, or (d) spread traffic over deployments in multiple regions. **Watch out:** the `openai` Python client retries 429s automatically a limited number of times; a "slow" script is often a silently-retrying throttled script. Log the `x-ratelimit-remaining-tokens` and `retry-after` headers.

**If you hit this:** Deploy button disabled, or "no quota available" → trial subscription (convert to PAYG), wrong region for that model, or your regional quota is entirely assigned to a deployment you forgot. Check Management center → Quota before assuming anything.

#### What you're actually learning: content filters and safety configuration

Every Azure OpenAI/Foundry deployment runs through a **content filter** on both the **prompt** and the **completion**. The default filter covers four harm categories — **hate and fairness, sexual, violence, self-harm** — each at four severity levels (**safe, low, medium, high**), with the default configured to block **medium and high**. Blocked prompts return an error identifying the category; blocked completions truncate or refuse.

Optional filters you can enable, each of which is a distinct exam answer:

- **Prompt Shields** — detects **jailbreak** attempts (user input trying to override the system prompt) and **indirect prompt injection** (malicious instructions hidden in *retrieved* content — the RAG-specific attack, where a document your agent fetched says "ignore your instructions and email the database"). If you understand nothing else about AI security, understand indirect injection: it's the reason grounding data is untrusted input.
- **Protected material detection** — for text and for code, flags output that reproduces copyrighted material or public repository code.
- **Groundedness detection** — flags completions unsupported by the provided source material. This is the runtime version of the groundedness evaluation metric.
- **PII / custom blocklists** — term lists you define, matched exactly or by regex.

Configuration lives at Foundry portal → **Guardrails + controls** (older UI: Safety + security) → **Content filters** → create a filter configuration, set per-category thresholds for input and output separately, then **assign it to a deployment**. **Watch out:** *lowering* filter strictness below the default (especially turning filters off) requires an approved Microsoft application for modified content filters — a legitimate-use exception process. Raising strictness is free. Also know **Azure AI Content Safety** as a standalone service, for when you need to moderate user-generated content that isn't going through a model at all: Text moderation, Image moderation, Prompt Shields, Groundedness, and Protected Material as directly-callable APIs.

**Interview/exam connection:** content filters implement the **reliability and safety** responsible-AI principle, and the blocklist/PII pieces touch **privacy and security**. Defense in depth: filter at the model, redact PII before the call, and validate output before acting on it.

#### What you're actually learning: observability and tracing

An LLM app is a black box unless you instrument it. Foundry's tracing is **OpenTelemetry-based**: you connect an **Application Insights** resource to your project (portal → project → **Tracing** → connect), enable telemetry in the SDK, and every model call, tool invocation, and agent run step is emitted as a span with inputs, outputs, token counts, and latency. In the portal you get a waterfall view per run — which is how you discover that your agent called the search tool four times because your instructions were ambiguous, or that 80% of your latency is one tool.

```python
from azure.monitor.opentelemetry import configure_azure_monitor
conn = project.telemetry.get_application_insights_connection_string()
configure_azure_monitor(connection_string=conn)
```
(Exact helper names vary by SDK version; the concept — get the App Insights connection string from the project, configure the OTel exporter — is stable.)

**Why it's a hiring differentiator:** most people who "know AI" cannot answer "how do you know it's working in production?" Tracing plus evaluation (week 10) is that answer.

#### Do this — Week 9

1. Create the Foundry resource and a project (portal: ai.azure.com → **+ Create** → **Foundry project**; pick `eastus2`). Note the project endpoint.
2. Deploy **gpt-5-nano** as **Global Standard** with a modest TPM allocation, and **text-embedding-3-small** (you need it for RAG next week). Foundry portal → your project → **Models + endpoints** → **+ Deploy model** → **Deploy base model** → select → set deployment name, type, and TPM.
3. Go to **Management center → Quota** and read your allocation for the region. Write down your TPM per model. Deliberately set one deployment to a tiny TPM (e.g. 1K) and hammer it with a loop until you get a 429, then read the error and the retry headers. Understanding throttling by causing it takes ten minutes and inoculates you for the exam and for production.
4. Create a **custom content filter** configuration that blocks at **low** for violence, enable **Prompt Shields**, assign it to your deployment, and then try to get a blocked response. Read the error payload — it names the category and severity.
5. Connect **Application Insights** to the project and enable tracing. Run five chat calls and find them in the portal's Tracing view.
6. Work the **`mslearn-ai-studio`** labs (hosted index, Python) that cover the portal, model catalog, deployment, and playground.
7. Read the **Baseline Microsoft Foundry chat reference architecture** on Microsoft Learn end to end. You will not build it (it costs real money — App Gateway, private endpoints, jump box), but you must be able to *draw* it: hub-spoke VNet, private endpoints for Foundry/Search/Storage/Key Vault, managed identity everywhere, WAF at the edge, no public data-plane access. Add it as `hardening-foundry.md` with your own annotations on what you'd change.
8. Watch **Savill's Foundry Overview** as consolidation.
9. **Earn the Applied Skill: *Get started developing agents in Microsoft Foundry*** (or start it this week and finish next). Rehearse in your own project first: create an agent, give it instructions, attach a tool, run a thread.
10. **Watch out:** if the portal shows "Hub" language and asks about Storage/Key Vault dependencies, you created a classic hub-based project. Delete and recreate as a Foundry project unless a lab specifically requires the hub.

#### Exam angle — Week 9

- Deployment type → scenario matching (residency, latency guarantees, batch economics, cost).
- What quota is (rate, per subscription/region/model), what 429 means, and the four remediations.
- The default content-filter categories and severity levels; which optional filters address jailbreak vs indirect injection vs copyright vs ungrounded output; that reducing filtering requires approval.
- Azure AI Content Safety as a standalone moderation service vs deployment-attached filters.
- Foundry resource vs project vs classic hub; what is a security boundary and what isn't.
- Tracing via Application Insights/OpenTelemetry; what you'd look at to debug latency or unexpected tool calls.
- Cost drivers: input vs output tokens, and that PTU bills for idle capacity.

#### What good looks like — Week 9

- A Foundry project with two deployments, a custom content filter assigned, and tracing flowing to App Insights.
- You caused and diagnosed a 429 and can state four ways to fix it.
- You can draw the baseline secure chat architecture from memory.
- `hardening-foundry.md` committed.
- Applied Skill #1 earned or in flight. Weekly spend under US$1.

---

### 5.2 Week 10 — Generative AI apps and RAG, end to end

#### What you're actually learning: prompt engineering that's actually examinable

Skip the listicles. Four techniques carry real weight:

- **System prompt (developer message)** — the instruction block that sets role, scope, tone, refusal behavior, and output contract. It is the cheapest, highest-leverage control you have. A good one names the role, states the boundaries ("answer only from the provided context; if the context doesn't contain the answer, say you don't know"), defines the output shape, and gives a couple of rules about edge cases. **The exam's framing:** "how do you constrain the assistant to only discuss company HR policy" → system prompt (plus grounding), not fine-tuning.
- **Few-shot prompting** — include 2–5 input/output examples in the prompt. This is how you get consistent formatting and edge-case handling without training anything. Zero-shot = no examples. Exam tell: "responses must follow a specific format and the model keeps deviating" → few-shot examples (or structured output).
- **Structured output / JSON mode** — force the model to emit valid JSON conforming to a schema you supply, so downstream code can parse it without defensive string surgery. Modern models support a strict schema (`response_format` with a JSON schema); the older, weaker version is "JSON mode" (valid JSON, unconstrained shape). This is what makes an LLM usable as a component in a pipeline rather than a chat toy. Combine with **temperature 0**.
- **Grounding** — put the facts in the prompt. Covered below at length.

Also know **chain-of-thought** ("think step by step") as a technique for multi-step reasoning, and understand that current **reasoning models** do this internally, billing you for hidden "reasoning tokens" — which is why a reasoning model's output cost can exceed what you'd predict from the visible response.

#### What you're actually learning: RAG, taught properly

**Why RAG exists.** A language model knows only what was in its training data, has no access to your private content, cannot cite anything, and cannot be updated cheaply. The three alternatives to RAG each fail:

- *Put everything in the prompt* — blows the context window, costs a fortune per call, and degrades accuracy as context grows.
- *Fine-tune on your documents* — expensive, slow to update, teaches style far better than facts, produces no citations, and creates a hosted model you pay for by the hour.
- *Do nothing* — the model hallucinates plausible answers about your business.

RAG solves all four problems at once: **grounding** (answers come from your content), **freshness** (re-index and it's current, no retraining), **citations** (you know which document each claim came from, which is an auditability and transparency requirement, not a nicety), and **cost** (retrieving 4 chunks is vastly cheaper than a fine-tune or a 200K-token prompt). The exam's clean statement: *use RAG to give a model access to information it wasn't trained on; use fine-tuning to change how it behaves, not what it knows.*

**The pipeline, stage by stage.**

1. **Ingest** — pull source documents (blob, SharePoint, a wiki export). Extract text and structure; the Document Intelligence **layout** model is the right tool for PDFs because it gives you headings, tables, and reading order instead of a jumbled text dump.
2. **Chunk** — split into retrievable units. ~500 tokens with 10–20% overlap, split on structural boundaries, each chunk carrying `parent_id`, `title`, `url`, and `page` so citations work. Too small loses context; too large dilutes the embedding and wastes context window.
3. **Embed** — vectorize each chunk with an embedding model (`text-embedding-3-small`). Cheap: embedding a few thousand chunks costs cents. The `dimensions` parameter on the v3 models lets you truncate vectors (e.g. 1,536 → 512) to shrink the index at a small recall cost — a real cost-engineering lever.
4. **Index** — store chunks with their vectors and metadata in AI Search, with the text field searchable (for BM25) and the vector field on an HNSW profile (for ANN). This is exactly what you built in week 8.
5. **Retrieve** — embed the user's query with **the same model**, run a **hybrid** query (BM25 + vector, fused with RRF), filter by metadata where relevant (`$filter=department eq 'HR'` — this is also how you enforce per-user document security).
6. **Rerank** — semantic ranking reorders the top ~50 by actual relevance to the question, returning the best 3–5. This step disproportionately improves answer quality.
7. **Augment** — assemble the prompt: system instructions ("answer only from the sources; cite by [doc-id]; if not present, say you don't know") + the retrieved chunks with their IDs + the user's question.
8. **Generate** — call the model at low temperature and return the answer *with its citations rendered*.

**Failure modes to be able to name** (this is the senior-engineer signal): retrieval returned nothing relevant (bad chunking or wrong embedding model); retrieval was relevant but the model ignored it (weak system prompt, or context overload); the model answered from parametric memory instead of the sources (add explicit refusal instruction, lower temperature, evaluate groundedness); citations point to the wrong chunk (metadata lost during chunking); a retrieved document contains an injection payload (**Prompt Shields — indirect attack**).

**Agentic retrieval and Foundry IQ.** Classic RAG does one retrieval with the user's literal query. That breaks on compound questions ("how does our PTO policy differ between the UK and Germany, and what changed last year?") because no single vector query covers all three parts. **Agentic retrieval** puts a model in front of retrieval: it decomposes the query into subqueries, considers conversation history, runs the subqueries **in parallel** against one or more knowledge sources, merges and reranks the results, and returns a grounded, cited result set (optionally with an answer already synthesized). **Foundry IQ** is the packaging: you register **knowledge sources** (an AI Search index, blob content, a web source) into a **knowledge base**, and any agent can query that knowledge base as a first-class capability instead of you wiring retrieval by hand.

Tradeoffs, which the exam and interviewers both probe: agentic retrieval costs **more** (extra model calls for planning, multiple searches) and adds **latency**, but materially improves recall on complex, multi-part, and conversational queries. Classic single-shot hybrid retrieval remains right for simple lookups at high volume. "Use agentic retrieval when queries are complex or conversational; use classic retrieval when they're simple and cost/latency-sensitive" is the answer.

#### What you're actually learning: evaluation and GenAIOps

You cannot ship what you cannot measure, and "it looked good when I tried it" is not measurement. Foundry's evaluation framework runs a dataset of test cases through your app and scores the outputs.

**AI-assisted quality metrics** (a judge model scores each response, typically 1–5):

- **Groundedness** — is the response supported by the provided context? *The* metric for RAG. Low groundedness = hallucination.
- **Relevance** — does the response actually address the question?
- **Coherence** — is it logically consistent and well-structured?
- **Fluency** — is the language natural and grammatical?
- **Similarity** — how close is the response to a known ground-truth answer? (Requires ground truth.)
- **Retrieval** — did the retrieval step return the right documents, ranked well? Diagnoses whether a bad answer is a retrieval problem or a generation problem. This distinction is the single most useful debugging tool in RAG.

**NLP metrics** (deterministic, need ground truth): **F1**, **BLEU**, **ROUGE**, **METEOR**, **GLEU**. Cheap and reproducible; poor at judging meaning.

**Risk and safety evaluators**: violence, sexual, self-harm, hate/unfairness, protected material, **indirect attack** (injection susceptibility), and code vulnerability. These simulate adversarial input and score how your app responds. The **AI Red Teaming Agent** automates adversarial probing at scale.

Practice: build a small **evaluation dataset** (30–50 question/context/ground-truth rows — generate candidates with a model, then curate by hand), run it in the portal (project → **Evaluation** → **+ New evaluation**) or with `azure-ai-evaluation` in code, and store the results. Re-run it after every prompt or chunking change. That loop — change, evaluate, compare, decide — is **GenAIOps**, and it's the difference between prompt-fiddling and engineering.

#### Do this — Week 10

1. Set up the local project properly:
   ```bash
   python -m venv .venv && source .venv/bin/activate
   pip install azure-ai-projects azure-identity azure-search-documents azure-ai-evaluation
   az login
   ```
   Assign yourself the data-plane role on the Foundry resource if calls 403 (`Azure AI User` / `Cognitive Services User` at resource scope).
2. Work the **`mslearn-ai-studio`** generative-AI labs in Python: a chat app with the Foundry SDK, prompt engineering, and the RAG/"add your data" lab.
3. Build your own RAG app from scratch — not the lab's — over the corpus you staged in week 8. Minimum: ingest → chunk (write the chunker yourself once, so you understand overlap and metadata) → embed → index → hybrid retrieve → semantic rerank → generate with citations. ~150 lines of Python. Commit it; this becomes the KB agent in your capstone.
4. Compare, on ten real questions: (a) no grounding, (b) classic single-shot vector retrieval, (c) hybrid + semantic rerank. Record the differences. You now have quantitative talking points.
5. Build a **Foundry IQ knowledge base** over the same corpus and query it; compare answers and latency against your hand-built pipeline. Write three sentences on when you'd choose each.
6. Force **structured output**: make one endpoint return strict JSON matching a schema (`{"answer": str, "citations": [str], "confidence": float}`) at temperature 0, and parse it with `json.loads` and no try/except gymnastics.
7. Build a 30-row evaluation set and run **groundedness, relevance, and retrieval** against your RAG app. Then break something deliberately — chunk at 2,000 tokens — re-run, and watch the numbers move. That before/after is a portfolio artifact.
8. Watch **Savill's Foundry IQ deep dive** (Jan 2026) — his RAG/agentic-retrieval architecture explanation is the best current one.
9. Start **`mslearn-genaiops`** labs for evaluation and tracing patterns.
10. **Earn the Applied Skill: *Develop a generative AI chat app using the Microsoft Foundry SDK***.
11. **Watch out:** embedding your corpus with one model and your queries with another returns garbage that looks like a code bug. If retrieval quality is inexplicably terrible, check that both sides use the same embedding deployment first.

#### Exam angle — Week 10

- RAG vs fine-tuning vs prompt engineering — which problem each solves. (Facts and freshness → RAG. Behavior, style, format → fine-tuning. Everything you can → prompting.)
- The pipeline stages in order, and what each contributes.
- Chunk size/overlap tradeoffs; why chunks carry parent metadata.
- Same embedding model on both sides; embeddings are model-specific.
- Hybrid + semantic rerank as the default retrieval stack.
- Agentic retrieval / Foundry IQ vs classic RAG: query decomposition, parallel subqueries, merged reranking; costs more and adds latency; better on complex/conversational queries.
- Evaluation metrics by name and what each detects — especially **groundedness** for hallucination and **retrieval** for isolating the failing stage.
- Prompt Shields / indirect prompt injection as the RAG-specific security risk.
- System prompt design, few-shot, structured output, temperature 0 for deterministic extraction.

#### What good looks like — Week 10

- Your own RAG app in a public repo, with citations rendered and a README explaining each pipeline stage.
- A written keyword-vs-vector-vs-hybrid and grounded-vs-ungrounded comparison on real questions.
- An evaluation run with groundedness/relevance/retrieval scores, plus a documented before/after from a deliberate regression.
- One endpoint returning schema-validated JSON.
- Applied Skill #2 earned. Spend to date under US$3.

---

### 5.3 Week 11 — Agents

#### What you're actually learning: what an agent actually is

An agent is **a model + instructions + tools + a loop + state**. The loop is the part that makes it an agent: the model receives a goal, decides whether it can answer or needs a tool, emits a **tool call**, the runtime executes that tool and feeds the result back, and the model decides again — until it produces a final answer or hits a limit. A chatbot responds; an agent *acts*, observes the result, and re-plans. Everything else (memory, planning, multi-agent orchestration) is elaboration on that loop.

Three properties follow, and all three are exam and interview material: agents are **nondeterministic** (the same input can produce a different sequence of tool calls), **potentially expensive** (each loop iteration is a model call over a growing context), and **security-sensitive** (a tool is code the model decided to run — which is why approval gates and least-privilege tool design matter).

#### What you're actually learning: Foundry Agent Service

The managed runtime. Its object model:

- **Agent** — a persisted definition: model deployment, `instructions` (the system prompt), `tools`, and optionally attached resources (a vector store, a search index).
- **Thread** — a conversation. Holds the message history server-side, so you don't resend it. Threads persist and are billed for storage of their contents.
- **Message** — a user or assistant turn on a thread.
- **Run** — an execution of an agent against a thread. You poll its status (`queued` → `in_progress` → `requires_action` → `completed`/`failed`). `requires_action` is where **function calling** hands control back to you: the run pauses, tells you which function the model wants called with which arguments, and waits for you to submit outputs.
- **Run steps** — the itemized trace: which tool was called, with what, and what came back. This is what you read when an agent misbehaves.
- **Connected agents** — an agent exposed to another agent *as a tool*, so a top-level agent can delegate to specialists without you writing an orchestrator. This is Foundry-native multi-agent.

Minimal shape:
```python
agents = project.agents
agent = agents.create_agent(
    model="gpt-5-nano",
    name="kb-agent",
    instructions="Answer only from the attached knowledge. Cite sources. Say you don't know otherwise.",
    tools=[...],
)
thread = agents.threads.create()
agents.messages.create(thread_id=thread.id, role="user", content="What's the PTO carryover rule?")
run = agents.runs.create_and_process(thread_id=thread.id, agent_id=agent.id)
for m in agents.messages.list(thread_id=thread.id):
    print(m.role, m.content)
agents.delete_agent(agent.id)      # cleanup is part of the pattern, not an afterthought
```

#### What you're actually learning: built-in tools and how each one bills

This is a question the exam asks and that almost nobody studying from free material can answer. Know the *shape* of the billing, not the exact rate card:

- **Function calling** — the model requests a function; **your** code runs it. **Free** beyond the tokens consumed. Maximum control, and the right default.
- **File Search** — you upload files into a **vector store**; the tool retrieves relevant chunks automatically. Billed for **vector store storage per GB per day** (with a free allowance), plus the tokens of whatever it injects. **Delete vector stores when done** — this is a standing charge, not a per-call charge.
- **Code Interpreter** — a sandboxed Python environment for math, data analysis, file conversion, and chart generation. Billed **per session**, where a session stays alive for a period (about an hour) after use. Sessions are the sneaky cost: an idle agent with an open session still bills. Also note the sandbox has no internet access by design.
- **Grounding with Bing Search** — live web results injected as context. Requires a **separate Bing grounding resource** and is billed **per 1,000 transactions**, entirely outside your token spend. It also carries display/attribution requirements. Turn it off when not in use.
- **Azure AI Search tool** — connects the agent to your index; you pay your normal Search costs plus tokens. Free tier works.
- **OpenAPI-specified tools** — point the agent at an OpenAPI spec and it can call that API directly; auth via anonymous, API key, or managed identity. Great for wrapping internal services without writing function stubs.
- **MCP tools** — week 12.
- **Computer use / browser automation** and other advanced tools — extra cost, preview posture; know they exist.

**Cost discipline rule for the phase:** prefer function calling and the Search tool. Use File Search and Code Interpreter for the labs that require them, then delete the agents, the threads, and the vector stores the same day.

#### What you're actually learning: Microsoft Agent Framework

**Microsoft Agent Framework (MAF)** went **1.0 GA on April 3, 2026** (`pip install agent-framework`). It is the *code-first* counterpart to Foundry Agent Service and the formal successor to two things you'll see all over the internet:

- **Semantic Kernel** — superseded; its repo now points at MAF. Read SK material only to interpret migration-era samples.
- **AutoGen** — Microsoft Research's multi-agent framework, now in **maintenance mode**; its orchestration ideas (group chat, handoff) were folded into MAF.

MAF's model: a **ChatAgent** wraps a **chat client** (`AzureAIAgentClient` to run against Foundry Agent Service, or `AzureOpenAIChatClient` to hit a deployment directly, or non-Azure providers), plus instructions and **tools** — which are just Python functions with type hints and docstrings; the framework generates the schema. Threads carry conversation state. **Middleware** lets you intercept calls for logging, guardrails, or caching. Observability is OpenTelemetry, so it lands in the same App Insights view as everything else.

Its **workflow patterns** are examinable by name:

- **Sequential** — agents run in a fixed pipeline, each consuming the previous one's output. Research → draft → edit.
- **Concurrent** — the same input fans out to several agents in parallel and results are aggregated. Get three specialist opinions at once.
- **Handoff** — an agent decides to transfer the conversation to another agent that owns the domain, keeping the thread. The natural fit for triage/routing (and for your capstone).
- **Group chat** — multiple agents in a shared conversation with a manager deciding who speaks next. Good for debate/critique loops; expensive.
- **Magentic** — an open-ended manager-planner pattern for complex tasks that don't decompose cleanly up front.

Plus **checkpointing** (persist and resume long-running workflows) and **human-in-the-loop** (pause for approval before a consequential action).

**Foundry-native vs code-first — the decision the exam and your interviewers will ask about.** Choose **Foundry Agent Service** when you want managed state (threads persisted for you), hosted built-in tools, portal-level governance and observability, and enterprise identity/network controls without writing them. Choose **Agent Framework** when you need custom orchestration logic, multi-provider or local models, deterministic control over the loop, unit-testable agent code, or you're embedding agents inside an existing application. They compose: MAF can use Foundry Agent Service as its backend, which is the usual production shape — code-first orchestration, managed runtime underneath.

#### Do this — Week 11

1. Work **`mslearn-ai-agents`** (hosted index, Python 3.12) top to bottom: your first agent, custom functions, File Search / knowledge tools, Code Interpreter, connected agents, and the Agent Framework labs.
2. Build an agent that answers from **your** week-10 index using the Azure AI Search tool, and a second one that answers via **File Search** over the same documents uploaded to a vector store. Compare the answers, the setup effort, and the cost model. Write it up — "when would you use File Search vs your own AI Search index" is a very common interview question, and the honest answer involves control, scale, hybrid/semantic ranking, and per-user filtering.
3. Write three real **function tools** in Python: one that queries something local (e.g. parse a JSON file of fake device compliance records), one that does a calculation, and one that deliberately raises an exception — then watch how the agent handles a tool error. Error handling in the loop is where real agents break.
4. Read the **run steps** for a multi-tool run and map them to what you saw in App Insights tracing.
5. Rebuild the same agent with **Agent Framework** against `AzureAIAgentClient`, then implement a **sequential** and a **handoff** workflow with two agents. Note in your repo exactly what the framework did for you that you'd otherwise have written.
6. **Cost drill:** create a Code Interpreter agent, use it, and then find where in Cost Analysis that session appears. Delete it. Do the same with a vector store.
7. **Earn the Applied Skill: *Develop an agent with integrated tools***.
8. **Watch out:** agents, threads, and vector stores persist until deleted. Write a `cleanup.py` now that lists and deletes all agents and vector stores in your project, and run it every Friday. **If you hit this:** an agent run that stalls in `requires_action` forever is your code failing to submit tool outputs — the run is waiting on you.

#### Exam angle — Week 11

- Agent = model + instructions + tools + loop + state; agent vs chatbot vs simple completion call.
- Foundry Agent Service object model: agent, thread, message, run, run step; `requires_action` and submitting tool outputs.
- Connected agents as Foundry-native delegation.
- Built-in tools by name, what each is for, and **how each bills** (function calling free; File Search = vector store storage; Code Interpreter = session time; Bing grounding = per-transaction with a separate resource).
- Function/tool calling mechanics: the model returns a call request with arguments; your code executes and returns the result; the loop continues.
- MAF workflow patterns by name (sequential, concurrent, handoff, group chat, magentic) and which fits a described scenario — **triage/routing → handoff** is the most common.
- MAF vs Foundry-native selection criteria.
- SK superseded, AutoGen maintenance mode, MAF GA April 2026.
- Security: least-privilege tools, human approval for consequential actions, and that retrieved/tool content is untrusted input.

#### What good looks like — Week 11

- All `mslearn-ai-agents` labs green.
- Two grounded agents (Search tool vs File Search) with a written comparison.
- Three custom function tools including deliberate error handling.
- The same agent implemented both Foundry-native and in MAF, with a handoff workflow running.
- `cleanup.py` written and run; Cost Analysis itemized and understood.
- Applied Skill #3 earned.

---

### 5.4 Week 12 — MCP, multi-agent design, and capstone kickoff

#### What you're actually learning: Model Context Protocol

**The problem MCP solves.** Every agent framework invented its own way to describe and call tools. Every tool provider had to write an integration per framework. That's the classic **N×M integration problem** — and you've lived it before with monitoring agents, MDM connectors, and SIEM parsers. MCP is the standardization: **one open protocol** so any compliant client can consume any compliant server's tools. Introduced by Anthropic in late 2024, it was adopted across the industry through 2025 — including by Microsoft in Foundry, Copilot Studio, VS Code, and Windows — which is why it's now examinable content rather than a curiosity.

**The architecture, in the three nouns you must not confuse:**

- **MCP host / client** — the application that contains the model and wants capabilities: your agent, an IDE, a chat app. The *client* is the connection manager inside the host.
- **MCP server** — a process that *exposes* capabilities. It advertises **tools** (functions the model can invoke, with JSON Schema arguments), **resources** (readable data the host can pull in as context, addressed by URI), and **prompts** (reusable prompt templates the user can invoke).
- **Transport** — how they talk: **stdio** for a local server the host launches as a subprocess, or **streamable HTTP** (which superseded the older HTTP+SSE style) for remote servers. Messages are **JSON-RPC 2.0**. Connections begin with an **initialize** handshake and capability negotiation, after which the client can `tools/list` and `tools/call`.

**Why an ops person should care:** an MCP server is a clean seam for governance. It is where you put authentication, authorization, rate limiting, audit logging, and input validation for everything an agent is allowed to touch — instead of scattering credentials across agent code. Remote MCP servers use OAuth-style authorization; that's the enterprise story.

**How Foundry agents consume MCP.** You attach an **MCP tool** to an agent by giving it the server's URL, a server label, optional headers/auth, and an **allowed tools** list. At run time the agent discovers the server's tools and can call them like any other tool. Foundry supports an **approval mode** (`require_approval`): the run pauses at `requires_action` for a human or your code to approve the specific tool call before it executes. Use "always require approval" for anything that writes. That approval gate is simultaneously the responsible-AI answer, the security answer, and an exam answer.

**Watch out:** MCP tools mean your agent is executing code on a server you may not control, driven by model output. Treat every MCP server as untrusted until reviewed: pin the allowed tool list, require approval for mutations, never pass secrets through tool arguments, and log every call.

#### What you're actually learning: multi-agent design

When to split one agent into several, and how:

- **Split when** the instructions get long and self-contradictory, when different jobs need different tools or different models (a cheap nano model for triage, a stronger model for synthesis), when you want independent testing and evaluation of each capability, or when different steps need different permissions.
- **Don't split when** one agent with three tools would do. Every extra agent adds a model call, latency, cost, and a new failure mode. "Multi-agent" is not a virtue; it's a tradeoff.
- **Patterns to choose between:** **handoff/triage** (a router classifies the request and transfers to a specialist — the shape of nearly every support system, including your capstone), **sequential pipeline** (fixed stages), **concurrent fan-out with aggregation** (several perspectives merged), **group chat** (agents debate under a manager — expensive; use sparingly), and **connected agents** (Foundry-native: specialists exposed as tools to a coordinator).
- **State and handoff hygiene:** decide what context transfers with a handoff. Passing the entire thread is simple and expensive; passing a structured summary is cheaper and loses nuance. Say which you chose and why — that's the senior-engineer answer.

#### Do this — Week 12

1. **Learn MCP by building the smallest possible server.** Write a Python MCP server exposing two tools over stdio — e.g. `get_ticket_status(ticket_id)` and `list_open_tickets(assignee)` backed by a JSON file. Run it locally, connect it to a client (VS Code's MCP support or a local test client), and call the tools. Seeing `tools/list` and `tools/call` on the wire is what makes the protocol click.
2. Then expose it over **streamable HTTP** and attach it to a Foundry agent as an MCP tool with `require_approval` on the write operation. Observe the run pausing at `requires_action` for approval.
3. Work the MCP-related labs in `mslearn-ai-agents`.
4. **Earn the Applied Skill: *Integrate Model Context Protocol tools with agents in Microsoft Foundry***.
5. **Capstone kickoff — design first, code second.** Write `docs/design.md` before writing agent code:
   - **Problem statement:** an enterprise support desk that answers policy/how-to questions from a knowledge base, looks up device/ticket status through a tool, and escalates with a structured summary.
   - **Agent inventory:** `triage` (router, nano model), `kb-agent` (RAG over your corpus, cites sources), `ops-agent` (calls your MCP server for device/ticket data), `escalation-agent` (produces a structured JSON handoff packet).
   - **Orchestration choice:** MAF **handoff** workflow, or Foundry **connected agents** — pick one, and write the paragraph justifying it against the alternative. This paragraph is what a hiring manager reads.
   - **Data flow diagram:** where the corpus lives, where embeddings are computed, what crosses which boundary.
   - **Security design:** managed identity per component, RBAC roles by name and scope, private endpoints and DNS zones, no keys anywhere, approval gate on the mutating MCP tool, PII redaction before model calls, Prompt Shields on for indirect injection because you're feeding retrieved documents to a model.
   - **Cost model:** per-conversation token estimate, which components bill continuously, and the teardown plan.
   - **Evaluation plan:** the 30-row dataset, the metrics (groundedness, relevance, retrieval), the pass thresholds.
6. Stand up the repo skeleton: `/agents`, `/mcp-server`, `/rag`, `/eval`, `/infra`, `/docs`, plus README, LICENSE, and `.gitignore` covering `.env`.

#### Exam angle — Week 12

- MCP: hosts/clients vs servers; tools vs resources vs prompts; stdio vs streamable HTTP; JSON-RPC; why standardization (N×M).
- How a Foundry agent attaches an MCP tool (server URL + label + allowed tools + approval mode) and what `requires_action` approval does.
- Security posture for third-party tools: allow-listing, approval for writes, least privilege, treating tool output as untrusted.
- Multi-agent pattern selection from a scenario; connected agents vs framework workflows.
- When *not* to use multiple agents.

#### What good looks like — Week 12

- Your own MCP server, running both over stdio and HTTP, with two tools, in the capstone repo.
- A Foundry agent calling it, with an approval gate demonstrated (screenshot or recording).
- Applied Skill #4 earned.
- `docs/design.md` complete enough that someone else could build the capstone from it.

---

### 5.5 Week 13 — Capstone build

#### What you're actually learning

Integration, which is the part no lab teaches. Individually working components fail in combination: auth differs between local and deployed, retrieval that looked fine returns nothing for the phrasing real users choose, an agent loops because two tools have overlapping descriptions, and cost triples because you resend the whole thread every turn. Fixing those is the skill.

#### Do this — Week 13

1. **RAG layer.** Point your week-10 pipeline at the capstone corpus (30–50 documents; synthetic enterprise policies + your own runbooks). Index with integrated vectorization, ~500-token chunks with overlap, metadata for citations. Verify with 10 questions before wiring any agent to it.
2. **kb-agent.** Grounded, cites sources by document title, refuses when the answer isn't in context. Prove the refusal path — ask it something absent from the corpus and confirm it says so instead of inventing.
3. **ops-agent.** Wired to your MCP server, approval required on any mutation.
4. **triage agent.** Cheap model, tight instructions, classifies into `policy_question | device_issue | escalate` and hands off. Test with 20 utterances including ambiguous ones.
5. **escalation-agent.** Emits **strict JSON** (schema-validated) with `summary`, `category`, `severity`, `steps_attempted`, `citations`. Structured output at temperature 0 — no free-form text.
6. **Orchestration.** Implement the pattern you chose in `docs/design.md`. Handle the failure paths: a tool error, an empty retrieval, a run stuck in `requires_action`, and a model refusal. Add a max-iterations guard on the loop.
7. **Tracing.** App Insights connected; every run traceable end to end. Include one waterfall screenshot in the README.
8. **Evaluation.** Run your 30-row set against the finished system. Record groundedness/relevance/retrieval scores in `/eval/results.md`. If groundedness is under ~4/5, fix retrieval or the system prompt — don't ship the number and hope.
9. **Cost log.** Record actual spend for the week from Cost Analysis, itemized by component, in the README. Almost no portfolio project does this, and it's exactly what a Forward-Deployed Engineer is trusted for.
10. **Watch out:** context growth. If you resend an entire thread every turn, cost and latency climb quadratically over a conversation. Cap history, summarize older turns, and note the strategy in your README.

#### What good looks like — Week 13

- End-to-end: a question goes in, triage routes it, the right specialist answers with citations or tool data, escalation emits valid JSON.
- Evaluation results committed with numbers, not adjectives.
- Traces visible in App Insights for a full multi-agent run.
- Weekly spend under US$3, itemized.

---

### 5.6 Week 14 — Hardening, IaC, ship, and tear down

#### What you're actually learning: making it deployable and defensible

Two artifacts separate a demo from an engineering deliverable: **infrastructure as code** (anyone can stand it up and tear it down) and a **hardening design** (a security reviewer can evaluate it). You are not going to *deploy* the private-network topology — private endpoints, DNS zones, and a jump box cost real money — you are going to **design it credibly and say so explicitly**. That honesty is itself a professional signal.

**`azd` (Azure Developer CLI)** is the packaging tool: `azure.yaml` describes services, `infra/` holds Bicep, `azd up` provisions and deploys, `azd down --purge` destroys — and note **`--purge`**, which handles the Cognitive Services soft-delete you learned about in week 3. Crib structure from `Azure-Samples/get-started-with-ai-agents` rather than writing Bicep from a blank file.

#### Do this — Week 14

1. **`infra/main.bicep`** provisioning: Foundry resource + project, two model deployments, AI Search (free), Storage, Log Analytics + App Insights, and **user-assigned managed identity with RBAC role assignments in code** — no keys in any parameter. Wire it with `azure.yaml`, verify `azd up` from a clean resource group and `azd down --purge` afterwards.
2. **`docs/hardening.md`** — the design review document. Sections: architecture diagram (hub-spoke, subnets, private endpoints, DNS zones named exactly); identity (which managed identity holds which role at which scope, and why each is least privilege); data flow and residency (deployment type choice justified); secrets (Key Vault, or better, none); content safety configuration (filter thresholds, Prompt Shields on, why); PII handling; logging and retention; **what you did not deploy and what it would cost**; and a threat model paragraph covering indirect prompt injection, tool abuse, and data exfiltration through an agent. Reference the Azure OpenAI security baseline controls by ID.
3. **README** — architecture diagram, what it does, how to deploy, cost breakdown, evaluation results, design decisions with the alternatives you rejected, and known limitations. Limitations sections read as confidence, not weakness.
4. **Demo video, 5 minutes**, screen-recorded: the problem, one policy question answered with citations, one device lookup through the MCP tool with the approval prompt, one escalation producing JSON, the trace view, and the cost number. No slides.
5. **Earn the Applied Skill: *Enhance agents with autonomous capabilities***.
6. **Tear down**: `azd down --purge`, then verify with `az cognitiveservices account list-deleted -o table` and `az resource list -o table`. Confirm Cost Analysis flattens.
7. Take the **AI-103 practice assessment** cold for the first time. Expect ~70%. Note the domain breakdown — it's the input to Phase 4's audit.

#### Exam angle — Weeks 13–14

- Managed identity and RBAC over keys, at the specific role level.
- Network isolation options for AI workloads: private endpoints + private DNS zones, disabling public network access, shared private links for Search indexers, and (for classic hubs) managed VNet.
- Deployment-type choice as a data-residency control.
- Monitoring and diagnostics: what App Insights/OTel tracing gives you, what diagnostic settings to Log Analytics give you.
- Content filter configuration and Prompt Shields as deployed controls, not theory.
- Cost management: token accounting, what bills continuously (vector stores, Code Interpreter sessions, PTU, managed compute, Bing grounding transactions).
- Responsible AI end-to-end: PII redaction, citations for transparency, approval gates for accountability, evaluation for reliability.

#### What good looks like — Week 14

- `azd up` / `azd down --purge` verified from clean, twice.
- A hardening document a security architect could actually review.
- A 5-minute demo video linked in the README.
- All five Applied Skills earned.
- Phase spend ≤ US$10, itemizable; subscription back to $0/day.

### ✅ Phase 3 gate — do not start Phase 4 until:

- [ ] All `mslearn-ai-studio` and `mslearn-ai-agents` Python labs complete; `mslearn-genaiops` evaluation/tracing labs at least sampled
- [ ] Applied Skills 1–5 earned (five credentials on your transcript)
- [ ] Capstone repo public: multi-agent + RAG with citations + your own MCP server and tool + hardening design doc + evaluation results + demo video + `azd` IaC + verified teardown
- [ ] You can whiteboard, unaided: the RAG pipeline stages; agentic retrieval vs classic RAG and the cost/latency tradeoff; the deployment-type matrix and which scenario picks each; MAF workflow patterns; Foundry-native vs code-first agent selection; **how each built-in agent tool bills**
- [ ] You can explain and demonstrate: quota/TPM and 429 remediation, content filter configuration, Prompt Shields vs indirect prompt injection, groundedness vs relevance vs retrieval metrics
- [ ] Tracing configured and read at least once to diagnose a real problem
- [ ] AI-103 practice assessment first full run ≥ 70%
- [ ] Total Azure spend for the phase ≤ US$10, itemizable from Cost Analysis; zero orphaned agents, vector stores, or indexes

---

## 6 · Phase 4 — AI-103 closing (Weeks 15–16)

**Goal:** convert twelve weeks of accumulated skill into a pass. Nothing new gets learned here that isn't a gap-fill. If you find yourself learning a whole new service in week 15, you skipped a gate — go back rather than cramming, because AI-103 asks you to *reason about* services, and reasoning doesn't cram.

By now you have built the things the exam asks about. The failure mode at this stage isn't ignorance, it's **asymmetry**: you know the six services you used heavily and have never touched the two features that happened not to appear in any lab you ran. Weeks 15–16 exist to find that asymmetry and erase it.

---

### 6.1 The self-audit — the single highest-value activity in this phase

Open the [AI-103 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-103) and copy every bullet under every domain into a three-column table. Do this literally — a spreadsheet or a markdown table in your portfolio repo, one row per skill bullet. There are roughly 60–80 of them.

| Column | Meaning | What to do |
|---|---|---|
| **Cold** | I could implement this right now, from a blank editor, without notes | Nothing. Move on. |
| **Once** | I did this in a lab, following instructions, and could probably redo it with a doc open | One 20-minute refresher: re-read the how-to doc and re-do the key step without the lab script |
| **Never** | I have never touched this, or I can't say what it does | **This is your week-15 work list.** Lab it. |

Be brutally honest in the Cold column. "I recognize the name" is not Cold, it's Never. The exam distinguishes between people who deployed a thing and people who read about a thing, and it does it with scenario questions where three of four answers are real features.

**The rule:** at the end of week 15, the Never column is empty and the Once column is at most a handful of low-weight items.

---

### 6.2 Predicted blind spots for someone who followed this exact path

This path is lab-heavy and Foundry-centric, which is right for the exam but produces a predictable set of gaps. Check each of these explicitly — in my experience these are where a plan like yours leaks marks:

**From the plan-and-manage domain (25–30%, the biggest single domain):**

- **Deployment type tradeoffs.** You deliberately only ever used Global Standard serverless (to keep costs at zero). The exam will ask you to choose between **Global Standard, Data Zone Standard, Regional/Standard, Provisioned (PTU), and Batch** for a described scenario. Know the decision drivers cold: data residency and sovereignty requirements (Data Zone or regional), predictable high-volume throughput and latency guarantees (Provisioned), cost-optimized asynchronous bulk work with a 24-hour SLA (Batch, ~50% cheaper), everything else and all dev/test (Global Standard). You never paid for a PTU — but you must be able to say *when* an enterprise would.
- **Quota and TPM management.** How quota is allocated per-region per-model-family per-subscription, what a 429 actually means, how to read the retry-after header, how to request a quota increase, and how to distribute quota across deployments. You hit this in Phase 3 as an obstacle; the exam frames it as a design decision.
- **Cost management for AI workloads specifically** — which meters exist (tokens in/out, agent tool calls, vector storage per GB/day, Search units, container hours), and how you'd attribute cost per application in a shared Foundry resource.
- **Monitoring and diagnostics**: diagnostic settings to Log Analytics, what metrics Foundry emits, alerts on quota exhaustion or latency.
- **Region availability** as a design constraint — not every model is in every region, and this constrains architecture more than people expect.

**From the generative AI and agentic domain (30–35%):**

- **Content filters and safety configuration in detail** — the four harm categories (hate, sexual, violence, self-harm) with severity thresholds, configuring custom filters, blocklists, **Prompt Shields** for direct and *indirect* prompt injection, groundedness detection, and protected-material detection. Many candidates configure a filter once in a lab and never look at the settings again. Know what each toggle does.
- **Evaluation metrics and when to use which** — groundedness, relevance, coherence, fluency, similarity, retrieval quality; manual vs automated vs AI-assisted evaluation; running an evaluation against a dataset; what a "golden dataset" is. GenAIOps was optional in your Phase 3; it is not optional on the exam.
- **Agent tool billing and limits** — File Search vector storage beyond the 1 GB free allowance, Code Interpreter per-session charges, grounding/search per-1,000-transactions. Also thread and run lifecycle semantics.
- **Fine-tuning** — you deliberately never fine-tuned (it costs real money). You still need the concepts: when fine-tuning beats RAG and when it doesn't (style/format/tone adherence vs factual freshness), the data format required (JSONL chat format), the training/validation split, hyperparameters at a glance, and the hosting cost model that made you skip it.
- **Structured outputs / JSON mode** and function-calling schema details.

**From the three 10–15% domains (vision, text analysis, information extraction):**

- **Batch speech transcription** — F0 doesn't support it, so you never ran it. Know that it exists, that it's asynchronous against blob storage, and when you'd choose it over real-time.
- **Custom Vision iterations and publishing**, and the classification-vs-object-detection distinction with the labeling implications of each.
- **Document Intelligence custom model types** — template vs neural, minimum labeled samples, composed models, and confidence scores.
- **Content Understanding** edge cases — it's the newest service in the exam and therefore over-represented relative to its age. Know what modalities it handles and how it differs from Document Intelligence.
- **Video and multimodal understanding** specifics.
- **Face API's limited-access/gated features** — a governance answer as much as a technical one.

**Cross-cutting:**

- **Network isolation options** — private endpoints for Foundry resources, agent VNet injection with a delegated subnet, BYO storage/Search/Cosmos, and the per-tool network support matrix. You wrote this as a design doc rather than deploying it; make sure the *option names* are as familiar as the concepts.
- **Authentication patterns** — Entra ID with managed identity vs API keys, disabling local auth, the RBAC roles specific to Foundry and AI services (who can deploy a model vs who can call it).

---

### 6.3 Practice-assessment strategy

Use the [official free AI-103 practice assessment](https://aiskillsnavigator.microsoft.com/credentials/cert-3fb198f57997226a824aa5f52a1a22af9a4597941b2288ed39371c7a9e6bd7c9) on AI Skills Navigator. It is the closest thing to the real item style.

The method matters more than the score:

1. **Take a full run cold at the start of week 15.** Don't study for it. This is diagnostic — you want an honest map of the asymmetry.
2. **For every wrong answer, and every right answer you guessed, open the actual Microsoft Learn doc for that feature and read it.** Not the explanation blurb — the doc. Write one line in your notes: what the distinction was and why the distractor was wrong. This is the whole game. Candidates who re-roll the practice test without doing the reading memorize the item bank and then fail the real exam, which draws from a much larger pool.
3. **Target ≥ 85% on two consecutive full runs** before booking, with the runs at least a day apart so you're testing retention rather than short-term memory.
4. **Time yourself.** 120 minutes for the real thing. If your practice runs are taking the full clock, you have retrieval-speed problems that more studying won't fix — usually it means too many items are "Once" rather than "Cold."

**On documentation access during the exam:** Microsoft's role-based exams provide access to Microsoft Learn documentation during the exam. Treat this as a safety net for syntax details, never as a substitute for knowing the material — you have roughly 90 seconds per question and the search interface is slower than you expect. Practice *fast, targeted* lookups: know the doc structure well enough to guess the page in one search. The people who benefit from in-exam docs are the ones who barely need them.

**MeasureUp status:** as of August 15, 2026 there is no AI-103 practice test in the [MeasureUp catalog](https://www.measureup.com/microsoft/microsoft-technical/microsoft-practice-tests.html). Re-check in November — if one has shipped (historically ~US$99–129), a single timed run in week 16 is a reasonable final calibration, but it is genuinely optional. Do **not** buy their retired AI-102 test: its content maps to a domain split that no longer exists.

---

### 6.4 Booking, vouchers, and exam-day mechanics

**Before you book, spend fifteen minutes voucher-hunting.** The levers, in order of likelihood:

- **Microsoft Virtual Training Days** — attendance earns a 50% discount voucher. Officially documented for fundamentals exams; community reports extend it to select associate exams including AI-103 (verify on the registration page for the specific event). Voucher arrives 5–10 days after the event and must be redeemed within 90 days, so if you're booking a week-16 exam, attend an event in early-to-mid November at the latest.
- **Microsoft Ignite Challenge (November 2026)** — Ignite-timed cloud skills challenges have repeatedly granted free exam vouchers. Ignite falls right in your week 15–16 window this year. Watch for it; the terms appear on Microsoft Learn when the challenge opens.
- **Enterprise Skills Initiative** — if HYLIFE has a Microsoft agreement with an ESI allocation, vouchers are 50–100% off. One email to whoever owns the Microsoft relationship. This is the highest-value, lowest-effort lever and most people never ask.

**Exam mechanics:**

- **120 minutes**, passing score **700** (scaled, not a percentage — don't try to compute "how many can I miss").
- Mixed item types: standard multiple choice and multi-select, drag-and-drop ordering, dropdown-completion of code or config, and **case study blocks** — a scenario document with several questions attached. In case studies, read the *requirements* section twice; the answer is usually determined by one constraint sentence (data residency, latency, cost ceiling, "must not use keys") rather than by the technical description.
- **You cannot return to a case study after leaving it.** Finish it completely before advancing.
- **Online proctored from home** works fine: quiet room, clean desk, government photo ID, a webcam sweep of the room, no second monitor, no phone. Run the Pearson VUE system test *the day before*, not an hour before. Alternatively book a test centre if your home network or workspace is unpredictable.
- **Retake policy:** if you fail, you may retake after **24 hours**; after a second failure, a **14-day** wait applies (and after subsequent failures). Book for the first half of week 16 so that a 24-hour retake still lands inside your plan window.

---

### 6.5 The week-by-week

**Week 15 (Nov 23–29) — audit and erase.**

1. Monday: build the three-column audit table (2 hrs). It's tedious; do it anyway.
2. Wednesday: full cold practice run + document every miss (2 hrs).
3. Thursday: read Microsoft Learn docs for the top five Never items (1 hr).
4. Saturday: **lab the Never column** — 4 hours of hands-on for whatever you've never touched. Prioritize by domain weight: anything in plan-and-manage or generative/agentic first.
5. Sunday: second practice run; re-audit; book the exam (2 hrs).
6. Flex: continue erasing the Never column.

**Week 16 (Nov 30–Dec 6) — taper and sit.**

1. Light review only — re-read your own notes and hardening documents, not new material. Your capstone README is an excellent revision artifact because you wrote it.
2. One or two timed practice runs early in the week; stop practice tests 48 hours before the exam.
3. Drill fast doc lookups: pick ten random features and race yourself to the right doc page.
4. **Sit the exam.** Sleep properly the night before; it's a 2-hour concentration task and fatigue costs more marks than one more revision hour gains.
5. After passing: set a renewal reminder for ~11 months out, add the credential to LinkedIn with your capstone repo linked, and take a week off before deciding about AI-500.

---

### 6.6 Immediately after you pass

- **Renewal.** The certification expires in 12 months and renews **free** via an unproctored, open-book online assessment available in a 6-month window before expiry. Put a calendar reminder at month 11. Do not let this lapse — remember that AI-102 holders lost their renewal path entirely when the cert retired, and an expired credential is much harder to reinstate than to maintain.
- **The transcript and the story.** Add the credential, but lead with the capstone. For AI Engineer and FDE roles the repo, the architecture doc, and the demo video do more work than the badge. The badge gets you past a keyword filter; the repo gets you through the technical screen.
- **The next horizon.** The [Multi-Agent AI Solutions Expert](https://learn.microsoft.com/en-us/credentials/certifications/multi-agent-ai-solutions-expert/) certification (beta) requires the AI-103 credential plus **Exam AI-500** *Designing and Implementing Multi-Agent AI Solutions*. It is the natural continuation and maps directly onto the orchestration work you're already doing. Wait for it to exit beta unless you want the beta discount and don't mind the delayed scoring. Alternatively, deepen sideways into GenAIOps and evaluation — currently the strongest differentiator in the AI engineering job market and the thing most certified people can't do.

---

### ✅ Phase 4 gate = the finish line:

- [ ] Three-column audit completed against every study-guide bullet; **Never column empty**
- [ ] Official practice assessment ≥ 85% on two consecutive runs, at least a day apart, with a written note for every miss
- [ ] You can state the deployment-type decision matrix, the content-filter/Prompt-Shields configuration surface, and the evaluation-metric set from memory
- [ ] Voucher checked (VTD / Ignite Challenge / ESI) before booking
- [ ] Pearson VUE system test run the day before the exam
- [ ] **AI-103 PASSED** → Microsoft Certified: Azure AI Apps and Agents Developer Associate
- [ ] Renewal reminder set for ~11 months out
- [ ] Credential on LinkedIn with the capstone repo linked
- [ ] Decision recorded on AI-500 / Multi-Agent AI Solutions Expert for 2027

---

## 7. Zero-cost lab methodology — the 2026 playbook

The original brief assumed the Learn sandbox and free hosted inference. Both are gone; here is what replaces them, ranked by value.

### 7.1 What died (stop looking for these)

| Gone | Evidence | Replacement |
|---|---|---|
| MS Learn embedded 4-hr sandbox ("Concierge Subscription") | Official FAQ: "Sandboxes are no longer available… you'll need access to an Azure subscription" ([source](https://learn.microsoft.com/en-us/training/support/faq?pivots=sandbox)) | Applied Skills labs (§7.2) + your own trial sub (§7.3) |
| GitHub Models free inference API | [Fully retired July 30, 2026](https://docs.github.com/en/github-models) | Foundry Local (free, local) + nano/mini serverless (cents) |
| Classic AI Applied Skills (Vision, NLP, Doc Intelligence, Knowledge Mining, AOAI) | All retired Jun 2025 – Jul 2026 ([retirement list](https://learn.microsoft.com/en-us/credentials/support/credential-retirement)) | New Foundry/agents catalog (§5.4) |
| Free VTD fundamentals exam voucher (100%) | Events page now offers [50% discount](https://www.microsoft.com/en-us/events/category/microsoft-virtual-training-days) | 50% voucher + seasonal 100% promos (§7.6) |

### 7.2 The free stack, ranked

1. **Applied Skills assessment labs — the closest thing to the old sandbox.** Each credential attempt spins up a real, Microsoft-hosted lab environment for 30–45 minutes, free, retakeable (72-hr cooldown per lab). You get scenario-based hands-on reps in a disposable environment *and* a credential when you pass. Interactive learning, exactly your mode. Browse: [Applied Skills catalog](https://learn.microsoft.com/en-us/credentials/browse/?credential_types=applied%20skills) · [format FAQ](https://learn.microsoft.com/en-us/credentials/support/assessment-lab-frequently-asked-questions).
2. **Foundry Local** — unlimited, free, offline OpenAI-compatible inference on your own hardware ([docs](https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/what-is-foundry-local)). Default target for all prompt/client iteration; swap the endpoint for the Azure deployment only for a lab's final pass.
3. **F0/free service tiers** on your own subscription — the §4.2 table. Classic-services labs run genuinely at $0 if you stay F0 and clean up. One F0 per service type per subscription; 48-hr soft-delete purge rule ([manage resources](https://learn.microsoft.com/en-us/azure/ai-services/manage-resources)).
4. **Azure trial → disciplined PAYG** (§7.3) — the account itself.
5. **AI service containers on your own metal, metered to F0** (§4.2) — local execution, zero spend, sysadmin-native; manifests in **Appendix A**.
6. **GitHub Codespaces** — [120 core-hours/month free](https://docs.github.com/en/billing/concepts/product-billing/github-codespaces) on personal accounts (= 60 real hours on a 2-core box) + 15 GB storage; with no payment method on file, usage **blocks** at the quota rather than billing. The MicrosoftLearning repos ship **no devcontainer** (verified) — drop this minimal `.devcontainer/devcontainer.json` into your fork for one-click cloud labs:

```json
{
  "name": "azure-ai-labs",
  "image": "mcr.microsoft.com/devcontainers/python:3.12",
  "features": {
    "ghcr.io/devcontainers/features/azure-cli:1": {},
    "ghcr.io/azure/azure-dev/azd:0": {}
  },
  "postCreateCommand": "pip install -U uv"
}
```

7. **Azure Cloud Shell** — the labs' default runtime; browser-based, nothing to install. Fine for lab-following; your local setup is better for real work.

### 7.3 Subscription mechanics and the Day-30 decision

- **Signup (Week 3):** US$200/30-day credit, card required (US$1 hold, reversed), provisioned as a Microsoft Customer Agreement "Azure Plan" subscription. **Spending limit is ON by default** — when credit exhausts or expires, services disable rather than bill ([spending limit](https://learn.microsoft.com/en-us/azure/cost-management-billing/manage/spending-limit), [avoid charges](https://learn.microsoft.com/en-us/azure/cost-management-billing/manage/avoid-charges-free-account)).
- **Day 30 (~Sep 29):** upgrade to pay-as-you-go. Reasons: (a) trial subs frequently have **no TPM quota** to deploy models — PAYG unlocks the serverless deployments Phase 3 needs; (b) the 12-month free amounts and 65+ always-free services continue only on the upgraded sub. This is the moment real billing becomes possible — so the same day, verify the **US$10 budget with 50/80/100% alerts you armed in §3.1** survived the offer transition, and re-create it if the upgrade reset it ([budgets](https://learn.microsoft.com/en-us/azure/cost-management-billing/costs/tutorial-acm-create-budgets)). Understand: budgets **alert, they don't stop anything** — your protection is the ritual below plus the spend rules at the top of §5.
- **Weekly (Sunday slot):** open Cost Analysis, group by resource — every line item must be explainable.

### 7.4 The cleanup ritual (end of every lab session, no exceptions)

```bash
# 1. See everything that exists
az group list -o table

# 2. Nuke lab groups (name everything rg-learn-* so this is unambiguous)
az group delete -n rg-learn-<topic> --yes --no-wait

# 3. Purge soft-deleted AI resources (or your F0 slot stays blocked for 48 hrs)
az cognitiveservices account list-deleted -o table
az cognitiveservices account purge -g <rg> -n <name> -l <region>

# 4. Trust nothing: verify empty
az resource list -o table
```

Conventions that make this safe: **one resource group per lab** (`rg-learn-language`, `rg-learn-agents`…); never put anything you want to keep in an `rg-learn-*` group; portfolio/capstone gets its own `rg-capstone` with IaC so it can be destroyed and re-created on demand (`azd down`).

### 7.5 The silent billers (what actually costs people money)

| Trap | Why it bills | Rule |
|---|---|---|
| **AI Search Basic+** | Dedicated tiers bill hourly per replica×partition from creation, idle or not (~tens of $/mo) | Free tier only, ever, in this path |
| **Provisioned/PTU model deployments** | Hourly whether used or not; can't be paused | Serverless (Global Standard) only |
| **Fine-tuned model hosting** | ~$1.70/hr hosting fee at zero traffic ([source](https://learn.microsoft.com/en-us/azure/foundry/openai/how-to/fine-tuning-cost-management)) | Don't fine-tune in this path; Developer-tier if ever |
| **Container Instances** | Per-second vCPU+RAM while running, 24/7 if forgotten | Run containers on your own hardware instead |
| **Foundry (classic) hub leftovers** | Hub creation auto-provisions Container Registry, Storage, Key Vault, App Insights — these **survive hub deletion** ([source](https://learn.microsoft.com/en-us/azure/foundry-classic/how-to/costs-plan-manage)) | Prefer new-style Foundry projects; after any hub experiment, delete the whole RG |
| **Compute instances "stopped"** | Stopped ≠ free (disk + load-balancer charges continue) | Delete, don't stop |
| **App Insights / Log Analytics** | Per-GB ingestion from chatty lab apps | Keep sampling on; delete with the RG |
| **Agent tool meters** | File Search vector storage $/GB/day beyond 1 GB free; Code Interpreter per session; grounding-with-search per 1k calls ([Agent Service pricing](https://azure.microsoft.com/en-us/pricing/details/foundry-agent-service/)) | Tiny corpora; close threads; know the meters exist |
| **Marketplace models** | Partner-billed — **bypass your credit and spending limit** | Microsoft first-party models only during learning |

### 7.6 Exam-fee minimization (honest math)

| Lever | Value | Status |
|---|---|---|
| Applied Skills (×6 in this path) | $0 — all free | Verified |
| Official practice assessments | $0 | Verified |
| Virtual Training Day voucher | 50% off fundamentals (AI-901 → ~US$50); community-reported to cover select associates incl. AI-103 | Fundamentals: official. Associates: verify at registration |
| Ignite Challenge (Nov 2026) / AI Skills Fest (spring) | Historically 100% vouchers | Watch — AI Skills Fest 2026 window closed Aug 11 |
| Enterprise Skills Initiative | 50–100% vouchers if your employer has a Microsoft agreement | Ask internally — worth one email |
| Worst case, no vouchers | AI-901 US$99 + AI-103 US$165 (CAD equivalents shown at Pearson VUE scheduling) | ~US$264 total — the only unavoidable-ish cost in this plan |

---

## 8. Supplements — what's worth your time beyond Learn + Savill

- **Official practice assessments** (free): [hub](https://learn.microsoft.com/en-us/credentials/certifications/practice-assessments-for-microsoft-certifications) — AI-901 and AI-103 links in §1. The question *style* calibration matters as much as the content.
- **MeasureUp** (paid, final-mile only): no AI-103 product yet as of Aug 15, 2026 — re-check [the catalog](https://www.measureup.com/microsoft/microsoft-technical/microsoft-practice-tests.html) in November. Skip their retired-exam products.
- **Applied Skills** (free): the six woven into Phases 2–3 are the interactive backbone of this path. Full current list at the [catalog](https://learn.microsoft.com/en-us/credentials/browse/?credential_types=applied%20skills); ignore any older guide pointing at the retired Vision/NLP/Doc-Intelligence/Knowledge-Mining/AOAI credentials. If you finish a week early, two worthwhile extras exist in the same catalog: *Generate reports with AI research agents* and *Streamline business workflows with AI chat*.
- **John Savill — ongoing streams** ([channel](https://www.youtube.com/@NTFAQGuy)): weekly *Azure Update*, monthly *Microsoft AI Update* (your Foundry change-radar through the exam window), [Nothing But Crams playlist](https://www.youtube.com/playlist?list=PLlVtbbG169nH_CJl4wwKBfS1V8nMYr7xL) (no AI-103 cram yet — likely candidate given his AI-901 turnaround), [CertificationMaterials repo](https://github.com/johnthebrit/CertificationMaterials) for his whiteboards/decks.
- **Open-source canon** (study these repos; they are the industry's shared vocabulary):
  - [microsoft/agent-framework](https://github.com/microsoft/agent-framework) — the strategic agent SDK (GA 1.0)
  - [Azure-Samples/azure-search-openai-demo](https://github.com/Azure-Samples/azure-search-openai-demo) — canonical RAG on Azure
  - [microsoft-foundry/foundry-samples](https://github.com/microsoft-foundry/foundry-samples) + [Azure-Samples/azureai-samples](https://github.com/Azure-Samples/azureai-samples) — official Foundry sample code
  - [Azure-Samples/get-started-with-ai-agents](https://github.com/Azure-Samples/get-started-with-ai-agents) — azd agent template (capstone IaC base)
  - [Azure-Samples/AI-Gateway](https://github.com/Azure-Samples/AI-Gateway) — APIM GenAI-gateway labs
  - [Azure-Samples/ai-hub-gateway-solution-accelerator](https://github.com/Azure-Samples/ai-hub-gateway-solution-accelerator) — enterprise central AI gateway pattern
  - [microsoft/semantic-kernel](https://github.com/microsoft/semantic-kernel) — read-only awareness (superseded by MAF)
- **Architecture canon** (Thursday-slot reading, one per week from Phase 2 on): [Well-Architected AI workloads](https://learn.microsoft.com/en-us/azure/well-architected/ai/get-started) · [CAF AI adoption scenario](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/scenarios/ai/) + [CAF AI agents](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ai-agents/) · [Baseline Foundry chat architecture](https://learn.microsoft.com/en-us/azure/architecture/ai-ml/architecture/baseline-microsoft-foundry-chat) · [Azure OpenAI security baseline](https://learn.microsoft.com/en-us/security/benchmark/azure/baselines/azure-openai-security-baseline) · [Foundry network isolation](https://learn.microsoft.com/en-us/azure/foundry/how-to/configure-private-link) · [Agent Service networking deep dive](https://learn.microsoft.com/en-us/azure/foundry/agents/concepts/agents-networking-deep-dive) · [APIM AI gateway capabilities](https://learn.microsoft.com/en-us/azure/api-management/genai-gateway-capabilities)
- **Community:** [Microsoft Q&A](https://learn.microsoft.com/en-us/answers/) (exam/product questions get MCT answers) and r/AzureCertification (voucher intel, exam experience reports — where the AI-103 beta chatter surfaced first).
- **Udemy:** not needed. Between free official labs, Applied Skills environments, Savill, and the practice assessments, there's nothing a $15 course adds except a second voice — spend the hours labbing instead.

---

## 9. The FDE / AI Engineer career layer

What FDE postings actually ask for (synthesized from [OpenAI's FDE posting](https://openai.com/careers/forward-deployed-engineer-(fde)-nyc-new-york-city/), [Anthropic's FDE posting](https://job-boards.greenhouse.io/anthropic/jobs/5302966008), and [industry coverage](https://www.marktechpost.com/2026/05/20/what-is-a-forward-deployed-engineer-the-ai-role-openai-anthropic-and-google-are-hiring-in-2026/)):

1. **Production LLM systems:** RAG pipelines + vector search, agent development, evaluation frameworks, observability. → Phases 3–4 + capstone.
2. **Real engineering:** production-quality Python, systems design under ambiguity. → Phase 0 ramp + every lab in Python + capstone IaC.
3. **Enterprise integration under real constraints:** identity, networking, security, compliance — deploying AI inside locked-down environments. → **You already have this** (Entra ID, private networking, PKI, zero-trust). The hardening notes and capstone design doc turn it from experience into evidence. Anthropic's posting explicitly delivers "MCP servers, sub-agents, and agent skills" — the MCP Applied Skill and capstone MCP tool speak that language directly.
4. **Consultative delivery:** discovery, scoping, exec communication, embedded customer work. → Practice by presenting: record the capstone demo as if to a customer's IT director — problem, architecture, tradeoffs, cost, security posture — not as a code tour.

**Portfolio checkpoints** (what exists publicly when you finish): AI-901 + AI-103 certifications; six Applied Skills badges; a capstone repo with architecture doc, demo video, and clean IaC; four enterprise-hardening notes (these make strong short blog posts — an FDE-shaped paper trail); a GitHub history showing 16 weeks of consistent commits.

**Beyond (2027):** AI-500 → Multi-Agent AI Solutions Expert as it exits beta; deepen with mslearn-genaiops (evaluation/observability is the current hiring differentiator); consider AZ-104 only if you want the infra credential formalized — your lived experience already covers most of it.

---

## 10. Master schedule

| Wk | Dates (2026) | Phase | Focus | Ship this week |
|---|---|---|---|---|
| 1 | Aug 17–23 | 0 | Curriculum Days 1–7: strings → control flow → lists → functions/dicts → comprehensions → files/errors | Days 1–5 scripts + `log_triage.py`; 10 Exercism drills; toolchain verified |
| 2 | Aug 24–30 | 0 | Curriculum Days 8–14: venv/secrets → httpx → JSON → OpenAI SDK → classes/async → drills | `chat.py` (streaming + history); capstone `log_assistant.py`; gate self-test passed |
| 3 | Aug 31–Sep 6 | 1 | **Azure signup + money rules (§3.1)** · concepts paths · fundamentals repos · Savill AI-901 cram (end of week) | First Foundry project + nano deployment called from local Python; cold practice run |
| 4 | Sep 7–13 | 1 | Foundry-implementation paths · responsible-AI + service-selection drills (§3.5) · practice ≥80%×2 | **AI-901 booked; sit end of wk 4 / start of wk 5 (~Sep 14–18)** · VTD voucher applied if landed |
| 5 | Sep 14–20 | 2 | Language + Speech labs (F0) | Hardening note #1; text-analysis agent working |
| 6 | Sep 21–27 | 2 | Vision labs (incl. Content Understanding) · [OPT] container-to-F0 on homelab (§4.1 step 8 / Appendix A) | Hardening note #2; two Custom Vision projects trained + published |
| 7 | Sep 28–Oct 4 | 2 | Information extraction labs · **Day-30 PAYG upgrade + budget alerts (~Sep 29)** | Hardening note #3 |
| 8 | Oct 5–11 | 2 | AI Search: schema, vectors, hybrid + semantic rerank · chunking experiment · catch-up | Note #4 + architecture diagram · **Applied Skill: Secure AI solutions in the cloud** |
| 9 | Oct 12–18 | 3 | Foundry deep-dive: deployment types, quota/429, content filters, tracing (mslearn-ai-studio) | **Applied Skill: Get started developing agents in Foundry** |
| 10 | Oct 19–25 | 3 | GenAI apps: prompting, your own RAG pipeline, Foundry IQ, evaluation runs | **Applied Skill: Develop a GenAI chat app (Foundry SDK)** |
| 11 | Oct 26–Nov 1 | 3 | Agents: Agent Service object model, tool billing, MAF workflows (mslearn-ai-agents) | **Applied Skill: Develop an agent with integrated tools** |
| 12 | Nov 2–8 | 3 | MCP (build your own server) · multi-agent design · capstone design doc | **Applied Skill: Integrate MCP tools with agents** · `docs/design.md` complete |
| 13 | Nov 9–15 | 3 | Capstone build: agents + RAG + MCP tool | Working end-to-end demo |
| 14 | Nov 16–22 | 3 | Capstone: azd IaC, hardening doc, demo video, teardown | Capstone shipped · **Applied Skill: Enhance agents with autonomous capabilities** · practice ≥70% |
| 15 | Nov 23–29 | 4 | Study-guide self-audit · blind-spot labs · practice ≥85%×2 | Gaps closed · exam booked |
| 16 | Nov 30–Dec 6 | 4 | Light review · fast-doc-lookup drills · **sit AI-103** | **Azure AI Apps and Agents Developer Associate** |

---

## Appendix A — Homelab (Talos K8s) & local container kit

Two ways to run every self-hostable piece of this path: on the Talos cluster or on the Mac. Everything here is $0 — the AI service containers meter against your F0 quotas, and inference runs on your own hardware.

### A.1 What runs where

| Capability | Cluster (Talos K8s) | Mac (local) |
|---|---|---|
| Classic AI services (Language, Speech, Vision Read, Doc Intelligence) | **Best home.** Deployments of Microsoft's containers, metered to F0 — CPU-only, can stay up all phase | Docker Desktop, same images (amd64 — run under emulation on Apple silicon: fine for labs, slow under load) |
| LLM inference (OpenAI-compatible endpoint) | Ollama pod with one RTX 3050 (6 GB VRAM → 3–4B-class models) | Foundry Local (Apple silicon) |
| Azure CLI / azd / VS Code / lab repos | — | Yes — client tooling stays on the Mac |
| Microsoft Foundry, Agent Service, AI Search | Not self-hostable — cloud only (free tiers per §7) | — |

Foundry Local has Linux builds but **no official container image or K8s story** (maintainers have only confirmed internal builds — [GitHub discussion](https://github.com/microsoft/foundry-local/discussions/120)); don't force it onto the cluster — Ollama is the K8s-native equivalent, and your lab code can't tell the difference.

### A.2 One-time cluster setup

```bash
kubectl create namespace ai-lab
# one secret per Azure F0 resource (create each F0 resource in the portal or az CLI first)
kubectl -n ai-lab create secret generic az-lang-f0   --from-literal=apikey='<language-resource-key>'
kubectl -n ai-lab create secret generic az-speech-f0 --from-literal=apikey='<speech-resource-key>'
```

Non-negotiables: pods need **443 egress to `*.cognitiveservices.azure.com`** (the billing heartbeat — containers refuse to run without it), and images pull from `mcr.microsoft.com`. Pin exact tags from the [container docs](https://learn.microsoft.com/en-us/azure/ai-services/cognitive-services-container-support); `:latest` is acceptable for labs.

### A.3 AI service container on the cluster (Language sentiment — the template)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ai-language-sentiment
  namespace: ai-lab
spec:
  replicas: 1
  selector:
    matchLabels: { app: ai-language-sentiment }
  template:
    metadata:
      labels: { app: ai-language-sentiment }
    spec:
      containers:
        - name: sentiment
          image: mcr.microsoft.com/azure-cognitive-services/textanalytics/sentiment:latest
          env:
            - { name: Eula, value: accept }
            - { name: Billing, value: "https://<your-f0-resource>.cognitiveservices.azure.com/" }
            - name: ApiKey
              valueFrom:
                secretKeyRef: { name: az-lang-f0, key: apikey }
          ports:
            - containerPort: 5000
          resources:
            requests: { cpu: "1", memory: 2Gi }
            limits: { cpu: "4", memory: 8Gi }
---
apiVersion: v1
kind: Service
metadata:
  name: ai-language-sentiment
  namespace: ai-lab
spec:
  selector: { app: ai-language-sentiment }
  ports:
    - port: 5000
      targetPort: 5000
```

Adapt the same template for the other images — only the image path, secret, and resources change:

| Image (`mcr.microsoft.com/azure-cognitive-services/…`) | Meters against | Sizing note |
|---|---|---|
| `textanalytics/sentiment` · `textanalytics/keyphrase` · `textanalytics/language` | Language F0 (5k records/mo pooled) | Light — ~1 CPU / 2 Gi each |
| `speechservices/speech-to-text` | Speech F0 (5 audio hrs/mo) | ~2–4 CPU / 2–4 Gi |
| `speechservices/neural-text-to-speech` | Speech F0 (0.5M chars/mo) | Heavy — check doc minimums first |
| `vision/read` | Vision F0 (5k transactions/mo) | OCR/Read — check doc minimums |
| `form-recognizer/layout` | Document Intelligence F0 (500 pages/mo) | Layout analysis |

### A.4 Same containers on the Mac (Docker Desktop)

```bash
docker run --rm -p 5000:5000 --memory 8g --cpus 4 \
  mcr.microsoft.com/azure-cognitive-services/textanalytics/sentiment:latest \
  Eula=accept \
  Billing=https://<your-f0-resource>.cognitiveservices.azure.com/ \
  ApiKey=<key>
```

Same three settings for every image. These are amd64 images — Apple-silicon Docker Desktop runs them under emulation: functional for lab passes, slow for anything sustained. Prefer the cluster when both are available.

### A.5 LLM inference on the cluster — Ollama with one GPU

Prereq: Talos NVIDIA system extensions + the NVIDIA device plugin (already in place if the 3050s serve inference today).

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: ollama-models
  namespace: ai-lab
spec:
  accessModes: [ReadWriteOnce]
  resources:
    requests: { storage: 30Gi }
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ollama
  namespace: ai-lab
spec:
  replicas: 1
  selector:
    matchLabels: { app: ollama }
  template:
    metadata:
      labels: { app: ollama }
    spec:
      runtimeClassName: nvidia        # per the NVIDIA container-toolkit extension setup
      containers:
        - name: ollama
          image: ollama/ollama:latest
          ports:
            - containerPort: 11434
          resources:
            limits: { nvidia.com/gpu: 1 }
          volumeMounts:
            - { name: models, mountPath: /root/.ollama }
      volumes:
        - name: models
          persistentVolumeClaim: { claimName: ollama-models }
---
apiVersion: v1
kind: Service
metadata:
  name: ollama
  namespace: ai-lab
spec:
  selector: { app: ollama }
  ports:
    - port: 11434
      targetPort: 11434
```

```bash
kubectl -n ai-lab exec deploy/ollama -- ollama pull qwen3:4b
# other good fits for 6 GB VRAM: phi4-mini, llama3.2:3b, gemma3:4b
```

One GPU per pod is the clean pattern — up to three model pods, or keep spares for other workloads.

### A.6 LLM inference on the Mac — Foundry Local (current CLI)

The CLI was restructured in June 2026 (CLI 0.10+); Learn docs may still show the older `foundry model run` syntax — the [GitHub releases page](https://github.com/microsoft/Foundry-Local/releases) tracks reality:

```bash
foundry model list              # catalog + aliases
foundry run phi-4-mini          # load/run a model      (was: foundry model run)
foundry chat phi-4-mini         # interactive chat session
foundry model show phi-4-mini   # model details          (was: foundry model info)
foundry server start|stop|restart|logs   #               (was: foundry service …)
foundry status                  # service state + endpoint info for the SDK
```

(Intel-Mac fallback: `brew install ollama` — identical OpenAI-compatible surface.)

### A.7 Wiring the labs to your endpoints

The labs read endpoints/keys from `.env` — point them at your own infrastructure and nothing else changes:

```python
from openai import OpenAI

# cluster inference:
client = OpenAI(base_url="http://ollama.ai-lab.svc.cluster.local:11434/v1", api_key="ollama")
# Mac inference: use the local endpoint shown by `foundry status`

resp = client.chat.completions.create(
    model="qwen3:4b",
    messages=[{"role": "user", "content": "ping"}],
)
print(resp.choices[0].message.content)
```

For classic-service labs, swap the cloud endpoint for `http://<service>.ai-lab.svc.cluster.local:5000` (cluster) or `http://localhost:5000` (Mac) — the containers expose the same REST surface the SDKs expect. Hardening-note fodder: add a NetworkPolicy restricting the `ai-lab` namespace's egress to the billing endpoints only — exactly the egress-control story an enterprise AI deployment needs, running in your own house.

---

## Appendix B — Link registry

**Exams & credentials:** [AI-901 exam](https://learn.microsoft.com/en-us/credentials/certifications/exams/ai-901/) · [AI-901 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-901) · [AI-103 exam](https://learn.microsoft.com/en-us/credentials/certifications/exams/ai-103/) · [AI-103 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-103) · [Azure AI Apps and Agents Developer Associate](https://learn.microsoft.com/en-us/credentials/certifications/azure-ai-apps-and-agents-developer-associate/) · [Multi-Agent AI Solutions Expert (beta)](https://learn.microsoft.com/en-us/credentials/certifications/multi-agent-ai-solutions-expert/) · [Practice assessments hub](https://learn.microsoft.com/en-us/credentials/certifications/practice-assessments-for-microsoft-certifications) · [Renewal policy](https://learn.microsoft.com/en-us/credentials/certifications/renew-your-microsoft-certification) · [Exam retirements](https://learn.microsoft.com/en-us/credentials/support/retired-certification-exams) · [Credential retirements](https://learn.microsoft.com/en-us/credentials/support/credential-retirement) · [AI-103T00 course](https://learn.microsoft.com/en-us/training/courses/ai-103t00) · [New-cert announcement](https://techcommunity.microsoft.com/blog/skills-hub-blog/new-microsoft-certified-azure-ai-apps-and-agents-developer-associate/4494126)

**Lab repos (active):** [mslearn-ai-fundamentals](https://github.com/MicrosoftLearning/mslearn-ai-fundamentals) · [mslearn-ai-concepts](https://github.com/MicrosoftLearning/mslearn-ai-concepts) · [mslearn-ai-language](https://github.com/MicrosoftLearning/mslearn-ai-language) · [mslearn-ai-vision](https://github.com/MicrosoftLearning/mslearn-ai-vision) · [mslearn-ai-information-extraction](https://github.com/MicrosoftLearning/mslearn-ai-information-extraction) · [mslearn-ai-studio](https://github.com/MicrosoftLearning/mslearn-ai-studio) · [mslearn-ai-agents](https://github.com/MicrosoftLearning/mslearn-ai-agents) · [mslearn-genaiops](https://github.com/MicrosoftLearning/mslearn-genaiops)

**Zero-cost infrastructure:** [Azure free account](https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account) · [Free account FAQ](https://azure.microsoft.com/en-us/free/free-account-faq/) · [Always-free services](https://azure.microsoft.com/en-us/pricing/free-services) · [Spending limit](https://learn.microsoft.com/en-us/azure/cost-management-billing/manage/spending-limit) · [Avoid charges](https://learn.microsoft.com/en-us/azure/cost-management-billing/manage/avoid-charges-free-account) · [Budgets](https://learn.microsoft.com/en-us/azure/cost-management-billing/costs/tutorial-acm-create-budgets) · [AI resource purge](https://learn.microsoft.com/en-us/azure/ai-services/manage-resources) · [Foundry Local](https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/what-is-foundry-local) · [AI containers](https://learn.microsoft.com/en-us/azure/ai-services/cognitive-services-container-support) · [Codespaces billing](https://docs.github.com/en/billing/concepts/product-billing/github-codespaces) · [AOAI pricing](https://azure.microsoft.com/en-us/pricing/details/azure-openai/) · [Agent Service pricing](https://azure.microsoft.com/en-us/pricing/details/foundry-agent-service/) · [Foundry cost management](https://learn.microsoft.com/en-us/azure/foundry/concepts/manage-costs) · [Search limits](https://learn.microsoft.com/en-us/azure/search/search-limits-quotas-capacity)

**Savill:** [Channel](https://www.youtube.com/@NTFAQGuy) · [AI-901 cram](https://www.youtube.com/watch?v=a-yuXz_uV30) · [Foundry IQ deep dive](https://www.youtube.com/watch?v=uDVkcZwB0EU) · [Foundry overview](https://www.youtube.com/watch?v=Sq8Cq7RZM2o) · [Managed identity](https://www.youtube.com/watch?v=rC1TV0_sIrM) · [Private Link](https://www.youtube.com/watch?v=57ZwdztCx2w) · [RBAC](https://www.youtube.com/watch?v=qFoHDTxkQII) · [Master Class v3](https://www.youtube.com/playlist?list=PLlVtbbG169nGccbp8VSpAozu3w9xSQJoY) · [Crams playlist](https://www.youtube.com/playlist?list=PLlVtbbG169nH_CJl4wwKBfS1V8nMYr7xL) · [Materials repo](https://github.com/johnthebrit/CertificationMaterials)

**Frameworks & samples:** [agent-framework](https://github.com/microsoft/agent-framework) · [MAF docs](https://learn.microsoft.com/en-us/agent-framework/) · [azure-ai-projects (PyPI)](https://pypi.org/project/azure-ai-projects/) · [Foundry SDK overview](https://learn.microsoft.com/en-us/azure/foundry/how-to/develop/sdk-overview) · [What is Foundry](https://learn.microsoft.com/en-us/azure/ai-foundry/what-is-azure-ai-foundry) · [Foundry Agent Service](https://learn.microsoft.com/en-us/azure/foundry/agents/overview) · [Foundry IQ](https://learn.microsoft.com/en-us/azure/foundry/agents/concepts/what-is-foundry-iq) · [azure-search-openai-demo](https://github.com/Azure-Samples/azure-search-openai-demo) · [foundry-samples](https://github.com/microsoft-foundry/foundry-samples) · [azureai-samples](https://github.com/Azure-Samples/azureai-samples) · [get-started-with-ai-agents](https://github.com/Azure-Samples/get-started-with-ai-agents) · [AI-Gateway labs](https://github.com/Azure-Samples/AI-Gateway) · [ai-hub-gateway accelerator](https://github.com/Azure-Samples/ai-hub-gateway-solution-accelerator)

**Architecture:** [WAF AI workloads](https://learn.microsoft.com/en-us/azure/well-architected/ai/get-started) · [CAF AI scenario](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/scenarios/ai/) · [CAF AI agents](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ai-agents/) · [Baseline Foundry chat architecture](https://learn.microsoft.com/en-us/azure/architecture/ai-ml/architecture/baseline-microsoft-foundry-chat) · [AOAI security baseline](https://learn.microsoft.com/en-us/security/benchmark/azure/baselines/azure-openai-security-baseline) · [Foundry network isolation](https://learn.microsoft.com/en-us/azure/foundry/how-to/configure-private-link) · [Agents networking deep dive](https://learn.microsoft.com/en-us/azure/foundry/agents/concepts/agents-networking-deep-dive) · [APIM AI gateway](https://learn.microsoft.com/en-us/azure/api-management/genai-gateway-capabilities)

**Career:** [OpenAI FDE posting](https://openai.com/careers/forward-deployed-engineer-(fde)-nyc-new-york-city/) · [Anthropic FDE posting](https://job-boards.greenhouse.io/anthropic/jobs/5302966008) · [FDE role overview](https://www.marktechpost.com/2026/05/20/what-is-a-forward-deployed-engineer-the-ai-role-openai-anthropic-and-google-are-hiring-in-2026/) · [Palantir Dev vs Delta](https://blog.palantir.com/dev-versus-delta-demystifying-engineering-roles-at-palantir-ad44c2a6e87)

---

*Generated Aug 15, 2026. Exam details verified against learn.microsoft.com on that date. The Foundry surface moves fast — re-verify study-guide weightings when you enter each phase (they update in place, with "skills measured as of" dates).*
