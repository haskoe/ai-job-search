# Search Queries for Job Scraper

<!-- Populated by /setup on 2026-09-08. Re-run `/setup --section search` to update. -->

Profile: Julian Askøe Bluming — autoriseret klinisk diætist, kandidat i Human Ernæring. Based in Solrød Strand; search scope is **all of Sjælland**.

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. Currently **enabled**:

| Skill | Why it's on |
|---|---|
| `jobnet-search` | Jobnet — the single most important board for this profile. Regioner and kommuner post virtually every clinical dietitian and health-consultant vacancy here. |
| `jobindex-search` | Jobindex — largest general Danish board; broad coverage of private clinics, industry and hospitals. |
| `jobbank-search` | Akademikernes Jobbank — best source for PhD-stipendiat, forskningsassistent and other academic posts. |
| `jobdanmark-search` | Jobdanmark — additional Danish coverage, useful for kommunale and healthcare categories. |
| `linkedin-search` | LinkedIn — industry roles (Nutricia, Nestlé Health Science, Fresenius Kabi, Novo Nordisk) are often posted here first. |

**Disabled:** `freehire-search` — tech-first aggregator (software/data/DevOps), no coverage of clinical nutrition. Flip `enabled: true` in its `SKILL.md` only if the search ever widens toward tech.

The `site:` query templates below are the **WebSearch fallback** — for portals without a CLI, hospital and university career pages, and when a CLI fails.

**Language scope:** write every category in **Danish first** — the overwhelming majority of relevant postings are Danish-language. Add **English** variants for PhD calls (Danish universities advertise these in English), international research groups and industry roles. Danish and English are the only declared languages; a posting requiring any third language as a job condition is excluded before scoring, and one requiring a *higher* spoken-English bar than B2 is flagged for Julian's own judgment rather than dropped — see `04-job-evaluation.md`'s Language Gate, the single source of truth for this rule.

## Search Sites

Primary Danish boards:
- **jobnet.dk** — public sector: regioner, kommuner, hospitaler (also covered by `jobnet-search` CLI)
- **jobindex.dk** — largest general board (also covered by `jobindex-search` CLI)
- **jobbank.dk** — Akademikernes Jobbank; academic, PhD, forskningsstillinger (also covered by `jobbank-search` CLI)
- **jobdanmark.dk** — general Danish board (also covered by `jobdanmark-search` CLI)
- **linkedin.com/jobs** — filter: Denmark / Region Hovedstaden / Region Sjælland (also covered by `linkedin-search` CLI)

Sector-specific career pages worth checking directly:
- `regionh.dk` / `regionsjaelland.dk` — regional hospital vacancies
- `jobportal.ku.dk`, `dtu.dk/om-dtu/job` — university and PhD posts
- `foa.dk`, `kost.dk` (Kost & Ernæringsforbundet) — professional-association listings
- Kommune career pages: Solrød, Køge, Greve, Roskilde, København

## Query Categories

Queries are grouped by priority and organised **by function, not by job title** — the same work is posted as "klinisk diætist", "diætist", "ernæringsfaglig medarbejder" or "ernæringsterapeut" depending on the employer. Combine with location terms where the site supports it.

### Priority 1: Klinisk diætist (hospital, region, kommune, privat klinik)

The core direction. 20 weeks of placements across nephrology, cardiology, neurology and endocrinology map directly.

```
site:jobnet.dk "klinisk diætist" Sjælland
site:jobnet.dk diætist region hovedstaden
site:jobnet.dk diætist region sjælland
site:jobindex.dk "klinisk diætist" København
site:jobindex.dk diætist Køge OR Roskilde OR Næstved OR Holbæk OR Slagelse
site:jobdanmark.dk diætist Sjælland
site:linkedin.com/jobs "klinisk diætist" Denmark
site:regionh.dk diætist
site:regionsjaelland.dk diætist
"ernæringsterapeut" OR "ernæringsfaglig medarbejder" hospital Sjælland
"diætist" nyuddannet Sjælland
```

Nephrology and cardiology are the strongest sub-specialities — worth searching directly:

```
site:jobnet.dk diætist nefrologi OR dialyse
site:jobnet.dk diætist hjerte OR kardiologi
site:jobindex.dk diætist diabetes OR endokrinologi København
```

### Priority 2: Forskningsdiætist, studiekoordinator, forskningsassistent

The genuine differentiator: protocol authorship, VEK approval, ClinicalTrials.gov registration, REDCap data management and analysis — unusually concrete for a new graduate.

