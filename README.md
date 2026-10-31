> **Design update (October 2026):** The public prototype has been restyled with an original, editorial, Artsy-inspired visual language (monochrome palette, serif headlines, whitespace, fine rules). The deployable `index.html` is standalone, so GitHub Pages can serve it without a build process. No Artsy branding or proprietary assets are used.

# ResidentFlow — Chief Resident Innovation Studio

A clean, interactive, static site presenting **three practical psychiatry-residency pilot concepts** for a chief resident application.

> **Prototype only.** The app is not approved for clinical, educational assessment, or administrative production use. Do not upload patient information or rely on demo trade suggestions for approved coverage.

## Explore the three working demos

| Concept | What you can do | What is deliberately not implemented |
| --- | --- | --- |
| **Call Exchange** | Import `.csv` (including Airtable CSV exports) or `.xlsx`, select a resident and offered call, filter and rank one-to-one swaps that match level and call type and avoid conflicts in the imported schedule; flag a candidate for human review | Automatic access to Airtable accounts; synchronization; official approvals; vacation data or other scheduling policies; notifications |
| **Learning Map** | View 14 illustrative, psychiatry-relevant learning themes; filter by rotation and learner stage; self-rate confidence (1–5); request teaching; export a CSV plan; insert goals into rotation agreement | Full Royal College objective catalogue; official numbered EPA / textbook chapter crosswalk; longitudinal multiuser tracking |
| **Rotation Agreement** | Record learner and staff details, shared learning goals, feedback and supervision expectations; record two **self-reported** acknowledgments; print to PDF; export JSON; automatically clear acknowledgments if contents change | Authentication, legally binding e-signatures, secure server recordkeeping, faculty invitations |

All workflows run in the browser. The app makes **no API requests** and does not save your roster, ratings, or agreement to a server or browser storage. Information entered in the tab is lost on refresh unless exported. External reference links are only opened by the user. The site itself can be hosted on GitHub Pages without any build tools or dependencies.

## Run locally

Open `index.html` directly, or in this directory run:

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000`.

## Publish for free with GitHub Pages

1. On GitHub, [create a new repository](https://github.com/new), e.g. `residentflow-chief-resident-prototypes`. Make it **Public**. You can initialize with a README or create it empty.
2. Upload the **contents** of this project folder to the repository root. Ensure `index.html`, `styles.css`, and `app.js` are at the **root**, not nested inside a subfolder. In GitHub's interface use **Add file → Upload files** and commit; or push from Git on your computer.
3. Open repository **Settings → Pages**. Under **Build and deployment**, choose **Deploy from a branch**, then select **main** and **/(root)**, and save.
4. GitHub Pages will publish the site at `https://YOUR-USERNAME.github.io/residentflow-chief-resident-prototypes/`. Use the URL GitHub actually shows under Pages to verify publication.

GitHub's official instructions: [Creating a GitHub Pages site](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site), [Configuring a publishing source](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

## Call schedule: data contract and matching assumptions

Import an Excel workbook `.xlsx` (the first sheet with recognizable headers) or a comma-delimited UTF-8 CSV. **Airtable** users can export a view as CSV and then import that file; direct API integration is a future option. The expected columns are:

```csv
date,resident,level,type,site
2026-11-05,Dr. Maya Chen,PGY3,Overnight,General Hospital
2026-11-12,Dr. Daniel Lee,PGY3,Overnight,General Hospital
```

Supported header alternatives include `Call Date`, `Resident Name`, `PGY`, `Call Type`, and `Hospital`. Date values may be ISO `YYYY-MM-DD`, US-style `MM/DD/YYYY`, or typical Excel date serials. A sample roster is available as `sample_schedule.csv` or using **Download sample CSV** inside the website.

A candidate swap requires:

- Different residents, different dates, identical trainee **level** and **call type**.
- Same site **if** the same-site toggle is enabled.
- No overlapping shift date in the imported schedule for either person after the hypothetical trade.
- No adjacent-day call in the imported roster if the rest-gap toggle is enabled.
- An optional preferred date window.

