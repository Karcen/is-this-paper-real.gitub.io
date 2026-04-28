# Citation Verifier

> A lightweight, single-file tool for checking whether scholarly references actually exist.

Paste a list of references in any prose-style format — APA, Chicago, Vancouver, MLA — and each entry is checked against the [CrossRef](https://www.crossref.org/) database to detect fabricated, mis-cited, or non-existent works.

Built primarily to catch AI-hallucinated citations in academic manuscripts.

[**→ Live demo**](https://karcen.github.io/citation-verifier/)

![Citation Verifier screenshot](./screenshot.png)

---

## Why

Large language models routinely fabricate plausible-looking but entirely fictional references — wrong DOIs, invented papers, real authors paired with non-existent titles. Manually verifying a 30-item bibliography on Google Scholar takes an hour. This tool does it in under a minute, with no API key and no sign-up.

## Features

- **Zero setup.** A single HTML file. Open it in any modern browser.
- **No API key required.** Uses CrossRef's free public API.
- **Format-agnostic parsing.** Handles `[1]`, `(1)`, `1.`, blank-line, and one-per-line layouts automatically.
- **DOI-first verification.** If a DOI is present it's resolved directly; otherwise the bibliographic text is matched via CrossRef's search API.
- **Three-tier status.** `Verified` / `Possibly Real` / `Not Found`, with title-overlap percentage and year-alignment checks.
- **CSV export.** Download all results, or filter by status — useful for quickly isolating fabricated citations.
- **Light and dark themes.** Automatic detection of system preference, with manual toggle.
- **Privacy.** Queries are sent only to `api.crossref.org`. Nothing is stored.

## How it works

1. **Parse.** The pasted text is split into individual references using one of three strategies (numbered → blank-line → newline).
2. **Extract DOI.** If a DOI matches the regex `10.xxxx/...`, it's looked up directly via `https://api.crossref.org/works/{doi}`.
3. **Bibliographic search.** Otherwise, the reference text is sent to `query.bibliographic` and the top three candidates are scored.
4. **Score.** Title-token overlap (excluding stopwords) is computed against the reference text. A separate year check compares the year extracted from the reference against the matched record.
5. **Classify.**
   - **Verified** — DOI resolves with strong title match, OR title overlap ≥ 70% with year alignment.
   - **Possibly Real** — partial match (25–70% overlap), or strong title match with year mismatch.
   - **Not Found** — no candidate clears the 25% threshold.

## Usage

### Online

Visit the [live demo](https://karcen.github.io/citation-verifier/), paste your references, click **Verify References**.

### Local

```bash
git clone https://github.com/karcen/citation-verifier.git
cd citation-verifier
open index.html       # macOS
xdg-open index.html   # Linux
start index.html      # Windows
```

No build step. No dependencies. No server.

## Example

Input:

```
[1] Dingess, K. A., Gazi, I., van den Toorn, H. W. P., et al. (2021).
    Monitoring human milk β-casein phosphorylation and O-glycosylation
    over lactation. International Journal of Molecular Sciences, 22(15),
    8140. https://doi.org/10.3390/ijms22158140

[2] Smith, J. (2023). The effect of imaginary peptides on fictional
    bioavailability. Journal of Made-Up Research, 99(1), 1–15.
```

Output:

| # | Status | Match |
|---|--------|-------|
| 1 | ✓ Verified | Dingess et al., *Int. J. Mol. Sci.*, 2021 — DOI resolves, 92% title match |
| 2 | ✗ Not Found | No CrossRef record. Likely fabricated or unindexed. |

## Limitations

- **CrossRef coverage.** Approximately 150 million scholarly works. Covers almost all major SCI journals, but **may not cover**: many Chinese-language journals (e.g. 食品科学, 中国乳品工业), some humanities monographs, theses, technical reports, preprints (arXiv, bioRxiv are partially indexed), and predatory journals.
- **Books and chapters** have lower indexing density than journal articles. A `Not Found` result for a book chapter does not necessarily mean it's fabricated.
- **Title heuristic.** The token-overlap score is robust against punctuation and word order but can be fooled by very generic titles. For ambiguous cases, manual verification is recommended.

## CSV output

Click any **Export CSV** button after verification to download a report with the columns:

```
Index, Status, Original Reference, Verification Method,
Title Match Score (%), CrossRef Title, CrossRef Authors,
CrossRef Journal/Publisher, CrossRef Year, CrossRef DOI,
CrossRef URL, Year Match, Note
```

UTF-8 with BOM, so Excel opens Chinese and accented characters correctly.

## Tech stack

- Vanilla HTML / CSS / JavaScript — no framework, no build
- [CrossRef REST API](https://api.crossref.org/) (polite pool)
- Source Serif 4, Inter, JetBrains Mono (via Google Fonts)

## License

MIT — see [LICENSE](./LICENSE).

## Author

Made by **Karcen Zheng** · [Contact](https://karcen.github.io/zhengjiacheng.github.io/)

If this saved you from a fabricated citation, a ⭐ on the repo is appreciated.

---

## Roadmap

Possible additions, in rough order:

- [ ] Bulk paste from `.bib` / `.ris` files
- [ ] PubMed fallback for unindexed biomedical works
- [ ] Semantic Scholar fallback for preprints
- [ ] Inline edit + re-verify
- [ ] Multi-language UI (中文 / EN)
- [ ] Browser extension version

PRs welcome.
