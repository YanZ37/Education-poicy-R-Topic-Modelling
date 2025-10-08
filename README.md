# Education-poicy-R-Topic-Modelling
# Structural Topic Modeling (STM) for Text-Coding: PRC TVET Assessment Policies

> A machine-learning workflow that applies **Structural Topic Modeling (STM)** to analyze assessment policy documents in China's **technical and vocational education and training (TVET)** context.

---

## Overview

Manual text coding is labor-intensive. This project demonstrates how **STM** can serve as a scalable alternative by modeling topics that vary with document-level metadata (e.g., discipline). We show end-to-end preprocessing, model search, quality evaluation, interpretation, and validation on a corpus of **166 policy documents**. Key takeaway: **formative goals were often secondary to summative ones in the analyzed policies.**

---

## Key Features

- **Method:** Structural Topic Modeling (extension of LDA) with covariates for **topic prevalence** and **topic content**.  
- **Quality Indices:** Held-out likelihood, residuals, lower bound, **semantic coherence**, and **exclusivity** to select K and assess model fit.  
- **Corpus:** 166 TVET policy documents (translated and quality-checked), producing 1,075 text units across **Computer Science, Mechanical & Electrical Engineering, Food Science, Health Science**.  
- **Result Highlights:** An optimal model in the **10–15 topics** range; final selection **K = 15** based on the coherence–exclusivity trade-off and qualitative review.

---

## Data & Preparation

- **Source:** Talent Development Plans (TDP) and sections focusing on **Course Standards** and **Implementation Guarantees**.  
- **Translation QA:** Human bilingual review on a 4-point functional equivalence scale (overall *close to very close*).  
- **Preprocessing:** Tokenization, lowercasing, stop-word removal (incl. **451 custom stop words**), and pruning of infrequent terms (`lower.thresh = 5`).

---

## Modeling Approach

1. **Bag-of-Words**: documents → document–term matrix for STM.  
2. **Model Search**: evaluate K = 5…20 using held-out likelihood, residuals, lower bound, and semantic coherence; shortlist **K = 10–15**.  
3. **Final Selection**: choose **K = 15** on the **coherence–exclusivity frontier**, confirmed via reading representative documents.  
4. **Interpretation**: use **high-probability** and **FREX** words; inspect **MAP** histograms and exemplar documents to label topics.  
5. **Validation**: semantic validity checked via multi-rater agreement (**Cohen’s κ ≈ .92 mean**).

---

## Results (Examples)

- Frequent themes include **Coursework & Final Exams**, **Online/Offline Assessments**, **Experiments**, **Simulations**, **Project Design**, and **Self/Peer Assessments**.  
- **Discipline differences** observed in topic prevalence and content (e.g., Health Science emphasizing online/offline assessments; Food Science emphasizing experiments).  
- **Formative assessment** appears widely referenced yet often contributes to **summative grading**, potentially diluting formative intent.

---

## How to Run

1. **Install R packages**: `stm`, `stminsights`, `dplyr`, `ggplot2` (see `DESCRIPTION` if you add one).  
2. **Preprocess:** run `01_preprocess.R` to create `documents`, `vocab`, `meta`.  
3. **Model Search:** run `02_model_search.R` to evaluate K and pick candidates.  
4. **Fit Selected Model:** run `03_fit_selected.R` (e.g., **K = 15**), then `save.image("stm.RData")`.  
5. **Explore Interactively:** `run_stminsights()` and select `stm.RData`.  
6. **Effects & Content:** use `estimateEffect` and `plot(type="perspectives")` for discipline differences.

---

## Interpretation Notes

- **Coherence vs. Exclusivity**: select K by balancing interpretability (co-occurring top words) and distinctiveness (less cross-topic overlap).  
- **Topic Naming**: combine **FREX** words with exemplar documents for reliable labels.  
- **Caveat**: STM uses **Bag-of-Words**, so word order/grammar are not modeled; use qualitative checks to confirm interpretations.

---

## Ethical & Methodological Considerations

- **Privacy & Licensing**: ensure rights to distribute texts or provide redacted references.  
- **Translation QA**: document translation procedure and reliability checks if using non-English sources.  
- **Bias Review**: inspect stop-word lists and labeling decisions to avoid inadvertent bias.

---


## Appendix

- **Custom Stop-Words**: curated list (~451) to remove high-frequency but uninformative terms.  
- **Exemplery documents**: exemplery policies for each topic with topic words highlighted.
