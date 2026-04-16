# Assignment 4: Named Entity Recognition (NER)
### BSAN 6200 — Text Mining & Social Media Analytics
**Loyola Marymount University | Spring 2026**
**Instructor:** Dr. Ace Vo

---

## Dataset
**[Broad Twitter Corpus](https://huggingface.co/datasets/GateNLP/broad_twitter_corpus)** — GateNLP/broad_twitter_corpus

| Split | Raw | After Filtering |
|-------|-----|-----------------|
| Train | 5,342 | 4,836 |
| Test | 2,002 | 1,688 |
| **Total** | **7,344** | **6,524** |

> Non-English tweets and emoji-heavy posts were removed using unicode filtering.

**Entity Types:** `PER` · `LOC` · `ORG` · `PROD`

---

## Notebooks

| Notebook | Description |
|----------|-------------|
| `assignment4_ner_checkpoint.ipynb` | Checkpoint 1 — data loading, filtering, pretrained baseline, IAA |
| `assignment4_ner_training_full.ipynb` | Full pipeline — model training, evaluation, error analysis, cross-domain inference |

---

## Pipeline

Dataset → Language/Emoji Filtering → Pretrained NER Baseline → Annotation Guidelines (v1.0 → v1.1) → Manual Annotation (Label Studio) → IAA Calculation → Model 1 (CRF) → Model 2 (Fine-tuned Transformer) → Evaluation & Comparison → Cross-Domain Inference

**Annotation Batches:**
- Batch 1: 10 docs — both annotators independently
- Batch 2: 100 docs each + 20 overlap for IAA
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

## Team
**Aziza Jamjoom** · **Sadaf Sarbazi**
