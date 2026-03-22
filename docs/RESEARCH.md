# MindMate — Deep Research
*Udarbejdet 22. marts 2026 af Claw*

---

## 1. Konkurrentlandskab — hvem laver noget lignende?

### Direkte konkurrenter (AI companion til demente)

| Produkt | Hvem | Hvad | Status | Pris |
|---|---|---|---|---|
| **ElliQ** | Intuition Robotics (Israel/US) | Fysisk robot + skærm. Proaktive samtaler, health tracking, spil. | Live, B2C + B2G. 800 enheder via NY State. | $249 setup + $30-59/md |
| **NewDays "Sunny"** | NewDays (Seattle) | AI companion med fokus på kognitiv terapi. Kombinerer AI-samtaler med telehealth. | Seed-funded ($11.5M). Ex-Amazon/Google founders. | Ikke offentlig |
| **Ella AI** | Ella AI Care | Digital assistent med hukommelse, reminders, nødalarm. | Pre-alpha prototype. Søger investorer. | N/A |
| **LifePod** | LifePod Solutions | Proaktiv voice assistant, medicin-reminders, mood tracking. | Live, B2B (plejecentre). | Enterprise pricing |
| **MyndYou** | MyndYou | AI voice bot der tracker kognitive mønstre via telefonsamtaler. | Live, B2B. | Enterprise |
| **Lenovo "Liv"** | Lenovo + Innovations in Dementia | 3D avatar med fotorealistisk ansigt, bygget på demenspersoners erfaringer. | Pilot | N/A |

### Indirekte konkurrenter (bredere ældrepleje)

| Produkt | Fokus |
|---|---|
| **GrandPad** | Forenklet tablet til ældre (ikke AI-drevet) |
| **Claris Companion** | Tablet med remote management for caregivers |
| **MindMate (app)** | ⚠️ **NAVNEKONFLIKT** — eksisterende app med kognitive øvelser for demens. UK-baseret. |
| **RecallCue** | Hukommelses-reminders og "Memory Lane" feature |
| **SingFit** | Musikterapeutisk app til demente |

### 🚨 Vigtigt: Navnekonflikt

**"MindMate" er allerede taget.** Der eksisterer en britisk app (MindMate) der laver kognitive træningsøvelser for demens. Vi skal finde et andet navn. Forslag:

- **MindVenn** (samtale + forbindelse)
- **Memolink** (hukommelse + link)
- **Samtal** (dansk, simpelt)
- **HuskMig** (dansk, direkte)
- **Rolig** (dansk, beskriver tonen)

---

## 2. Hvad gør vi ANDERLEDES?

De fleste eksisterende løsninger fejler på mindst ét af disse punkter:

| Problem med eksisterende | Vores approach |
|---|---|
| **Kræver hardware** (ElliQ = $250 robot) | Kører på enhver iPad/tablet der allerede er i hjemmet |
| **Engelsk-fokuseret** | Dansk fra dag 1 — sprog og kulturel kontekst |
| **Enterprise pricing** (LifePod, MyndYou) | Gratis/næsten gratis for individuelle brugere |
| **Kognitiv træning** (MindMate app, Lumosity) | Naturlig samtale, ikke "øvelser" |
| **Caregiver-fokuseret** (TapRoot Ella) | Bruger-fokuseret — den demente er primary user |
| **Generisk AI** (ChatGPT, Siri) | Persistert personlig hukommelse + tilpasset persona |
| **Kompleks UI** | Én knap: tryk og snak |

**Vores unfair advantage:** Ingen laver en dansksprog, voice-first, iPad-baseret AI-samtalepartner med personlig hukommelse specifikt til demente. Det er en underserved niche — især i Skandinavien.

---

## 3. Markedet

### Danmark
- **87.000** danskere lever med demens (2024)
- **~300.000** pårørende er direkte berørt
- Dementia care market DK: **$84.4M** projected by 2030 (hurtigst voksende i Europa)
- **21%** af befolkningen er 65+ (stigende til 25% i 2050)
- Stærk digital sundhedsinfrastruktur — DK er Europas mest digitaliserede sundhedsvæsen

### Skandinavien
- Samlet 65+ population: **21%** (2025), stigende til **25%** i 2040
- Sverige: $120.8M dementia market by 2030
- Norge: $74.1M by 2030
- **Samlet nordisk marked: ~$280M by 2030**

### Key insight
Markedet er stort nok til at en niche-løsning kan finde fodfæste, men vores mål er ikke markedsandel — det er validering. 10 brugere der får glæde af det er vores succes.

---

## 4. Regulering og ting I skal vide

### GDPR — den store elefant

Helbredsdata er **"special category data"** under GDPR Art. 9. Det betyder:

| Krav | Hvad det betyder for os |
|---|---|
| **Explicit consent** | Pårørende (eller værge) skal give skriftligt samtykke |
| **Data minimization** | Gem kun hvad der er nødvendigt for samtalen |
| **Right to deletion** | Brugere kan kræve al data slettet |
| **Privacy by design** | Skal bages ind fra starten, ikke boltes på bagefter |
| **Data processing agreement** | Kræves med alle underleverandører (Anthropic, ElevenLabs, Supabase) |

