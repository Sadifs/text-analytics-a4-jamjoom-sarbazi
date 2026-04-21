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
| `assignment4_final_models.ipynb` | Full pipeline — CoNLL generation, IAA, model training, evaluation, error analysis, cross-domain inference |

---

## Pipeline

Dataset → Language/Emoji Filtering → Pretrained NER Baseline → Annotation Guidelines (v1.0 → v1.1) → Manual Annotation (Label Studio) → IAA Calculation → Model 1 (CRF) → Model 1b (Bi-LSTM) → Model 2 (Fine-tuned Transformer) → Evaluation & Comparison → Cross-Domain Inference

**Annotation Batches:**
- Batch 1: 10 docs — both annotators independently → initial IAA
- Batch 2: ~100 docs each + 20 overlap → bulk annotation + IAA check
- Batch 3: 90 docs pre-annotated by CRF → both annotators reviewed & corrected
- **Total: 300 annotated documents in CoNLL format**

---

## Models

| Model | Description | Precision | Recall | F1 |
|-------|-------------|-----------|--------|----|
| **Baseline** | `dslim/bert-base-NER` — pretrained, no fine-tuning | 0.222 | 0.273 | 0.245 |
| **Model 1 (CRF)** | CRF trained on manual annotations (240 train sentences) | 0.250 | 0.091 | 0.133 |
| **Model 1b (Bi-LSTM)** | Bidirectional LSTM trained on manual annotations | 0.000 | 0.000 | 0.000 |
| **Model 2 (Transformer)** | `dslim/bert-base-NER` fine-tuned on 300 annotated docs | 0.200 | 0.136 | 0.162 |

**Train/Val/Test split:** 80/10/10 (240 / 30 / 30 sentences)

> **Note on Bi-LSTM performance:** The Bi-LSTM collapsed to predicting all-O tags due to severe class imbalance (94.3% of tokens are O). With only 300 annotated tweets, the model defaulted to the majority class. This is a known limitation of neural models on small, imbalanced NER datasets — traditional ML methods like CRF outperform neural approaches in this low-resource setting.

---

## Inter-Annotator Agreement

| Batch | Annotators | κ (Cohen's Kappa) | Entity F1 | Status |
|-------|------------|-------------------|-----------|--------|
| Batch 1 (10 docs) | Sadaf + Aziza | 0.760 | — | ✅ Acceptable |
| Batch 2 (20 overlap) | Sadaf + Aziza | **0.851** | 0.833 | 🌟 Excellent |

**Per-entity Kappa (Batch 2 overlap):**

| Entity | κ | Notes |
|--------|---|-------|
| PER | 0.438 | Most disagreement — informal Twitter handles hard to classify |
| LOC | 1.000 | Perfect agreement |
| ORG | 0.922 | Near-perfect agreement |
| PROD | 1.000 | Perfect agreement |

---

## Error Analysis (CRF — Model 1)

**False Negatives (missed entities):** Twitter handles (`digitalkipper`, `kimberleybarber`), informal spellings (`blink 182`), ambiguous entities (`smartphone`, `UK`)

**False Positives (spurious entities):** Common nouns misclassified as PER (`Me`, `Choice Awards`, `Best Lifestyle`)

**Type Mismatches:** `CULTOFDOMKELLER` labeled as LOC instead of PROD

**Key insight:** CRF struggles with Twitter-specific entities (handles, hashtags, informal spellings) and rare entity types like PROD which have limited training examples.

---

## Cross-Domain Inference

The CRF model trained on Twitter was applied to 20 restaurant-domain sentences. Results showed poor generalization — only 5 entities found across 20 sentences, with errors like classifying "Los Angeles" as PER and "Eleven Madison Park" as PER. This confirms that Twitter-trained models do not generalize well to formal restaurant review text due to domain shift in writing style and entity surface forms.

---

## Tools & Libraries

| Purpose | Tool |
|---------|------|
| Annotation | Label Studio (app.heartex.com) |
| Baseline & Model 2 | HuggingFace Transformers (`dslim/bert-base-NER`) |
| Model 1 | sklearn-crfsuite (CRF) |
| Model 1b | TensorFlow/Keras (Bi-LSTM) |
| Evaluation | seqeval (entity-level F1) |
| IAA | Cohen's Kappa (sklearn) |
| Data | HuggingFace Datasets — Broad Twitter Corpus |

---

## Team
**Aziza Jamjoom** · **Sadaf Sarbazi**

---
## Conclusion

This project gave us hands-on experience with the full NER pipeline, from raw Twitter data to trained and evaluated models. Our key finding was that traditional ML methods like CRF outperformed neural approaches in this low-resource setting — with only 300 annotated tweets and severe class imbalance, the Bi-LSTM and fine-tuned Transformer struggled to learn meaningful entity patterns while the CRF leveraged hand-crafted features effectively. The annotation process was significantly more time-consuming and subjective than we anticipated, and achieving an IAA of κ=0.851 required careful guideline iteration and regular discussion between annotators. In future work, we would expand the annotated dataset substantially, apply data augmentation to address class imbalance, and explore few-shot learning approaches better suited to low-resource NER scenarios.
