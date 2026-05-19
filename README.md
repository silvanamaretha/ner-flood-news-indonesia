# Named Entity Recognition on Indonesian Flood News (2023)

Silvana's old project (2024)

---

## Overview

This project applies Named Entity Recognition (NER) to extract structured information from 250 Indonesian flood news articles published in 2023. Rather than relying solely on a pre-trained model, this project uses a hybrid approach: combining IndoBERT for general entity recognition with a custom rule-based extractor for flood-specific entities that general models do not cover.

---

## Approach

### IndoBERT NER

Uses `cahya/bert-base-indonesian-NER`, a BERT-based model pre-trained on Indonesian text, to identify general entities:

| Entity  | Description          | Example                      |
| ------- | -------------------- | ---------------------------- |
| GPE     | Geo-political entity | Jakarta Selatan, DKI Jakarta |
| LOC     | Location             | Jalan Jembatan Otista        |
| DAT     | Date                 | 31 Desember 2023             |
| TIM     | Time                 | 19.00 WIB                    |
| PER     | Person               | Bima Arya                    |
| NOR/ORG | Organization         | BPBD DKI Jakarta             |

### Rule-Based Extraction (Flood-Specific)

Custom regex and keyword-based extractor for entities unique to flood reporting:

| Entity       | Description             | Example                         |
| ------------ | ----------------------- | ------------------------------- |
| TINGGI_AIR   | Water level measurement | 60 cm, 1.5 meter                |
| JENIS_BANJIR | Flood type              | banjir bandang, banjir rob      |
| KORBAN       | Casualties              | 1 orang meninggal               |
| PENYEBAB     | Flood cause             | luapan kali, curah hujan tinggi |

---

## Dataset

- Source: Online news portals (Detik.com, Kompas, Tribun News, CNN Indonesia, Liputan6)
- Collection method: Manual collection + web scraping (BeautifulSoup)
- Total articles: 250
- Period: January - December 2023
- Keyword: "Banjir 2023"

---

## Key Findings

| Metric                    | Value          |
| ------------------------- | -------------- |
| Total entities extracted  | 3,924          |
| Most mentioned location   | Jakarta        |
| Most common flood cause   | Hujan Deras    |
| Most common flood type    | Banjir Bandang |
| Peak month for flood news | Desember       |

Insight: Flood reporting peaks in November–December, consistent with Indonesia's rainy season. The dominant cause identified across articles is heavy rainfall, while Jakarta and surrounding areas are the most frequently reported locations.

---

## Limitations

- Max token limit:IndoBERT processes only the first 512 characters per article, potentially missing entities in longer texts
- Rule-based sensitivity: TINGGI_AIR may extract non-flood measurements (e.g., road lengths in meters)
- No gold standard evaluation: qualitative spot-check was used instead of formal precision/recall against annotated data
- Single year coverage: data limited to 2023; trends may differ across years

---

## How to Run

Developed using Google Colab. To reproduce:

1. Upload `Banjir_ALL.xlsx` to Colab
2. Run `NER_BERITA_BANJIR_INDONESIA_2023.ipynb` sequentially

Note: IndoBERT model download (~443MB) requires internet connection and may take a few minutes.

---

## Tech Stack

Python · Pandas · HuggingFace Transformers · Regex · Matplotlib · Seaborn · Collections