**I prototype-fasen (v1):** Ikke et problem. I tester med 3-5 personer I kender personligt. Men det SKAL løses inden I skalerer.

**Pragmatisk approach:**
1. V1: Informeret samtykke fra pårørende (papirform). Data i EU-hosted Supabase.
2. V2: Proper privacy policy, DPA med leverandører, cookie consent.
3. V3 (hvis skalering): Juridisk review, evt. Data Protection Impact Assessment (DPIA).

### EU AI Act

AI i healthcare = **"high-risk"** klassificering. Krav:
- Transparens (brugeren skal vide det er AI)
- Human oversight
- Datakvalitet og bias-monitorering

**I praksis for v1:** Sørg for at det er tydeligt at det er en AI, ikke et menneske. Det er nok for nu.

### Etiske overvejelser (de vigtige)

1. **Samtykke for demente** — kan en person med demens give informeret samtykke? Juridisk og etisk gråzone. Pårørende/værge skal involveres.
2. **Emotionel afhængighed** — risiko for at brugeren bliver mere knyttet til AI end til mennesker. Skal designes som supplement, ikke erstatning.
3. **Misinformation** — LLM'er kan hallucinate. I en medicinsk kontekst kan det være farligt. Løsning: AI'en giver ALDRIG medicinsk rådgivning.
4. **Data efter dødsfald** — hvad sker der med samtaledata når brugeren dør? Skal defineres.

---

## 5. Tekniske risici og mitigering

| Risiko | Sandsynlighed | Impact | Mitigering |
|---|---|---|---|
| **Whisper forstår ikke ældre danskere** | Høj | Showstopper | Test tidligt med rigtige brugere. Fallback: tekst-input. Overvej Azure Speech (bedre dansk) |
| **LLM hallucinator** | Medium | Høj | System prompt: "Du giver ALDRIG medicinsk rådgivning. Du er en samtalepartner, ikke en læge." |
| **Bruger bliver bange/forvirret** | Medium | Høj | Varm, beroligende persona. Tydelig "dette er en computer". Pårørende kan tilpasse. |
| **Latency (voice pipeline)** | Medium | Medium | STT→LLM→TTS kan tage 3-5 sek. Acceptabelt for målgruppen, men test det. |
| **GDPR-klage** | Lav (i prototype) | Høj (ved skalering) | Løs det i v2, ikke v1. |
| **Navnekonflikt "MindMate"** | 100% | Medium | Skift navn nu, inden det sætter sig. |

### Whisper og ældre dansk tale — det største tekniske spørgsmål

Speech-to-text for ældre danskere med muligvis utydelig tale er den **#1 tekniske risiko**. Anbefalinger:
1. Test med den faktiske målgruppe ASAP (Jens' far)
2. Overvej **Azure Cognitive Services Speech** som alternativ — bedre dansk model end Whisper
3. Byg en fallback: stor "SKRIV" knap på skærmen
4. Mikrofon-kvalitet matters — iPad's built-in mic er OK men ikke fantastisk i støjende miljøer

---

## 6. Hvad bør I tage stilling til inden kickoff

### Beslutninger der skal træffes

1. **Navn** — MindMate er taget. Vælg et nyt.
2. **Persona** — skal AI'en være en "ven", en "hjælper", eller noget neutralt? Skal den have et navn? En alder?
3. **Sprog** — kun dansk? Eller dansk + engelsk fra start?
4. **Hosting region** — EU-hosted Supabase (Frankfurt) for GDPR-compliance
5. **Første testbruger** — er Jens' far realistisk? Har Jacob adgang? Er pårørende med på det?
6. **Open source?** — gør det projektet mere troværdigt (samfundsgavnligt vinkel) men fjerner kommerciel optionalitet

### Min anbefaling

- **Navn:** "HuskMig" eller "Samtal" — dansk, simpelt, beskrivende
- **Persona:** Varm, tålmodig, nysgerrig. Ikke medicinsk. Aldrig nedladende. Har et navn (vælg noget dansk og trygt).
- **Sprog:** Dansk only i v1. Tilføj engelsk i v2 hvis relevant.
- **Open source:** Ja. Det matcher jeres "proces > profit" filosofi og gør historien stærkere.
- **Første test:** Jens' far, men kun hvis Jacob kan facilitere det naturligt og pårørende er komfortable.

---

## 7. Inspirationskilder og videre læsning

- ElliQ: <https://elliq.com>
- NewDays/Sunny: <https://www.newdays.ai>
- Dementia Platform UK (etik + data): <https://portal.dementiasplatform.uk>
- EU AI Act healthcare: <https://health.ec.europa.eu/ehealth-digital-health-and-care/artificial-intelligence-healthcare_en>
- Alzheimer Europe data sharing position: <https://www.alzheimer-europe.org/policy/positions/data-sharing-dementia-research-eu-landscape>

---

*Denne research er et levende dokument. Opdateres løbende som projektet udvikler sig.*
