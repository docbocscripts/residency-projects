# Residency projects

Three independent browser demos exploring residency scheduling and rotation setup workflows. This is a front-end prototype repository; it does not provide a shared database, login system, or production integrations.

**Demo:** `https://deskpig.github.io/residency-projects/` (available once GitHub Pages is enabled)

## Run

```sh
python3 -m http.server 8000
# open http://localhost:8000
```

No package installation or build step. The published `index.html` includes the CSS and JavaScript inline so the demo can be run or shared as a single file.

## Demos

### 1. Call trades

- Starts with a fictional 22-shift schedule.
- Reads local `.csv` files, including CSV exports from Airtable, and conventional `.xlsx` workbooks. The browser's native `DecompressionStream` API is used for XLSX; unsupported files can be exported to CSV.
- Select a resident and offered call, optionally limit dates or require the same site, and view candidate one-for-one swaps.
- Optional rest-gap filter rejects trades with adjacent-day calls found in the imported schedule.
- A **Flag for review** action only changes the interface; it does not submit a request, send a message or change the roster.

Expected columns:

```csv
date,resident,level,type,site
2026-11-05,Dr. Maya Chen,PGY3,Overnight,General Hospital
2026-11-12,Dr. Daniel Lee,PGY3,Overnight,General Hospital
```

Alternative headers such as `Call Date`, `Resident Name`, `PGY`, `Call Type` and `Hospital` are recognized. Dates can be ISO, `MM/DD/YYYY`, or typical Excel serial dates. See `sample_schedule.csv` for a test file.

**Matching assumptions:** equal PGY level and call type, different resident and date, no duplicate-date conflicts, optional same site, optional no-adjacent-calls rule, optional replacement date range. The displayed percentages are *sorting heuristics*, not probabilities of approval. The demo does not consider leave, non-call clinical assignments, coverage rules, duty hour rules, post-call requirements, or approvals. Human review remains necessary.

### 2. Learning objectives

- Shows 14 **illustrative** psychiatry learning themes, filterable by rotation, learner stage and search.
- Lets the learner assign confidence ratings (1–5), flag teaching requests and export a teaching plan.
- Can copy selected priorities into the rotation agreement.
- Provides links to primary curriculum materials and external reading suggestions.

These themes are **not official verbatim Royal College Psychiatry objectives**, a complete list, an approved assessment, or an exact mapping to EPAs. The learner-stage selector provides context for discussion but does not load a stage-specific official objective set. Textbook suggestions reference topics rather than chapter numbers because editions of *Kaplan & Sadock* and *Stahl* differ.

Reference starting points:

- [Royal College Psychiatry discipline standards](https://www.royalcollege.ca/en/standards-and-accreditation/information-by-discipline?specialty=royal-college%3Aibd%2Fspecialty%2Fpsychiatry)
- [Royal College Psychiatry EPA guide (2026, version 2.0)](https://www.royalcollege.ca/content/dam/documents/ibd/psychiatry/epa-guide-psychiatry-v2-e.pdf)
- [CANMAT MDD 2023 update (published 2024)](https://pubmed.ncbi.nlm.nih.gov/38711351/)
- [CANMAT / ISBD bipolar disorder 2023 evidence update](https://pubmed.ncbi.nlm.nih.gov/38695002/)
- [Canadian anxiety, PTSD and OCD guideline (2014)](https://pmc.ncbi.nlm.nih.gov/articles/PMC4120194/)
- [CCSMH dementia/BPSD guidelines](https://ccsmh.ca/areas-of-focus/dementia/clinical-guidelines/)

These links are suggestions to check against current training standards and local licensed educational resources before making a real curriculum crosswalk.

### 3. Rotation agreement

- Edit names, rotation dates, learning goals, clinical exposure, supervision, feedback and responsibilities.
- Resident and supervisor can independently **acknowledge** the current draft.
- Any edit clears both acknowledgments to require another review.
- Print/save as PDF or export a JSON snapshot.

**No identity verification:** The acknowledgments are self-reported UI markers, not signed legal documents. There is no shared state, staff invitation, permissions or server-backed audit history.

## Code layout

| File | Purpose |
| --- | --- |
| `index.html` | All three demos, their browser logic, and styling in one standalone file |
| `sample_schedule.csv` | Fictional schedule for testing import |
| `.nojekyll` | Use branch-based GitHub Pages without Jekyll processing |
| `LICENSE` | MIT license |

## Implementation limits

- **Client-side only.** The demos make no application API requests; form state lives in memory within the current browser tab and resets on refresh. Exports are local downloads. Following external resource links navigates to third-party sites.
- **No sensitive data.** Use fictional names and schedules. Do not enter personal resident evaluations, identifiable staff schedules, or patient information into a public demonstration.
- **Not scheduling software.** The matching algorithm is a candidate generator, not an eligibility engine, approval system, or institutional roster source of truth.
- **Not a credentialed assessment.** Confidence ratings are learner-entered examples; they are not official competency scores.
- **Not an e-signature tool.** Agreement acknowledgments are only markers within the page.

If developed for actual departmental use, this would need institutional review and an approved security design: authentication/SSO, role-based access, encrypted durable storage, audit records, privacy impact assessment, integration with the authoritative roster, policy rules, and appropriate consent or record-retention procedures.

## GitHub Pages

For this public repository, open [Settings → Pages](https://github.com/deskpig/residency-projects/settings/pages). Set **Source: Deploy from a branch**, **Branch: main**, **Folder: /(root)**, then save. GitHub should then serve the root `index.html` at `https://deskpig.github.io/residency-projects/`. Publishing requires repository administration; committing code does not itself enable Pages.

## Testing

Browser-level smoke checks were performed with Playwright/Chromium for navigation, call-match flags, learning objective search, transferring goals into the agreement, and desktop/mobile layouts. Re-run using a local Chromium/Playwright environment.

This repository is licensed under MIT. Contributions and issue reports are welcome.