# MindMate — AI-samtalepartner for ældre med demens

*Peter Staunstrup & Jacob Prichander — Marts 2026*

---

## Hvad er det?

En AI-drevet samtalepartner designet til ældre med demens. Kører på en iPad (eller tablet), voice-baseret, og husker brugerens historier, relationer og interesser. Ingen kompleks UI — bare en samtale.

**Formål:** Give demente en stimulerende, tålmodig samtalepartner der aldrig bliver træt af at høre den samme historie igen.

---

## Hvorfor os, og hvorfor nu?

- **AI er modent nok.** LLM'er (Claude, GPT) er ekstremt gode til naturlig samtale og kan instrueres til at være tålmodige, varme og kontekst-bevidste.
- **Det koster næsten ingenting at bygge.** API-omkostninger er minimale. En fungerende prototype kræver ingen investering ud over vores tid.
- **Ingen laver det i DK.** Der findes companion-bots, men ingen der er designet specifikt til dansk ældreplejes kontekst.
- **Vi har domænenærhed.** Jacob kender problemet tæt på (Jens' far). Peter har erfaring med AI-adoption og transformation.

---

## Succeskriterier (bevidst lave)

| Mål | Metric |
|---|---|
| Fungerende prototype | Voice-samtale på iPad der husker kontekst |
| Testet med rigtige brugere | 3-5 ældre har brugt den i mindst en uge |
| Valideret behov | Pårørende/plejepersonale ser værdi |
| Læringsmål nået | Vi har et framework vi kan genbruge til næste idé |

**Vi bygger ikke en virksomhed. Vi bygger et bevis på at vi kan gå fra idé til produkt.**

---

## MVP — Hvad vi bygger (og hvad vi IKKE bygger)

### V1 — "Weekend prototype" (2-3 weekender)

**Inkluderet:**
- Web-app optimeret til iPad (fullscreen, store knapper)
- Voice interface: tryk for at tale → AI lytter → AI svarer med stemme
- Persistent hukommelse per bruger (navne, relationer, historier, interesser)
- Admin-panel for pårørende: "Far hedder Jørgen, han var tømrer, han elsker at snakke om sommerhuset i Gilleleje"
- Dansk sprog (samtale + voice)

**IKKE inkluderet i v1:**
- Login/authentication (vi kender brugerne personligt)
- Betaling
- GDPR-compliance (prototype, ikke produktion)
- App Store (det er en webapp)
- Skalering

### User flow

```
Pårørende: Opretter profil → Indtaster context (navn, familie, historier)
                                        ↓
Ældre bruger: Åbner iPad → Trykker på mikrofon-knap → Snakker
                                        ↓
AI: Lytter → Forstår → Svarer med varm stemme → Husker samtalen
                                        ↓
Pårørende: Kan se samtale-log → Tilføje mere context over tid
```

---

## Tech stack

### Kernekomponenter

| Komponent | Teknologi | Hvorfor |
|---|---|---|
| **Frontend** | Next.js (React) på Vercel | Hurtig at bygge, fungerer som webapp på iPad, gratis hosting |
| **Voice → Tekst** | Whisper API (OpenAI) eller browser Web Speech API | Dansk speech-to-text, høj kvalitet |
| **LLM (hjernen)** | Claude API (Anthropic) | Bedst til nuanceret, empatisk samtale. Stærk på dansk. |
| **Tekst → Voice** | ElevenLabs API | Naturlig dansk stemme, varm og rolig |
| **Database** | Supabase (PostgreSQL) | Gratis tier, nem auth senere, real-time |
| **Hukommelse** | Vector store (Supabase pgvector) | Semantisk søgning i brugerens historier og samtaler |

### Estimeret månedlig omkostning (5 brugere)

| Post | Pris |
|---|---|
| Claude API | ~100-200 kr/md |
| ElevenLabs | ~80 kr/md (starter plan) |
| Whisper API | ~30 kr/md |
| Vercel + Supabase | 0 kr (free tier) |
| **Total** | **~200-300 kr/md** |

---

## Hvordan vi bygger det — værktøjer og workflow

### Agentic coding setup

Vi bruger AI til at bygge AI. Det er hele pointen — vi vil bevise at to ikke-udviklere kan shippe et produkt med moderne AI-værktøjer.

**Claude Code** (primært udviklingsværktøj)
- CLI-baseret coding agent fra Anthropic
- Forstår hele codebases, kan refaktorere, bygge features, skrive tests
- Workflow: vi beskriver hvad vi vil have → Claude Code bygger det → vi reviewer og itererer
- Kører på Claude Max ($100/md) — ingen ekstra API-omkostning under udvikling

**OpenClaw** (operations og automation)
- Peters personlige AI-agent der allerede kører 24/7
- Kan overvåge deploys, køre tests, tjekke at alt virker
- Håndterer reminders, koordinering, og baggrundstjek
- Kan bruges til at prototype prompt-arkitektur inden det flyttes til produkt

**GitHub + Vercel** (deployment pipeline)
- Push til GitHub → auto-deploy til Vercel
- Ingen server-administration, ingen DevOps
- Preview-deploys på hver branch = nem testing

**Cursor / Windsurf** (alternativ IDE)
- AI-assisteret IDE hvis vi foretrækker GUI over CLI
- God til frontend-arbejde og visuel iteration

### Vores roller

| Rolle | Person | Ansvar |
|---|---|---|
| Product & UX | Peter + Jacob | Definere features, teste med brugere, designe flows |
| Prompt engineering | Peter | System prompts, persona, hukommelses-arkitektur |
| Frontend | Claude Code + review | UI, interactions, iPad-optimering |
| Backend | Claude Code + review | API, database, voice pipeline |
| Test & brugerkontakt | Jacob | Koordinere med Jens, finde testbrugere |
| DevOps | OpenClaw + Vercel | CI/CD, monitoring, alerts |

---

## Tidsplan

| Uge | Milestone | Deliverable |
|---|---|---|
| **Uge 1** | Kickoff + arkitektur | Tech stack besluttet, repo oprettet, basic voice loop fungerer |
| **Uge 2** | Core samtale | LLM-integration med persistent hukommelse, dansk voice |
| **Uge 3** | Admin + polish | Pårørende-panel, iPad-optimering, persona-tuning |
| **Uge 4** | Test med rigtige brugere | 2-3 ældre tester det i en uge |
| **Uge 5-6** | Iterér på feedback | Fix hvad der ikke virker, tilføj hvad der mangler |
| **Uge 7-8** | "Demo day" | Fungerende produkt, video-demo, beslutning om næste skridt |

*En "uge" = 4-8 timer i weekenden eller om aftenen. Ikke fuldtid.*

---

## Det store perspektiv

Dette projekt er bevidst småt. Pointen er:

1. **Bevise processen** — vi kan gå fra idé til produkt på 8 uger med AI-værktøjer
2. **Skabe et framework** — tech stack, workflow og roller der kan genbruges til næste idé
3. **Hjælpe mennesker** — hvis bare 5 ældre får en bedre hverdag, er det en succes
4. **Bygge credibility** — "vi byggede en AI-demensassistent på 8 uger" er en stærk historie

Hvad der sker *efter* prototypen er sekundært. Måske sælger vi konceptet. Måske giver vi det væk. Måske pitcher vi det i Løvens Hule. Måske bruger vi frameworket til næste idé allerede ugen efter.

**Det vigtige er at starte.**

---

## Næste skridt

1. **Peter + Jacob:** Book et 2-timers kickoff-møde (fysisk eller online)
2. **Før mødet:** Begge tænker over persona — hvordan skal AI'en "være"? Varm? Humoristisk? Formel?
3. **På mødet:** Opret GitHub repo, sæt tech stack op, byg den første voice-loop
4. **Inden uge 1 er slut:** En iPad der kan lytte til dig og svare på dansk

---

*Dokument udarbejdet af Claw (Peters AI-assistent) baseret på samtale 22. marts 2026.*
*Spørgsmål? Smid en mail eller ring til Peter.*
