# 📚 Citation Verifier

A lightweight, browser-based tool for checking whether scholarly references actually exist.

Paste references in any common format (APA, Chicago, Vancouver, MLA), and the tool verifies them against the CrossRef database, returning clean, standardized, and copy-ready results.

---

## ✨ Features

* 🔍 **Reference Verification**

  * Automatically checks if a citation exists in CrossRef
  * Supports DOI-based and text-based lookup

* 📊 **Smart Classification**

  * **Verified** — strong match with CrossRef record
  * **Possibly Real** — partial match, needs manual check
  * **Not Found** — no reliable record detected

* 🧾 **Multiple Input Formats**

  * APA, MLA, Chicago, Vancouver
  * Numbered lists (`[1]`, `(1)`, `1.`)
  * Paragraph-separated references

* 📤 **Export Options**

  * CSV (all / grouped)
  * APA format (.txt)
  * Vancouver format (.txt)
  * BibTeX (.bib)
  * Copy to clipboard

* 🎯 **Canonical Metadata**

  * Returns standardized metadata from CrossRef
  * Includes title, authors, journal, year, DOI

* ⚡ **No Setup Required**

  * No API key
  * No login
  * Runs entirely in the browser

---

## 🧠 How It Works

1. **DOI Detection**

   * If a DOI is present, it directly queries CrossRef for an exact match.

2. **Bibliographic Search**

   * If no DOI is found, the reference text is sent to the CrossRef API.
   * The best candidate is selected using:

     * Title token similarity
     * Year consistency

3. **Scoring & Classification**

   * High similarity → **Verified**
   * Medium similarity → **Possibly Real**
   * Low / no match → **Not Found**

---

## 🚀 Usage

1. Open the web page (`index.html`)
2. Paste your references into the input box
3. Click **“Verify References”**
4. Review grouped results
5. Export or copy verified citations

---

## 📦 Project Structure

```
.
├── index.html     # Main application (HTML + CSS + JS)
└── README.md      # Project documentation
```

---

## 🔌 API

This project uses the public **CrossRef REST API**:

* Base URL: [https://api.crossref.org](https://api.crossref.org)
* No authentication required
* Used for:

  * DOI resolution
  * Bibliographic search

---

## ⚠️ Limitations

* CrossRef does **not index all publications**

  * Some books, preprints, or regional journals may not appear
* Predatory or non-indexed journals may return **Not Found**
* Matching is heuristic-based (not guaranteed perfect)

---

## 🛠️ Tech Stack

* HTML5
* CSS3 (custom styling + responsive design)
* Vanilla JavaScript (no frameworks)
* CrossRef REST API

---

## 📄 License

This project is open-source and free to use.
(You can specify a license here, e.g., MIT if needed.)

---

## 👤 Author

Created by **Karcen Zheng**

* Website: [https://karcen.github.io/zhengjiacheng.github.io/](https://karcen.github.io/zhengjiacheng.github.io/)

---

If you want, I can also:

* make it more **academic / publication-style**
* or rewrite it as a **GitHub trending-level README (with badges, demo GIF, etc.)**
