# 隐信通 / InfoCloak

> 순수 프런트엔드 · 오프라인 · 전 형식 지원 데이터 마스킹 & 복원 도구 (V2)

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

**언어 / Language**：[中文](README.md) · [English](README.en.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Français](README.fr.md) · [Русский](README.ru.md)

---

## 태그

`데이터 마스킹` `데이터 보안` `개인정보 보호` `PII` `GDPR` `컴플라이언스` `오프라인 도구` `Excel 마스킹` `Word 마스킹` `PDF 마스킹` `OCR` `토큰화` `AES 암호화` `가역 마스킹` `일괄 처리` `글로벌 사전` `동일 값 동일 코드` `프런트엔드` `단일 파일` `오프라인`

---

## 개요

본 도구는 **단일 파일 · 순수 프런트엔드 · 오프라인 사용 가능**한 데이터 마스킹 및 복원 도구입니다. 네트워크 연결이나 서버 업로드가 필요 없으며, 모든 연산은 사용자의 브라우저(Chrome / Edge) 안에서 완료됩니다. 제3자, 협력사, 공개 채널과 데이터를 공유하기 전에 개인정보와 영업상 민감 정보를 마스킹하고, 허가된 범위에서 복원하는 데 사용합니다.

## 기능

- **전 형식 지원**: Excel / CSV / Word / PowerPoint / PDF / 이미지 / ZIP(중첩 포함) / 구버전 `.xls`(SheetJS 경유) / 구버전 `.doc`(docx로 다시 저장 안내)
- **마스킹 + 복원(양방향)**:
  - 구조화 문서(표, Word, PPT, ZIP 내 문서)는 **토큰화 / AES / 셔플 / 수치 반올림** 등의 가역 마스킹과 일관된 복원을 지원합니다.
  - **PDF / 이미지는 두 가지 모드 지원**:
    - 「가리기(비가역)」—— 레이아웃의 픽셀/벡터를 직접 검은 블록으로 가려 PDF/이미지의 물리적 특성에 부합합니다.
    - 「Word로 변환해 마스킹(가역)」—— 로컬 PDF 텍스트 엔진 / OCR로 글자와 양식 필드를 추출한 뒤 자동 토큰화하여 최소 `.docx`를 생성합니다. 토큰은 글로벌 사전에 등록되어 **사전으로 원문을 복원할 수 있습니다**.
- **13가지 민감 정보 인식**: 이름, 기관, 주민등록번호(신분증), 사업자등록번호(신용코드), 휴대전화, 유선전화, 은행카드, 이메일, 금액, 날짜, 주소, URL, 문서번호
- **다양한 방식**: 토큰화 / 마스킹 / 해시 / 일반화 / AES-GCM 암호화 / 무작위 셔플 / 수치 반올림(암호화된 나머지 열로 가역) / 열 삭제
- **글로벌 사전(동일 값 동일 코드)**: 파일 간·열 간에 같은 평문이 같은 토큰으로 매핑되어 연관성 일관성과 정확한 복원을 보장합니다. **패스프레이즈 보호 내보내기(AES 암호화 사전 파일)**를 지원합니다.
- **완전 오프라인**: PDF 텍스트 엔진(pdf.js)과 이미지 OCR(tesseract.js + 로컬 wasm + 중국어/영어 인식 언어 팩)이 모두 `libs/`에 로컬 패키징되어 있으며 CDN 폴백도 내장했습니다. **네트워크가 끊겨도 실행됩니다.**
- **일괄 처리**: 폴더 드래그 앤 드롭(재귀 순회 포함)과 다중 파일 드롭을 지원하며, 기본 전략으로 일괄 마스킹합니다. 실시간 진행 표시줄과 로그를 제공하고 결과를 ZIP으로 묶습니다.

## 지원 형식과 가역성

| 형식 | 마스킹 | 복원 |
|------|--------|------|
| CSV / Excel(.xls 포함) | 지원 | 지원 |
| Word / PowerPoint(PDF 양식 필드 포함) | 지원 | 지원 |
| ZIP(중첩 포함) | 지원 | 지원(재귀) |
| PDF / 이미지 · 가리기 | 지원 | 미지원(비가역) |
| PDF / 이미지 · Word 변환 모드 | 지원 | 지원(글로벌 사전 사용) |

> 참고: PDF / 이미지의 「Word 변환」 모드는 원래 레이아웃을 잃습니다(추출된 글자/필드와 토큰만 유지)지만 원문을 완전히 복원할 수 있습니다. 가리기는 레이아웃을 유지하며 비가역입니다. 두 모드는 문서 업로드 카드의 드롭다운에서 전환합니다.

## 디렉터리 구조

```
범용 마스킹 도구/
├─ InfoCloak_V2.html        # 메인 프로그램(Chrome/Edge로 더블클릭하여 열기)
├─ README.md                # 이 파일(루트)
├─ libs/                    # 로컬 의존성(완전 오프라인 구현)
│  ├─ xlsx.full.min.js      # 표 읽기/쓰기(구버전 .xls 포함)
│  ├─ jszip.min.js          # ZIP 읽기/쓰기
│  ├─ pdf-lib.min.js        # PDF 재그리기 및 가리기
│  ├─ pdfjs/                # 로컬 pdf.js(PDF 텍스트 추출)
│  │  ├─ pdf.min.js
│  │  └─ pdf.worker.min.js
│  └─ tesseract/            # 로컬 tesseract.js(이미지 OCR)
│     ├─ tesseract.min.js
│     ├─ worker.min.js
│     ├─ tesseract-core.wasm.js   # 자체 완결형 코어(wasm 내장, 오프라인 즉시 사용)
│     └─ tessdata/          # OCR 인식 언어 팩(중국어 chi_sim / 영어 eng)
│        ├─ chi_sim.traineddata.gz
│        └─ eng.traineddata.gz
├─ files/                   # 오프라인 문서(다크 모드가 메인 UI와 연동)
│  ├─ User_Guide.html
│  └─ Tech_Docs.html
└─ elders/                  # 이전 버전(V1 등)
```

