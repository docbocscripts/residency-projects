# Residency projects

Three browser-based prototypes for residency call trades, learning objectives, and pre-rotation agreements.

## Demo pages

1. **Call trades** — Browse a fictional call roster, select a shift and find compatible one-for-one swaps. The **Email resident** control opens a draft in your email client; because the names are fictional, add the recipient address yourself. No email is sent automatically and no trade is finalized.
2. **Learning objectives** — Browse 14 illustrative psychiatry themes, filter by rotation, rate confidence, flag teaching requests, and export the learning plan or transfer the top priorities to the agreement.
3. **Rotation agreement** — Enter shared expectations, record two self-reported acknowledgments and use **Print / Save as PDF** to print the completed form (select **Save as PDF** in the browser print dialog).

All prototypes use sample data only. A later implementation could connect to the scheduling and data-storage formats used by individual sites.

## Implementation

- `index.html`: page markup and navigation
- `styles.css`: screen and print styles
- `app.js`: demo data and client-side interactions
- `sample_schedule.csv`: fictional roster reference (the website uses the equivalent embedded sample data)

No backend, accounts, email directory, electronic signature verification, or real schedule integration is present. State is kept in the browser tab and resets on refresh. Do not enter patient information or private personnel data.

## Run

Open `index.html` in a browser, or use GitHub Pages with the `main` branch and repository root as its publishing source. No build process or dependencies are required.

## Notes

Call-swap filters are illustrative and do not implement institution-specific policies or formal approval. The 14 learning themes are summaries for demonstration; they are not an authoritative, comprehensive Royal College objective mapping. The PDF action uses the browser print dialog and does not store records remotely.

MIT licensed.