The percentage shown in matching results is an **illustrative ranking heuristic based on date distance**, not a calibrated probability, a claim of fairness, or a certification of safe coverage. The schedule parser does not interpret availability, sick leave, leave requests, statutory hour limits, post-call days, continuity-of-care, protected teaching, approval hierarchies, or other program rules. An approved workflow would need these policies and a designated final approver.

### Import / security detail

The XLSX import is powered by a small, local ZIP/XML reader using the browser's `DecompressionStream` API, without a third-party script or server. If your browser lacks this API, or an XLSX variant is unsupported, export to CSV first. The importer is designed for modest, conventional worksheets rather than large or complex workbooks; maximum 8 MB.

## Learning content and reference integrity

The 14 learning themes are **editorial summaries** of relevant clinical learning areas, informed by broad Royal College competencies and rotation needs. They are **not** the exact Royal College objectives, EPA texts, an official Royal College mapping, a complete curriculum, or a validated assessment instrument. They may not reflect every applicable competency for a specific cohort, institution or learner stage. The Royal College released updated Psychiatry EPA documentation for **2026 version 2.0**; verify your own training cohort's requirements.

Textbook pointers intentionally map to **chapter topics**, not chapter numbers: the chapter numbers and divisions change with the edition of *Kaplan & Sadock's Synopsis of Psychiatry* and *Stahl's Essential Psychopharmacology*. Editors should check an institution's licensed edition before adding precise chapter numbers.

External authoritative learning links used:

- [Royal College — Psychiatry discipline standards](https://www.royalcollege.ca/en/standards-and-accreditation/information-by-discipline?specialty=royal-college%3Aibd%2Fspecialty%2Fpsychiatry)
- [Royal College — Psychiatry EPAs (2026, version 2.0)](https://www.royalcollege.ca/content/dam/documents/ibd/psychiatry/epa-guide-psychiatry-v2-e.pdf)
- [CANMAT MDD 2023 update (published 2024)](https://pubmed.ncbi.nlm.nih.gov/38711351/)
- [CANMAT / ISBD bipolar disorder 2023 evidence update](https://pubmed.ncbi.nlm.nih.gov/38695002/)
- [Canadian anxiety, PTSD and OCD guideline (2014)](https://pmc.ncbi.nlm.nih.gov/articles/PMC4120194/) — older reference; check for newer sources when adapting locally
- [Canadian Coalition for Seniors' Mental Health — BPSD guideline resources](https://ccsmh.ca/areas-of-focus/dementia/clinical-guidelines/)

Links are for clinician education and are not a substitute for up-to-date local protocols or individualized clinical care. Full textbook or Royal College text is not reproduced.

## Security and responsible pilot development

**Do not place real trainee rosters, personal evaluations, staff signatures or patient information in this publicly hosted demo until your institution has approved the security and privacy architecture.** GitHub Pages is public hosting, not a compliant clinical or confidential workforce application. Even though this app currently works within a browser tab, it lacks formal auditability, authentication and durable secure storage. The acknowledgment feature is a conversation aid, **not a legally binding digital signature**.

For an institutional pilot, next steps would include SSO (institutional login), server-side authorization and encryption, scheduler-owned data ingestion, version history, audit logs, true notifications/approvals, privacy impact assessment, policy validation, and alignment with applicable Canadian and provincial privacy obligations.

## Candidate pilot measures (aspirational, not measured results)

- Median time spent finding an **eligible** call exchange, and percent of proposals approved.
- Percent of residents reporting rotation learning goals were discussed within the first week.
- Number of teaching requests addressed by the rotation midpoint.
- Percent of rotation agreements discussed and acknowledged by both participants.
- Resident and staff satisfaction, administrative burden, and any unexpected equity or safety issues.

## Files

- `index.html` — responsive app pages and semantic content
- `styles.css` — responsive styling and print stylesheet
- `app.js` — data import, matching, ratings, export, acknowledgment logic
- `sample_schedule.csv` — fictional roster to test import
- `PROJECT_PITCH.md` — chief resident application pitch / pilot outline
- `.nojekyll` — prevents Jekyll processing on branch-based GitHub Pages

**License:** MIT. You may adapt, review and propose improvements, but source links and safety notes should be preserved where relevant.