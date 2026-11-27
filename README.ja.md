# 隐信通 / InfoCloak

> 纯前端・オフライン・全形式対応のデータマスキング＆復元ツール（V2）

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

**言語 / Language**：[中文](README.md) · [English](README.en.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Français](README.fr.md) · [Русский](README.ru.md)

---

## タグ

`データマスキング` `データセキュリティ` `プライバシー保護` `PII` `GDPR` `コンプライアンス` `オフラインツール` `Excelマスキング` `Wordマスキング` `PDFマスキング` `OCR` `トークン化` `AES暗号化` `可逆マスキング` `一括処理` `グローバル辞書` `同値同コード` `フロントエンド` `単一ファイル` `オフライン`

---

## 概要

本ツールは**単一ファイル・純フロントエンド・オフライン対応**のデータマスキング＆復元ツールです。ネットワーク接続やサーバーへのアップロードは不要で、すべての処理はお使いのブラウザ（Chrome / Edge）内で完結します。第三者・取引先・公開チャネルとデータを共有する前に、個人情報や営業上の機微情報をマスキングし、許可された範囲で復元するために使用します。

## 機能

- **全形式対応**：Excel / CSV / Word / PowerPoint / PDF / 画像 / ZIP（入れ子対応）/ 旧形式 `.xls`（SheetJS 経由）/ 旧形式 `.doc`（docx への再保存を案内）
- **マスキング ＋ 復元（双方向）**：
  - 構造化ドキュメント（表、Word、PPT、ZIP 内のドキュメント）は**トークン化 / AES / シャッフル / 数値丸め**などの可逆マスキングと一貫した復元に対応。
  - **PDF / 画像は 2 つのモードに対応**：
    - 「塗りつぶし（不可逆）」—— 版面のピクセル／ベクタを直接黒塗りし、PDF／画像の物理的特性に適合。
    - 「Word に変換してマスキング（可逆）」—— ローカルの PDF テキストエンジン / OCR で文字とフォーム項目を抽出し、自動トークン化して最小限の `.docx` を生成。トークンはグローバル辞書に登録され、**辞書により原文を復元可能**。
- **13 種類の機微情報認識**：氏名、組織、身分証番号、法人番号、携帯番号、固定電話、銀行口座、メール、金額、日付、住所、URL、文書番号
- **多彩な手法**：トークン化 / マスキング / ハッシュ / 一般化 / AES-GCM 暗号化 / ランダムシャッフル / 数値丸め（暗号化された余剰列による可逆）/ 列削除
- **グローバル辞書（同値同コード）**：ファイル間・列間で同じ平文が同じトークンにマッピングされ、関連性の一貫性と正確な復元を保証。**パスフレーズ保護によるエクスポート（AES 暗号化辞書ファイル）**に対応。
- **完全オフライン**：PDF テキストエンジン（pdf.js）と画像 OCR（tesseract.js + ローカル wasm + 中国語／英語認識言語パック）はすべて `libs/` にローカルパッケージされ、CDN フォールバックも内蔵。**ネットワーク遮断時でも動作**。
- **一括処理**：フォルダのドラッグ＆ドロップ（再帰走査含む）と複数ファイルのドラッグに対応し、デフォルト戦略で一括マスキング。リアルタイムの進捗バーとログを表示し、結果を ZIP にまとめる。

## 対応形式と可逆性

| 形式 | マスキング | 復元 |
|------|-----------|------|
| CSV / Excel（.xls 含む） | 対応 | 対応 |
| Word / PowerPoint（PDF フォーム項目含む） | 対応 | 対応 |
| ZIP（入れ子対応） | 対応 | 対応（再帰） |
| PDF / 画像・塗りつぶし | 対応 | 非対応（不可逆） |
| PDF / 画像・Word 変換モード | 対応 | 対応（グローバル辞書による） |

> 補足：PDF / 画像の「Word 変換」モードは元のレイアウトを失います（抽出された文字／項目とトークンのみ保持）が、原文を完全に復元できます。塗りつぶしはレイアウトを保持し、不可逆です。2 つのモードはドキュメントアップロード欄のドロップダウンで切り替えます。

## ディレクトリ構成

```
汎用マスキングツール/
├─ InfoCloak_V2.html        # メインプログラム（Chrome/Edge でダブルクリックして開く）
├─ README.md                # このファイル（ルート）
├─ libs/                    # ローカル依存（完全オフライン化のため）
│  ├─ xlsx.full.min.js      # 表の読み書き（旧形式 .xls 含む）
│  ├─ jszip.min.js          # ZIP の読み書き
│  ├─ pdf-lib.min.js        # PDF の再描画と塗りつぶし
│  ├─ pdfjs/                # ローカル pdf.js（PDF テキスト抽出）
│  │  ├─ pdf.min.js
│  │  └─ pdf.worker.min.js
│  └─ tesseract/            # ローカル tesseract.js（画像 OCR）
│     ├─ tesseract.min.js
│     ├─ worker.min.js
│     ├─ tesseract-core.wasm.js   # 自己完結型コア（wasm 内蔵、オフラインで動作）
│     └─ tessdata/          # OCR 言語パック（中国語 chi_sim / 英語 eng）
│        ├─ chi_sim.traineddata.gz
│        └─ eng.traineddata.gz
├─ files/                   # オフラインドキュメント（ダークモードは本体に連動）
│  ├─ User_Guide.html
│  └─ Tech_Docs.html
└─ elders/                  # 過去バージョン（V1 など）
```

