---

## Models

| Model | Description | F1 |
|-------|-------------|-----|
| **Baseline** | `dslim/bert-base-NER` — pretrained on CoNLL-2003, no fine-tuning | TBD |
| **Model 1** | CRF trained on manual annotations | TBD |
| **Model 2** | `dslim/bert-base-NER` fine-tuned on expanded annotations | TBD |

---

## Inter-Annotator Agreement

| Batch | Annotators | κ (Cohen's Kappa) | Status |
|-------|------------|-------------------|--------|
| Batch 1 (10 docs) | Sadaf + Aziza | 0.760 | Acceptable |
| Batch 2 (20 overlap) | Sadaf + Aziza | TBD | — |

---

## Tools & Libraries

| Purpose | Tool |
|---------|------|
| Annotation | Label Studio |
| Baseline & Model 2 | HuggingFace Transformers (`dslim/bert-base-NER`) |
| Model 1 | sklearn-crfsuite (CRF) |
| Evaluation | seqeval (entity-level F1) |
| IAA | Cohen's Kappa (sklearn) |
| Data | HuggingFace Datasets — Broad Twitter Corpus |

---

## Results

*(To be updated after model training)*

| Model | Precision | Recall | F1 |
|-------|-----------|--------|----|
| Baseline | — | — | — |
| Model 1 (CRF) | — | — | — |
| Model 2 (Transformer) | — | — | — |

---

## Note

- Checkpoint 1 (Apr 12) — Dataset, pretrained model, guidelines v1.0, Batch 1 IAA
- Final submission — All batches annotated, models trained, report complete

---

## Team
**Aziza Jamjoom** · **Sadaf Sarbazi**
