# 隐信通 / InfoCloak

> Outil de masquage et de restauration de données, purement frontal, hors ligne, tous formats (V2)

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

**Langue / Language**：[中文](README.md) · [English](README.en.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Français](README.fr.md) · [Русский](README.ru.md)

---

## Étiquettes

`masquage de données` `sécurité des données` `protection de la vie privée` `PII` `GDPR` `conformité` `outil hors ligne` `masquage Excel` `masquage Word` `masquage PDF` `OCR` `tokenisation` `chiffrement AES` `masquage réversible` `traitement par lots` `dictionnaire global` `même valeur, même code` `frontend` `fichier unique` `hors ligne`

---

## Aperçu

Cet outil est un utilitaire de **masquage et de restauration de données, en fichier unique, purement frontal et utilisable hors ligne**. Aucune connexion réseau ni envoi vers un serveur n'est nécessaire : tous les calculs s'effectuent dans votre navigateur local (Chrome / Edge). Il permet de masquer les données personnelles et les informations commerciales sensibles avant de les partager avec des tiers, des partenaires ou des canaux publics, puis de les restaurer dans le cadre autorisé.

## Fonctionnalités

- **Tous formats couverts** : Excel / CSV / Word / PowerPoint / PDF / images / ZIP (imbriqué) / ancien `.xls` (via SheetJS) / ancien `.doc` (invitation à enregistrer en docx)
- **Masquage + restauration (bidirectionnel)** :
  - Les documents structurés (tableaux, Word, PPT, documents dans un ZIP) prennent en charge le masquage réversible (tokenisation / AES / mélange / arrondi numérique) et une restauration cohérente.
  - **PDF / images proposent deux modes** :
    - « Masquage par recouvrement (irréversible) » — recouvre directement les pixels/vecteurs de la page par des blocs noirs, conformément à la nature physique du PDF/de l'image.
    - « Conversion en Word puis masquage (réversible) » — extrait d'abord le texte et les champs de formulaire via le moteur PDF local / l'OCR, tokenise automatiquement, puis génère un `.docx` minimal. Les jetons entrent dans le dictionnaire global et **le texte d'origine peut être restauré à partir du dictionnaire**.
- **13 catégories de données sensibles** : nom, organisation, pièce d'identité, code de crédit, mobile, téléphone fixe, carte bancaire, e-mail, montant, date, adresse, URL, numéro de document.
- **Multiples méthodes** : tokenisation / masquage / hachage / généralisation / chiffrement AES-GCM / mélange aléatoire / arrondi numérique (réversible avec colonne de reste chiffrée) / suppression de colonne
- **Dictionnaire global (même valeur, même code)** : un même texte en clair correspond à un même jeton across fichiers et colonnes, garantissant la cohérence des associations et une restauration exacte ; prend en charge **l'export protégé par phrase secrète (fichier de dictionnaire chiffré par AES)**.
- **Entièrement hors ligne** : le moteur de texte PDF (pdf.js) et l'OCR d'images (tesseract.js + wasm local + packs de langues chinois/anglais) sont tous embarqués dans `libs/`, avec repli CDN intégré — **fonctionne même sans réseau**.
- **Traitement par lots** : glisser-déposer de dossiers (avec parcours récursif) et de plusieurs fichiers, masquage en masse selon la stratégie par défaut, barre de progression et journal en temps réel, résultats regroupés en ZIP.

## Formats pris en charge et réversibilité

| Format | Masquage | Restauration |
|--------|----------|--------------|
| CSV / Excel (y compris .xls) | Oui | Oui |
| Word / PowerPoint (y compris champs de formulaire PDF) | Oui | Oui |
| ZIP (imbriqué) | Oui | Oui (récursif) |
| PDF / images · recouvrement | Oui | Non (irréversible) |
| PDF / images · mode conversion Word | Oui | Oui (via dictionnaire global) |

> Remarque : le mode « conversion en Word » des PDF/images perd la mise en page d'origine (seuls le texte/champs extraits et les jetons sont conservés) mais permet de restaurer intégralement le texte d'origine. Le recouvrement préserve la mise en page et est irréversible. Basculez entre les deux modes via le menu déroulant de la carte d'import du document.

## Structure du répertoire

```
Outil de masquage universel/
├─ InfoCloak_V2.html        # Programme principal (double-clic pour ouvrir avec Chrome/Edge)
├─ README.md                # Ce fichier (racine)
├─ libs/                    # Dépendances localisées (permettent le fonctionnement hors ligne)
│  ├─ xlsx.full.min.js      # Lecture/écriture de tableurs (y compris ancien .xls)
│  ├─ jszip.min.js          # Lecture/écriture ZIP
│  ├─ pdf-lib.min.js        # Redessin et recouvrement PDF
│  ├─ pdfjs/                # pdf.js local (extraction de texte PDF)
│  │  ├─ pdf.min.js
│  │  └─ pdf.worker.min.js
│  └─ tesseract/            # tesseract.js local (OCR d'images)
│     ├─ tesseract.min.js
│     ├─ worker.min.js
│     ├─ tesseract-core.wasm.js   # Noyau autonome (wasm intégré, utilisable hors ligne)
│     └─ tessdata/          # Packs de langues OCR (chinois chi_sim / anglais eng)
│        ├─ chi_sim.traineddata.gz
│        └─ eng.traineddata.gz
├─ files/                   # Documents hors ligne (mode sombre synchronisé avec l'interface)
│  ├─ User_Guide.html
│  └─ Tech_Docs.html
└─ elders/                  # Versions historiques (V1, etc.)
```

