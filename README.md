# Assignment 4: Named Entity Recognition (NER)
### BSAN 6200 — Text Mining & Social Media Analytics
**Loyola Marymount University | Spring 2026**
**Instructor:** Dr. Ace Vo

---

## Team
**Aziza Jamjoom**
**Sadaf Sarbazi**

---

## Dataset
**Broad Twitter Corpus** — [GateNLP/broad_twitter_corpus](https://huggingface.co/datasets/GateNLP/broad_twitter_corpus)

| Split | Documents |
|-------|-----------|
| Train | 5,342 |
| Test | 2,002 |
| **Total** | **7,344** |

**Entity Types:** `PER` · `LOC` · `ORG` · `PROD`

---

## Pipeline

```
Dataset → Pretrained NER → Annotation Guidelines → Manual Annotation
→ IAA Calculation → Custom Model Training → Fine-tuning → Evaluation
```

---

## Models

| Model | Description |
|-------|-------------|
| **Baseline** | `dslim/bert-base-NER` — pretrained on CoNLL-2003 |
| **Model 1** | Custom trained on manual annotations |
| **Model 2** | Fine-tuned on expanded + corrected annotations |

---

## 🛠️ Tools
- **Annotation:** Label Studio
- **Models:** HuggingFace Transformers
- **Evaluation:** seqeval (entity-level F1)
- **IAA:** Cohen's Kappa (sklearn)
