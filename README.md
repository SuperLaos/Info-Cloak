# 隐信通 / InfoCloak

> 纯前端 · 离线 · 全格式数据脱敏与还原工具（V2）
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
[![Chinese](https://img.shields.io/badge/chinese-ff6b6b?style=for-the-badge)](https://github.com/SuperLaos/Info-Cloak)
[![MIT](https://img.shields.io/badge/license-MIT-blue?style=for-the-badge)](https://opensource.org/licenses/MIT)

**中文** | [English](#english)

---

## 标签 | Tags

`数据脱敏` `数据安全` `隐私保护` `PII` `GDPR` `合规` `离线工具` `Excel脱敏` `Word脱敏` `PDF脱敏` `OCR` `令牌化` `AES加密` `可逆脱敏` `批量处理` `全局字典` `同值同码` `前端` `单文件` `中文`

---

## 中文说明

### 简介

本工具是一个**单文件、纯前端、离线可用**的数据脱敏与还原工具。无需联网、无需上传服务器，所有计算都在你本机浏览器内完成（Chrome / Edge）。适用于在向第三方、合作方、公开渠道分享数据前，对个人隐私与商业敏感信息进行脱敏，并在授权范围内还原。

### 功能特性

- **全格式覆盖**：Excel / CSV / Word / PowerPoint / PDF / 图片 / ZIP（含嵌套）/ 旧版 `.xls`（经 SheetJS）/ 旧版 `.doc`（提示另存为 docx）
- **脱敏 + 还原（双向）**：
  - 结构化文档（表格、Word、PPT、ZIP 内文档）支持**令牌化 / AES / 洗牌 / 数值取整**等可逆脱敏与一致还原；
  - **PDF / 图片支持两种模式**：
    - 「遮挡式（不可逆）」—— 直接对版面像素/矢量做黑块遮挡，符合 PDF/图片的物理特性；
    - 「转为 Word 脱敏（可逆）」—— 先用本地 PDF 文本引擎 / OCR 抽取文字与表单字段，自动令牌化后生成最小 `.docx`，令牌进入全局字典，**可凭字典还原原文**。
- **13 类敏感识别**：姓名、机构、身份证、信用代码、手机、固话、银行卡、邮箱、金额、日期、地址、网址、文书编号
- **多种方法**：令牌化 / 掩码 / 哈希 / 泛化 / AES-GCM 加密 / 随机洗牌 / 数值取整（可逆带加密余项列）/ 删除列
- **全局字典（同值同码）**：跨文件、跨列同一明文映射同一令牌，保证关联一致与一致还原；支持**口令保护导出（AES 加密字典文件）**
- **彻底离线**：PDF 文本引擎（pdf.js）、图片 OCR（tesseract.js + 本地 wasm + OCR 中文/英文识别语言包）均已本地化打包于 `libs/`，并内建 CDN 回退；**完全断网亦可运行**
- **批量处理**：支持文件夹拖拽（含递归遍历）与多文件拖拽，按默认策略批量脱敏，实时进度条与日志，结果汇总为 ZIP

### 支持格式与可逆性

| 格式 | 脱敏 | 还原 |
|------|------|------|
| CSV / Excel（含 .xls） | 支持 | 支持 |
| Word / PowerPoint（含 PDF 表单字段） | 支持 | 支持 |
| ZIP（含嵌套） | 支持 | 支持（递归） |
| PDF / 图片 · 遮挡式 | 支持 | 不支持（不可逆） |
| PDF / 图片 · 转 Word 模式 | 支持 | 支持（凭全局字典） |

> 说明：PDF / 图片「转 Word」模式会损失原有排版（仅保留抽取出的文字/字段与令牌），但可完整还原原文；遮挡式则保留版面、不可逆。两种模式在文档上传卡中通过下拉切换。

### 目录结构

```
通用脱敏工具/
├─ InfoCloak_V2.html        # 主程序（双击用 Chrome/Edge 打开）
├─ README.md                # 本文件（根目录）
├─ libs/                    # 本地化依赖（实现彻底离线）
│  ├─ xlsx.full.min.js      # 表格读写（含旧版 .xls）
│  ├─ jszip.min.js          # ZIP 读写
│  ├─ pdf-lib.min.js        # PDF 重绘遮挡
│  ├─ pdfjs/                # 本地 pdf.js（PDF 文本抽取）
│  │  ├─ pdf.min.js
│  │  └─ pdf.worker.min.js
│  └─ tesseract/            # 本地 tesseract.js（图片 OCR）
│     ├─ tesseract.min.js
│     ├─ worker.min.js
│     ├─ tesseract-core.wasm.js   # 自包含核心（已内联 wasm，离线即用）
│     └─ tessdata/          # OCR 识别语言包（中文 chi_sim / 英文 eng）
│        ├─ chi_sim.traineddata.gz
│        └─ eng.traineddata.gz
├─ files/                   # 离线文档（深色模式随主界面同步）
│  ├─ User_Guide.html
│  └─ Tech_Docs.html
└─ elders/                  # 历史版本（V1 等）
```

### 快速开始

1. 用 Chrome / Edge 打开 `InfoCloak_V2.html`（双击即可）。
2. 左侧菜单选择功能：① 表格脱敏 ② 文档脱敏 ③ 还原 ④ 全局字典。
3. 上传文件 → 选择方法（PDF/图片可在文档卡切换「遮挡式 / 转 Word」）→ 生成 → 下载脱敏产物。
4. **批量**：把整个文件夹拖入「批量处理」区，或点击选择文件夹，开始后即按默认策略脱敏并汇总为 ZIP，实时显示进度。
5. 需还原时，到「③ 还原」上传脱敏文件 + 主字典（加密字典需先输入口令导入）。

### 全局字典与口令保护

- 全局字典保证「同值同码」，跨文件/跨列一致，是还原的唯一依据。
- 导出时可设置**口令**：字典经 AES-GCM（PBKDF2 派生密钥，150000 迭代）加密后保存为 `.json` 包（含 `salt`/`iv`/`ct`）。
- 导入加密字典时需输入正确口令；口令从不写入字典文件，仅用于本次会话派生密钥。
- **主字典含全部明文映射，是最高敏感资产，务必本地独掌、严禁随脱敏文件外发。**

### 脱敏方法可逆性

| 方法 | 可逆 | 还原所需 |
|------|------|----------|
| 令牌化 | 是 | 主字典 |
| AES 加密 | 是 | 主字典 + 口令 |
| 随机洗牌 | 是 | 主字典（按值映射） |
| 数值取整·可逆 | 是 | 主字典 + 口令 |
| 掩码 / 哈希 / 泛化 / 删除 / 遮挡 | 否 | — |

### ⚠️ 字典下载选择规则（必读）

**字典不会自动保存！** 脱敏完成后字典仅存于浏览器内存，关闭页面即丢失。必须手动去「④ 全局字典」下载。

| 脱敏时使用的方法 | 去④下载哪个 |
|---|---|
| 仅令牌化 / 随机洗牌 | **下载 主字典.json**（明文） |
| AES 加密 / 数值取整·可逆 | **下载 加密主字典.json** + 填写口令 |
| 掩码 / 哈希 / 泛化 / 删除 | 不需要（不可逆，无法还原） |

**还原时对应关系**：下载的是 `主字典.json` → 上传它 + 口令留空；下载的是 `主字典_加密.json` → 上传它 + 填写当时设的口令。

### 隐私与安全

- 数据全程不出本机，无网络上传（libs 本地化后断网亦可运行）。
- 加密口令仅用于本次会话派生密钥，不写入字典文件。
- **主字典含全部明文映射，是最高敏感资产，务必本地独掌、严禁随脱敏文件外发。**
- 本工具仅供信息整理与学习，不保证数据完全安全，请注意备份源文件。

### 已知限制

- PDF / 图片「转 Word」模式依赖文本抽取，扫描件脱敏质量取决于 OCR 识别率；复杂排版会简化为纯文字。
- 旧版 `.doc` 无法直接解析，请先在 Word/WPS 中另存为 `.docx`。
- 遮挡式 PDF/图片不可逆，请确认无需还原后再使用。

### 许可证

[MIT](https://opensource.org/licenses/MIT) —— 可自由使用、修改与再分发，请保留原创作者信息。

**原创作者**：SuperLaos ｜ **公众号**：技术宅SuperLaos

---

<span id="english"></span>

## English

### Overview

A **single-file, pure-frontend, offline** data masking and restoration tool. No server, no network upload — all computation runs locally in your browser (Chrome / Edge). Use it to mask personal and commercially sensitive information before sharing data with third parties, and to restore it within authorized scope.

### Features

- **All-format coverage**: Excel / CSV / Word / PowerPoint / PDF / Images / ZIP (nested) / legacy `.xls` (via SheetJS) / legacy `.doc` (prompt to re-save as docx)
- **Mask & Restore (both directions)**:
  - Structured documents (tables, Word, PPT, in-ZIP docs) support reversible masking (tokenization / AES / shuffle / rounding) with consistent restoration.
  - **PDF / Images support two modes**:
    - *Redaction (irreversible)* — black-out pixels/vectors directly, matching the physical nature of PDF/images.
    - *Convert to Word (reversible)* — extract text and form fields via a local PDF engine / OCR, auto-tokenize, then emit a minimal `.docx`. Tokens enter the global dictionary, so **the original text can be restored with the dictionary**.
- **13 sensitive categories**: name, org, ID card, credit code, mobile, landline, bank card, email, money, date, address, URL, document no.
- **Multiple methods**: tokenization / masking / hashing / generalization / AES-GCM encryption / shuffle / numeric rounding (reversible with encrypted remainder column) / column drop
- **Global dictionary (same-value-same-code)**: one plaintext maps to one token across files and columns; supports **passphrase-protected export (AES-encrypted dictionary file)**
- **Fully offline**: PDF text engine (pdf.js) and image OCR (tesseract.js + local wasm + zh/en language packs) are bundled under `libs/`, with built-in CDN fallback — **runs with no network at all**
- **Batch processing**: folder drag-and-drop (recursive) and multi-file drop, default-strategy masking, live progress bar + log, results zipped

### Supported formats & reversibility

| Format | Mask | Restore |
|--------|------|---------|
| CSV / Excel (incl. .xls) | Yes | Yes |
| Word / PowerPoint (incl. PDF form fields) | Yes | Yes |
| ZIP (nested) | Yes | Yes (recursive) |
| PDF / Images · Redaction | Yes | No (irreversible) |
| PDF / Images · To-Word mode | Yes | Yes (via global dictionary) |

### Quick start

1. Open `InfoCloak_V2.html` with Chrome / Edge (double-click).
2. Pick a function from the left menu: ① Table ② Document ③ Restore ④ Global Dictionary.
3. Upload file → choose method (for PDF/images, switch *Redaction / To-Word* in the document card) → generate → download masked output.
4. **Batch**: drop a whole folder into the Batch area (or pick a folder); masking runs with the default strategy and results are zipped, with live progress.
5. To restore, go to ③ Restore, upload the masked file + master dictionary (encrypted dictionaries need the passphrase first).

### Global dictionary & passphrase

- The global dictionary guarantees same-value-same-code across files/columns and is the sole basis for restoration.
- On export you may set a **passphrase**: the dictionary is AES-GCM encrypted (PBKDF2 key derivation, 150,000 iterations) and saved as a `.json` package (`salt`/`iv`/`ct`).
- Importing an encrypted dictionary requires the correct passphrase; the passphrase is never written to the dictionary file.
- **The master dictionary contains all plaintext mappings and is the highest-sensitivity asset — keep it local and never distribute it with masked files.**

### Method reversibility

| Method | Reversible | Needs |
|--------|-----------|-------|
| Tokenization | Yes | Master dictionary |
| AES encryption | Yes | Dictionary + passphrase |
| Shuffle | Yes | Dictionary (value-map) |
| Reversible rounding | Yes | Dictionary + passphrase |
| Mask / Hash / Generalize / Drop / Redaction | No | — |

### Privacy & security

- Data never leaves your machine; no network upload (works fully offline once `libs/` is localized).
- The passphrase is used only to derive the key for the session and is never written to the dictionary file.
- **The master dictionary contains all plaintext mappings and is the highest-sensitivity asset — keep it local and never distribute it with masked files.**
- Provided for information organizing and learning; not guaranteed fully safe — back up your source files.

### Known limitations

- The PDF/Image "To-Word" mode relies on text extraction; scan quality depends on OCR accuracy, and complex layouts are simplified to plain text.
- Legacy `.doc` cannot be parsed directly — re-save as `.docx` in Word/WPS first.
- Redaction mode for PDF/images is irreversible; confirm you don't need restoration before using it.

### License

[MIT](https://opensource.org/licenses/MIT) — free to use, modify, and redistribute; please retain the original author attribution.

**Author**: SuperLaos ｜ **WeChat public account**: 技术宅SuperLaos