```
site:jobbank.dk forskningsassistent ernæring
site:jobbank.dk studiekoordinator klinisk studie
site:jobnet.dk "forskningsdiætist"
site:jobnet.dk projektkoordinator klinisk forskning Sjælland
site:jobindex.dk "klinisk studie" koordinator København
site:jobbank.dk REDCap OR "clinical trial" coordinator Denmark
site:linkedin.com/jobs "clinical research coordinator" nutrition Denmark
site:jobbank.dk datamanager klinisk forskning
"forskningsassistent" ernæring OR kost Københavns Universitet
"research assistant" nutrition Copenhagen
```

### Priority 3: PhD-stipendiat (human / klinisk ernæring)

Search in **English** — Danish universities advertise PhD calls in English. A first-author manuscript in preparation is a real differentiator here.

```
site:jobbank.dk PhD nutrition Denmark
site:jobportal.ku.dk PhD human nutrition
site:jobportal.ku.dk PhD clinical nutrition
site:dtu.dk PhD nutrition OR "food institute"
"PhD stipendiat" ernæring
"PhD fellowship" nutrition Copenhagen
site:linkedin.com/jobs PhD nutrition Denmark
site:jobbank.dk ph.d. ernæring OR kostforskning
```

### Priority 4: Industri — medical / scientific advisor, produktspecialist

Clinical nutrition applied commercially. Named targets: Nutricia, Nestlé Health Science, Fresenius Kabi, Arla Foods Ingredients, Novo Nordisk.

```
site:linkedin.com/jobs "medical advisor" nutrition Denmark
site:linkedin.com/jobs "scientific advisor" nutrition Denmark
site:jobindex.dk produktspecialist klinisk ernæring
site:jobindex.dk "medical science liaison" ernæring OR nutrition
site:linkedin.com/jobs Nutricia OR "Nestlé Health Science" OR "Fresenius Kabi" Denmark
site:jobindex.dk ernæringsfaglig konsulent
"clinical nutrition" specialist Denmark
```

### Priority 5: Kommunal forebyggelse og sundhedsfremme (wider net)

Adjacent, lower priority — apply where the posting welcomes nyuddannede and the work is genuinely nutrition-led.

```
site:jobnet.dk sundhedskonsulent ernæring kommune
site:jobnet.dk "ernæring og sundhed" kommune Sjælland
site:jobnet.dk forebyggelse kost kommune Køge OR Solrød OR Greve OR Roskilde
site:jobindex.dk sundhedsfaglig konsulent ernæring
```

## Location Filter

Home base: **Solrød Strand (2680)**. Scope is all of Sjælland, both regions.

- **Ideal** (short transit commute): Solrød, Køge, Greve, Roskilde, Taastrup, Hvidovre, København S/SV
- **Acceptable** (standard Storkøbenhavn commute): København (inkl. Rigshospitalet, Bispebjerg), Frederiksberg, Glostrup, Herlev, Gentofte, Hillerød, Amager
- **Borderline** (long but workable — flag the commute time): Næstved, Slagelse, Holbæk, Ringsted, Helsingør, Nykøbing Falster
- **Too far** (FAIL): anywhere off Sjælland — Fyn, Jylland, Bornholm, abroad

**Driving licence:** expected approx. **Nov 2026**. Postings requiring own car or a licence are **flagged, not excluded** — many will accept a start date after it. Surface the date rather than dropping the role.

**Shift work:** night, evening and rotating shift roles are a **deal-breaker** — exclude.

## Language Filter

Danish (native) and English (B2, good working level) are the declared languages. Apply `04-job-evaluation.md`'s Language Gate:
- A posting requiring any third language as a job condition → **excluded**
- "Flydende engelsk i tale" / English as working language → **flagged**, not excluded (B2 spoken)
- "Gode engelskkundskaber" or English named without a level → **passes**
- An English-language ad for a Danish hospital or university post → judge the role's working language, not the ad's

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. Danish public-sector postings almost always carry an explicit `ansøgningsfrist` — use it in preference to the posting date. If neither can be determined, include but flag as "date unknown".

## Deal-breaker Filter (exclude before ranking)

- Rene salgs- og provisionsstillinger
- Solostillinger uden diætistkolleger eller fagligt fællesskab — verify before excluding, since some kommune posts have an external professional network
- Nat-, aften- og skifteholdsarbejde
- Kommercielle vægttabskoncepter, slankeklinikker og kosttilskudssalg uden evidensgrundlag

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and generate 2-3 custom queries for that focus. For example:
- `/scrape forskning` -> Priority 2 + 3 queries plus custom research-specific terms
- `/scrape nyre` -> Priority 1 nephrology queries plus dialysis-centre and nephrology-department searches
- `/scrape industri` -> Priority 4 queries plus named-company career-page searches
