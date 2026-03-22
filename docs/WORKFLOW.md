# MindMate — Workflow & Tooling Guide
*Hvordan vi faktisk arbejder sammen*

---

## Overblik

```
Peter / Jacob
    ↓ (beskriver feature/opgave)
Claude Code
    ↓ (skriver kode, tests, commits)
GitHub repo (mindmate)
    ↓ (auto-deploy)
Vercel (live preview)
    ↓
Claw (overvåger, hjælper, koordinerer)
```

---

## 1. Værktøjer — hvem bruger hvad

### Begge skal have

| Værktøj | Hvad | Setup |
|---|---|---|
| **Claude Max** | $100/md subscription — ubegrænset Claude Code | [claude.ai](https://claude.ai) → Max plan |
| **Claude Code** | CLI coding agent | `npm install -g @anthropic-ai/claude-code` |
| **Git + GitHub** | Versionsstyring | [github.com/signup](https://github.com/signup) + `brew install git` |
| **Node.js** | Runtime (til Next.js + Claude Code) | [nodejs.org](https://nodejs.org) (v22 LTS) |
| **VS Code** (valgfrit) | Editor til at kigge kode igennem | [code.visualstudio.com](https://code.visualstudio.com) |

### Nice-to-have

| Værktøj | Hvad | Hvornår |
|---|---|---|
| **Cursor** | AI-assisteret IDE (GUI alternativ til Claude Code) | Hvis I foretrækker GUI over terminal |
| **OpenClaw** | AI-agent (Peters kører allerede) | Jacob kan sætte sin egen op senere |
| **Vercel CLI** | Deploy fra terminal | `npm i -g vercel` — men auto-deploy via GitHub er nok |

### Claw's rolle (Peters OpenClaw)

Claw kan:
- ✅ Overvåge repo (nye commits, PRs, issues)
- ✅ Køre baggrundstjek (er deploy ok? fejler tests?)
- ✅ Holde projektdokumentation opdateret
- ✅ Researche når I har spørgsmål
- ✅ Sende koordinerings-mails mellem Peter og Jacob

Claw kan IKKE:
- ❌ Pushe kode direkte (det gør Claude Code via jeres lokale machines)
- ❌ Snakke med Jacob direkte (Claw er Peters personlige agent)

**Anbefaling:** Jacob sætter IKKE sin egen OpenClaw op endnu. Det er en distraction. Start med Claude Code + GitHub. OpenClaw kan tilføjes senere hvis der er behov.

---

## 2. GitHub repo-struktur

```
mindmate/
├── CLAUDE.md              ← Instruktioner til Claude Code (VIGTIG)
├── README.md              ← Projekt-overblik
├── docs/
│   ├── PLAN.md            ← Projektplan
│   ├── BRAINSTORM.md      ← Idéer og noter
│   ├── DECISIONS.md       ← Beslutningslog
│   ├── RESEARCH.md        ← Konkurrenter, marked, regulering
│   └── WORKFLOW.md        ← Denne fil
├── src/
│   ├── app/               ← Next.js app router
│   ├── components/        ← React components
│   ├── lib/               ← Utilities, API clients, prompts
│   └── types/             ← TypeScript types
├── public/                ← Static assets
├── supabase/              ← Database migrations og schema
├── tests/                 ← Tests
├── .env.example           ← Environment variables template
├── .github/
│   └── workflows/
│       └── claude.yml     ← Claude GitHub Actions (optional)
├── next.config.js
├── package.json
└── tsconfig.json
```

---

## 3. CLAUDE.md — det vigtigste fil i repoet

Claude Code læser denne fil automatisk ved start af hver session. Den fortæller Claude hvad projektet er, hvordan koden er struktureret, og hvad den skal/ikke skal gøre.

**Anbefalet indhold for vores CLAUDE.md:**

```markdown
# MindMate

AI-samtalepartner for ældre med demens. Voice-first iPad webapp.

## Tech Stack
- Next.js 15 (App Router, TypeScript)
- Anthropic Claude API (samtale-motor)
- ElevenLabs API (text-to-speech, dansk)
- Whisper API eller Web Speech API (speech-to-text)
- Supabase (PostgreSQL + pgvector for hukommelse)
- Vercel (hosting)

## Arkitektur
- /src/app — Next.js pages og API routes
- /src/components — React components (functional, ingen class components)
- /src/lib — API clients, prompts, utilities
- /supabase — Database schema og migrations

## Regler
- Alt kode i TypeScript (strict mode)
- Functional components med hooks
- Server components som default, "use client" kun når nødvendigt
- Tailwind CSS til styling
- Ingen inline styles
- Alle API keys i environment variables, ALDRIG hardcoded
- Commit messages på engelsk, korte og beskrivende
- AI'en giver ALDRIG medicinsk rådgivning — dette er hardcoded i system prompts

## Test
- Kør: npm run test
- Kør lint: npm run lint
- Kør typecheck: npx tsc --noEmit

## Vigtige filer
- /src/lib/prompts.ts — System prompts til Claude API (samtalepartner-persona)
- /src/lib/memory.ts — Hukommelses-system (vector search)
- /supabase/schema.sql — Database schema
```

---

## 4. Daglig workflow

### Når Peter eller Jacob vil bygge en feature

```
1. Åbn terminal i repo-mappen
2. git pull (hent seneste ændringer)
3. Kør: claude
4. Beskriv opgaven: "Byg voice input component der bruger Web Speech API
   til at optage dansk tale og vise transkription"
5. Claude Code bygger det, kører tests, committer
6. Review output → godkend eller bed om ændringer
7. git push → auto-deploy til Vercel
```

### Når begge arbejder samtidig

Brug **branches** for at undgå konflikter:

```
Peter: git checkout -b feature/voice-input
Jacob: git checkout -b feature/admin-panel

→ Arbejd uafhængigt
→ Lav Pull Request til main
→ Den anden reviewer (eller Claw hjælper)
→ Merge til main
```

### Kommunikation

| Kanal | Brug til |
|---|---|
| **Telegram** (Peter ↔ Claw) | Peter giver Claw opgaver, får status |
| **GitHub Issues** | Feature requests, bugs, opgaver |
| **GitHub PRs** | Code review, diskussion om implementation |
| **Mail / telefon** | Peter ↔ Jacob koordinering |

---

## 5. Opsætning step-by-step (for Jacob)

### Dag 1: Grundlæggende setup

```bash
# 1. Installér Node.js (hvis ikke allerede)
# Download fra https://nodejs.org (v22 LTS)

# 2. Installér Claude Code
npm install -g @anthropic-ai/claude-code

# 3. Log ind på Claude
claude login
# (åbner browser → log ind med din Claude Max konto)

# 4. Klon repo
git clone https://github.com/musagent-create/mindmate.git
cd mindmate

# 5. Start Claude Code
claude

# 6. Prøv det: skriv en opgave
# > "Opret Next.js projekt med TypeScript og Tailwind CSS i src/"
```

### Dag 1: Vercel deploy

```bash
# 1. Opret konto på vercel.com (gratis)
# 2. Forbind GitHub repo
# 3. Auto-deploy er nu aktiv — hver push til main deployer automatisk
```

---

## 6. Best practices

### For Claude Code sessioner

1. **Start med at læse** — bed Claude om at forstå codebasen før den ændrer noget
2. **Én feature ad gangen** — ikke "byg hele appen", men "byg voice input component"
3. **Verificér altid** — bed Claude om at skrive tests og køre dem
4. **Commit ofte** — små, hyppige commits > store, sjældne
5. **Ny session per feature** — start fresh Claude Code session for hver større opgave (undgå context pollution)

### For samarbejdet

1. **GitHub Issues er jeres backlog** — skriv en issue for hver feature/opgave
2. **Branches per feature** — aldrig commit direkte til main
3. **PR reviews** — selv om Claude skrev koden, skal et menneske godkende
4. **CLAUDE.md er levende** — opdatér den når I lærer noget nyt om hvad Claude gør godt/dårligt

---

## 7. Hvad Claw gør i baggrunden

Peters OpenClaw (Claw) kan sættes op til automatisk at:

1. **Tjekke repo-aktivitet** — nye commits, åbne PRs, failed deploys
2. **Sende daglig status** — "MindMate: 3 nye commits i går, deploy OK, 2 åbne issues"
3. **Holde docs opdateret** — DECISIONS.md, RESEARCH.md etc.
4. **Svare på spørgsmål** — Peter kan spørge Claw om projektet via Telegram

Dette sættes op som et cron job når I er i gang med at kode.

---

## TL;DR — Minimum Viable Setup

| Hvem | Skal have | Dag 1 |
|---|---|---|
| **Peter** | Claude Max ✅, Claude Code ✅, GitHub ✅, Git ✅ | Klar |
| **Jacob** | Claude Max, Claude Code, GitHub-konto, Git | Installér + klon repo |
| **Repo** | CLAUDE.md, branch protection, Vercel deploy | Peter/Claw sætter op |
| **Claw** | Monitoring cron job | Sættes op når kodning starter |

**Alt andet er nice-to-have. Start med dette.**
