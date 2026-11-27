# InfoCloak

> Pure-frontend, offline, all-format data masking & restoration tool (V2)

[![Data Masking](https://img.shields.io/badge/data-masking-blue?style=for-the-badge)](https://github.com/SuperLaos/Info-Cloak)
[![Data Security](https://img.shields.io/badge/data-security-green?style=for-the-badge)](https://github.com/SuperLaos/Info-Cloak)
[![Privacy](https://img.shields.io/badge/privacy-purple?style=for-the-badge)](https://github.com/SuperLaos/Info-Cloak)
[![GDPR](https://img.shields.io/badge/GDPR-orange?style=for-the-badge)](https://github.com/SuperLaos/Info-Cloak)
[![Compliance](https://img.shields.io/badge/compliance-red?style=for-the-badge)](https://github.com/SuperLaos/Info-Cloak)
[![Offline](https://img.shields.io/badge/offline-success?style=for-the-badge)](https://github.com/SuperLaos/Info-Cloak)
[![Excel](https://img.shields.io/badge/excel-blue?style=for-the-badge)](https://github.com/SuperLaos/Info-Cloak)
[![PDF](https://img.shields.io/badge/pdf-red?style=for-the-badge)](https://github.com/SuperLaos/Info-Cloak)
[![OCR](https://img.shields.io/badge/OCR-teal?style=for-the-badge)](https://github.com/SuperLaos/Info-Cloak)
[![Tokenization](https://img.shields.io/badge/tokenization-cyan?style=for-the-badge)](https://github.com/SuperLaos/Info-Cloak)
[![AES](https://img.shields.io/badge/AES-encryption-yellow?style=for-the-badge)](https://github.com/SuperLaos/Info-Cloak)
[![Reversible](https://img.shields.io/badge/reversible-lightgreen?style=for-the-badge)](https://github.com/SuperLaos/Info-Cloak)
[![Batch](https://img.shields.io/badge/batch%20processing-emerald?style=for-the-badge)](https://github.com/SuperLaos/Info-Cloak)
[![HTML](https://img.shields.io/badge/html-frontend-slate?style=for-the-badge)](https://github.com/SuperLaos/Info-Cloak)
[![MIT](https://img.shields.io/badge/license-MIT-blue?style=for-the-badge)](https://opensource.org/licenses/MIT)

**Language / 语言**：[中文](README.md) · [English](README.en.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Français](README.fr.md) · [Русский](README.ru.md)

---

## Tags

`data masking` `data security` `privacy` `PII` `GDPR` `compliance` `offline tool` `Excel masking` `Word masking` `PDF masking` `OCR` `tokenization` `AES encryption` `reversible masking` `batch processing` `global dictionary` `same-value-same-code` `frontend` `single file` `offline`

---

## Overview

A **single-file, pure-frontend, offline** data masking and restoration tool. No server, no network upload — all computation runs locally in your browser (Chrome / Edge). Use it to mask personal and commercially sensitive information before sharing data with third parties, partners, or public channels, and to restore it within authorized scope.

## Features

- **All-format coverage**: Excel / CSV / Word / PowerPoint / PDF / Images / ZIP (nested) / legacy `.xls` (via SheetJS) / legacy `.doc` (prompt to re-save as docx)
- **Mask & Restore (both directions)**:
  - Structured documents (tables, Word, PPT, in-ZIP docs) support reversible masking (tokenization / AES / shuffle / rounding) with consistent restoration.
  - **PDF / Images support two modes**:
    - *Redaction (irreversible)* — black-out pixels/vectors directly, matching the physical nature of PDF/images.
    - *Convert to Word (reversible)* — extract text and form fields via a local PDF engine / OCR, auto-tokenize, then emit a minimal `.docx`. Tokens enter the global dictionary, so **the original text can be restored with the dictionary**.
- **13 sensitive categories**: name, organization, ID card, credit code, mobile, landline, bank card, email, money, date, address, URL, document number.
- **Multiple methods**: tokenization / masking / hashing / generalization / AES-GCM encryption / shuffle / numeric rounding (reversible with encrypted remainder column) / column drop
- **Global dictionary (same-value-same-code)**: one plaintext maps to one token across files and columns, keeping associations consistent and restoration exact; supports **passphrase-protected export (AES-encrypted dictionary file)**.
- **Fully offline**: PDF text engine (pdf.js) and image OCR (tesseract.js + local wasm + zh/en language packs) are bundled under `libs/`, with built-in CDN fallback — **runs with no network at all**.
- **Batch processing**: folder drag-and-drop (recursive) and multi-file drop, default-strategy masking, live progress bar and log, results zipped.

## Supported formats & reversibility

| Format | Mask | Restore |
|--------|------|---------|
| CSV / Excel (incl. .xls) | Yes | Yes |
| Word / PowerPoint (incl. PDF form fields) | Yes | Yes |
| ZIP (nested) | Yes | Yes (recursive) |
| PDF / Images · Redaction | Yes | No (irreversible) |
| PDF / Images · To-Word mode | Yes | Yes (via global dictionary) |

> Note: the PDF/Image "To-Word" mode loses the original layout (only extracted text/fields and tokens are kept) but can fully restore the original text; redaction preserves the layout and is irreversible. Switch between the two modes via the dropdown in the document upload card.

## Directory structure

```
Universal Masking Tool/
├─ InfoCloak_V2.html        # Main program (double-click to open with Chrome/Edge)
├─ README.md                # This file (root)
├─ libs/                    # Localized dependencies (enable full offline use)
│  ├─ xlsx.full.min.js      # Spreadsheet read/write (incl. legacy .xls)
│  ├─ jszip.min.js          # ZIP read/write
│  ├─ pdf-lib.min.js        # PDF redraw & redaction
│  ├─ pdfjs/                # Local pdf.js (PDF text extraction)
│  │  ├─ pdf.min.js
│  │  └─ pdf.worker.min.js
│  └─ tesseract/            # Local tesseract.js (image OCR)
│     ├─ tesseract.min.js
│     ├─ worker.min.js
│     ├─ tesseract-core.wasm.js   # Self-contained core (wasm inlined, works offline)
│     └─ tessdata/          # OCR language packs (Chinese chi_sim / English eng)
│        ├─ chi_sim.traineddata.gz
│        └─ eng.traineddata.gz
├─ files/                   # Offline docs (dark mode follows the main UI)
│  ├─ User_Guide.html
│  └─ Tech_Docs.html
└─ elders/                  # Historical versions (V1, etc.)
```

## Quick start

1. Open `InfoCloak_V2.html` with Chrome / Edge (double-click).
2. Pick a function from the left menu: ① Table ② Document ③ Restore ④ Global Dictionary.
3. Upload file → choose method (for PDF/images, switch *Redaction / To-Word* in the document card) → generate → download masked output.
4. **Batch**: drop a whole folder into the Batch area (or pick a folder); masking runs with the default strategy and results are zipped, with live progress.
5. To restore, go to ③ Restore, upload the masked file + master dictionary (encrypted dictionaries need the passphrase first).

## Global dictionary & passphrase

- The global dictionary guarantees same-value-same-code across files/columns and is the sole basis for restoration.
- On export you may set a **passphrase**: the dictionary is AES-GCM encrypted (PBKDF2 key derivation, 150,000 iterations) and saved as a `.json` package (`salt`/`iv`/`ct`).
- Importing an encrypted dictionary requires the correct passphrase; the passphrase is never written into the dictionary file and is used only to derive the key for the current session.
- **The master dictionary contains all plaintext mappings and is the highest-sensitivity asset — keep it local and never distribute it with masked files.**

## Method reversibility

| Method | Reversible | Needs |
|--------|-----------|-------|
| Tokenization | Yes | Master dictionary |
| AES encryption | Yes | Master dictionary + passphrase |
| Shuffle | Yes | Master dictionary (value-map) |
| Reversible rounding | Yes | Master dictionary + passphrase |
| Mask / Hash / Generalize / Drop / Redaction | No | — |

## ⚠️ Dictionary download rules (must read)

**The dictionary is NOT saved automatically!** After masking, the dictionary lives only in browser memory and is lost when the page is closed. You must manually download it from ④ Global Dictionary.

| Method used for masking | What to download from ④ |
|---|---|
| Tokenization / Shuffle only | **Download `master_dictionary.json`** (plaintext) |
| AES encryption / Reversible rounding | **Download `encrypted_master_dictionary.json`** + set a passphrase |
| Mask / Hash / Generalize / Drop | Not needed (irreversible, cannot be restored) |

**Restoration mapping**: downloaded `master_dictionary.json` → upload it and leave the passphrase blank; downloaded `master_dictionary_encrypted.json` → upload it and enter the passphrase you set.

## Privacy & security

- Data never leaves your machine; no network upload (works fully offline once `libs/` is localized).
- The passphrase is used only to derive the key for the session and is never written into the dictionary file.
- **The master dictionary contains all plaintext mappings and is the highest-sensitivity asset — keep it local and never distribute it with masked files.**
- Provided for information organizing and learning; not guaranteed fully safe — back up your source files.

## Known limitations

- The PDF/Image "To-Word" mode relies on text extraction; scan quality depends on OCR accuracy, and complex layouts are simplified to plain text.
- Legacy `.doc` cannot be parsed directly — re-save as `.docx` in Word/WPS first.
- Redaction mode for PDF/images is irreversible; confirm you don't need restoration before using it.

## License

[MIT](https://opensource.org/licenses/MIT) — free to use, modify, and redistribute; please retain the original author attribution.

**Author**: SuperLaos ｜ **WeChat Official Account**: 技术宅SuperLaos