## クイックスタート

1. `InfoCloak_V2.html` を Chrome / Edge で開きます（ダブルクリックで可）。
2. 左メニューから機能を選択：① 表マスキング ② ドキュメントマスキング ③ 復元 ④ グローバル辞書。
3. ファイルをアップロード → 手法を選択（PDF／画像はドキュメント欄で「塗りつぶし / Word 変換」を切替）→ 生成 → マスキング結果をダウンロード。
4. **一括処理**：フォルダ全体を「一括処理」エリアにドロップ、またはフォルダを選択。開始後はデフォルト戦略でマスキングし、ZIP にまとめて進捗を表示します。
5. 復元が必要な場合は「③ 復元」でマスキング済みファイル ＋ マスター辞書をアップロード（暗号化辞書は先にパスフレーズを入力して読み込み）。

## グローバル辞書とパスフレーズ保護

- グローバル辞書はファイル間／列間の「同値同コード」を保証し、復元の唯一の根拠となります。
- エクスポート時に**パスフレーズ**を設定できます：辞書は AES-GCM（PBKDF2 による鍵導出、150000 回迭代）で暗号化され、`salt`/`iv`/`ct` を含む `.json` パッケージとして保存されます。
- 暗号化辞書の読み込みには正しいパスフレーズが必要です。パスフレーズは辞書ファイルに書き込まれず、今回のセッションの鍵導出にのみ使用されます。
- **マスター辞書にはすべての平文マッピングが含まれ、最も機密性の高い資産です。必ずローカルで管理し、マスキング済みファイルと一緒に外部へ送らないでください。**

## マスキング手法の可逆性

| 手法 | 可逆 | 復元に必要なもの |
|------|------|-----------------|
| トークン化 | はい | マスター辞書 |
| AES 暗号化 | はい | マスター辞書 ＋ パスフレーズ |
| ランダムシャッフル | はい | マスター辞書（値マッピング） |
| 数値丸め・可逆 | はい | マスター辞書 ＋ パスフレーズ |
| マスキング / ハッシュ / 一般化 / 削除 / 塗りつぶし | いいえ | — |

## ⚠️ 辞書ダウンロードの選択ルール（必読）

**辞書は自動保存されません！** マスキング後、辞書はブラウザのメモリにのみ存在し、ページを閉じると失われます。「④ グローバル辞書」から手動でダウンロードしてください。

| マスキングに使用した手法 | ④でダウンロードするもの |
|---|---|
| トークン化 / シャッフルのみ | **`主字典.json`（マスター辞書.json）をダウンロード**（平文） |
| AES 暗号化 / 数値丸め・可逆 | **`加密主字典.json`（暗号化マスター辞書.json）をダウンロード** ＋ パスフレーズを入力 |
| マスキング / ハッシュ / 一般化 / 削除 | 不要（不可逆、復元不可） |

**復元時の対応関係**：ダウンロードしたのが `主字典.json` → それをアップロードしパスフレーズは空欄；`主字典_加密.json` → それをアップロードし設定時のパスフレーズを入力。

## プライバシーとセキュリティ

- データは一切端末外に出ず、ネットワークへアップロードされません（`libs/` のローカル化によりオフラインでも動作）。
- 暗号化パスフレーズは本次セッションの鍵導出にのみ使用され、辞書ファイルには書き込まれません。
- **マスター辞書にはすべての平文マッピングが含まれ、最も機密性の高い資産です。必ずローカルで管理し、マスキング済みファイルと一緒に外部へ送らないでください。**
- 本ツールは情報整理と学習のみを目的とし、データの完全な安全性を保証するものではありません。ソースファイルのバックアップにご注意ください。

## 既知の制限

- PDF / 画像の「Word 変換」モードはテキスト抽出に依存し、スキャン原稿のマスキング品質は OCR 認識率に左右されます。複雑なレイアウトはプレーンテキストに簡略化されます。
- 旧形式 `.doc` は直接解析できません。先に Word / WPS で `.docx` として再保存してください。
- 塗りつぶし方式の PDF / 画像は不可逆です。復元が不要であることを確認してから使用してください。

## ライセンス

[MIT](https://opensource.org/licenses/MIT) —— 自由に使用・改変・再配布できます。原作者の情報を保持してください。

**原作者**：SuperLaos ｜ **WeChat 公式アカウント**：技术宅SuperLaos