## Démarrage rapide

1. Ouvrez `InfoCloak_V2.html` avec Chrome / Edge (double-clic).
2. Choisissez une fonction dans le menu de gauche : ① Masquage de tableaux ② Masquage de documents ③ Restauration ④ Dictionnaire global.
3. Importez un fichier → choisissez la méthode (pour PDF/images, basculez « Recouvrement / Conversion Word » dans la carte document) → générez → téléchargez le résultat masqué.
4. **Traitement par lots** : déposez un dossier entier dans la zone « Traitement par lots » ou sélectionnez un dossier. Le masquage démarre selon la stratégie par défaut, les résultats sont regroupés en ZIP et la progression est affichée en temps réel.
5. Pour restaurer, allez dans ③ Restauration, importez le fichier masqué + le dictionnaire maître (les dictionnaires chiffrés nécessitent d'abord la phrase secrète).

## Dictionnaire global et protection par phrase secrète

- Le dictionnaire global garantit « même valeur, même code » across fichiers/colonnes et constitue l'unique base de restauration.
- Lors de l'export, vous pouvez définir une **phrase secrète** : le dictionnaire est chiffré en AES-GCM (dérivation de clé PBKDF2, 150000 itérations) et enregistré sous forme de paquet `.json` contenant `salt`/`iv`/`ct`.
- L'import d'un dictionnaire chiffré requiert la phrase secrète correcte ; celle-ci n'est jamais écrite dans le fichier de dictionnaire et sert uniquement à dériver la clé de la session en cours.
- **Le dictionnaire maître contient tous les mappages en clair et constitue l'actif le plus sensible — conservez-le localement et ne le diffusez jamais avec les fichiers masqués.**

## Réversibilité des méthodes de masquage

| Méthode | Réversible | Nécessite |
|---------|-----------|-----------|
| Tokenisation | Oui | Dictionnaire maître |
| Chiffrement AES | Oui | Dictionnaire maître + phrase secrète |
| Mélange aléatoire | Oui | Dictionnaire maître (mappage par valeur) |
| Arrondi numérique réversible | Oui | Dictionnaire maître + phrase secrète |
| Masquage / Hachage / Généralisation / Suppression / Recouvrement | Non | — |

## ⚠️ Règles de téléchargement du dictionnaire (à lire absolument)

**Le dictionnaire n'est PAS enregistré automatiquement !** Après le masquage, il ne subsiste que dans la mémoire du navigateur et est perdu à la fermeture de la page. Vous devez le télécharger manuellement depuis ④ Dictionnaire global.

| Méthode utilisée pour le masquage | Élément à télécharger depuis ④ |
|---|---|
| Tokenisation / mélange uniquement | **Télécharger `主字典.json` (dictionnaire maître)** (en clair) |
| Chiffrement AES / arrondi numérique réversible | **Télécharger `加密主字典.json` (dictionnaire maître chiffré)** + saisir une phrase secrète |
| Masquage / Hachage / Généralisation / Suppression | Inutile (irréversible, restauration impossible) |

**Correspondance à la restauration** : fichier `主字典.json` téléchargé → importez-le et laissez la phrase secrète vide ; fichier `主字典_加密.json` téléchargé → importez-le et saisissez la phrase secrète définie à l'origine.

## Confidentialité et sécurité

- Les données ne quittent jamais votre machine ; aucun envoi réseau (fonctionne entièrement hors ligne une fois `libs/` localisé).
- La phrase secrète ne sert qu'à dériver la clé de la session et n'est jamais écrite dans le fichier de dictionnaire.
- **Le dictionnaire maître contient tous les mappages en clair et constitue l'actif le plus sensible — conservez-le localement et ne le diffusez jamais avec les fichiers masqués.**
- Cet outil est fourni à des fins d'organisation d'informations et d'apprentissage ; il ne garantit pas une sécurité absolue des données. Pensez à sauvegarder vos fichiers source.

## Limites connues

- Le mode « conversion en Word » des PDF/images repose sur l'extraction de texte ; la qualité du masquage des scans dépend de la précision de l'OCR. Les mises en page complexes sont simplifiées en texte brut.
- L'ancien format `.doc` ne peut pas être analysé directement — enregistrez-le d'abord en `.docx` dans Word/WPS.
- Le recouvrement des PDF/images est irréversible ; vérifiez que vous n'avez pas besoin de restauration avant de l'utiliser.

## Licence

[MIT](https://opensource.org/licenses/MIT) — utilisation, modification et redistribution libres ; veuillez conserver les informations de l'auteur d'origine.

**Auteur d'origine** : SuperLaos ｜ **Compte officiel WeChat** : 技术宅SuperLaos