## 빠른 시작

1. `InfoCloak_V2.html`을 Chrome / Edge로 엽니다(더블클릭).
2. 왼쪽 메뉴에서 기능 선택: ① 표 마스킹 ② 문서 마스킹 ③ 복원 ④ 글로벌 사전.
3. 파일 업로드 → 방식 선택(PDF/이미지는 문서 카드에서 「가리기 / Word 변환」 전환) → 생성 → 마스킹 결과 다운로드.
4. **일괄 처리**: 폴더 전체를 「일괄 처리」 영역에 드롭하거나 폴더를 선택합니다. 시작 후 기본 전략으로 마스킹하여 ZIP으로 묶고 진행 상황을 표시합니다.
5. 복원이 필요하면 「③ 복원」에서 마스킹된 파일 + 마스터 사전을 업로드합니다(암호화 사전은 먼저 패스프레이즈를 입력해 불러오기).

## 글로벌 사전과 패스프레이즈 보호

- 글로벌 사전은 파일 간/열 간 「동일 값 동일 코드」를 보장하며 복원의 유일한 근거입니다.
- 내보내기 시 **패스프레이즈**를 설정할 수 있습니다. 사전은 AES-GCM(PBKDF2 키 유도, 150000회 반복)으로 암호화되어 `salt`/`iv`/`ct`를 포함한 `.json` 패키지로 저장됩니다.
- 암호화 사전을 불러올 때는 올바른 패스프레이즈가 필요합니다. 패스프레이즈는 사전 파일에 기록되지 않으며 이번 세션의 키 유도에만 사용됩니다.
- **마스터 사전에는 모든 평문 매핑이 담겨 있어 가장 민감한 자산입니다. 반드시 로컬에 보관하고 마스킹 파일과 함께 외부로 보내지 마세요.**

## 마스킹 방식의 가역성

| 방식 | 가역 | 복원에 필요한 것 |
|------|------|-----------------|
| 토큰화 | 예 | 마스터 사전 |
| AES 암호화 | 예 | 마스터 사전 + 패스프레이즈 |
| 무작위 셔플 | 예 | 마스터 사전(값 매핑) |
| 수치 반올림·가역 | 예 | 마스터 사전 + 패스프레이즈 |
| 마스킹 / 해시 / 일반화 / 삭제 / 가리기 | 아니오 | — |

## ⚠️ 사전 다운로드 선택 규칙(필독)

**사전은 자동 저장되지 않습니다!** 마스킹 완료 후 사전은 브라우저 메모리에만 존재하며 페이지를 닫으면 사라집니다. 「④ 글로벌 사전」에서 직접 다운로드해야 합니다.

| 마스킹에 사용한 방식 | ④에서 다운로드할 것 |
|---|---|
| 토큰화 / 셔플만 | **`主字典.json`(마스터 사전.json) 다운로드**(평문) |
| AES 암호화 / 수치 반올림·가역 | **`加密主字典.json`(암호화 마스터 사전.json) 다운로드** + 패스프레이즈 입력 |
| 마스킹 / 해시 / 일반화 / 삭제 | 불필요(비가역, 복원 불가) |

**복원 시 대응 관계**: `主字典.json`을 다운로드했다면 → 그것을 업로드하고 패스프레이즈는 비움; `主字典_加密.json`을 다운로드했다면 → 그것을 업로드하고 설정 당시의 패스프레이즈를 입력.

## 개인정보 및 보안

- 데이터는 기기 밖으로 나가지 않으며 네트워크 업로드가 없습니다(`libs/` 로컬화로 오프라인 실행 가능).
- 암호화 패스프레이즈는 이번 세션의 키 유도에만 사용되며 사전 파일에 기록되지 않습니다.
- **마스터 사전에는 모든 평문 매핑이 담겨 있어 가장 민감한 자산입니다. 반드시 로컬에 보관하고 마스킹 파일과 함께 외부로 보내지 마세요.**
- 본 도구는 정보 정리 및 학습용으로 제공되며 데이터의 완전한 안전을 보장하지 않습니다. 원본 파일을 백업하세요.

## 알려진 제한

- PDF / 이미지의 「Word 변환」 모드는 텍스트 추출에 의존하며, 스캔 원본의 마스킹 품질은 OCR 인식률에 따라 달라집니다. 복잡한 레이아웃은 일반 텍스트로 단순화됩니다.
- 구버전 `.doc`은 직접 파싱할 수 없습니다. 먼저 Word / WPS에서 `.docx`로 다시 저장하세요.
- 가리기 방식의 PDF / 이미지는 비가역입니다. 복원이 필요하지 않은지 확인한 뒤 사용하세요.

## 라이선스

[MIT](https://opensource.org/licenses/MIT) —— 자유롭게 사용·수정·재배포할 수 있습니다. 원저작자 정보를 유지해 주세요.

**원저작자**: SuperLaos ｜ **위챗 공식 계정**: 技术宅SuperLaos
