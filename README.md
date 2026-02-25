# Text Summarization using Transformers (T5 & BART)

This project focuses on building a robust text summarization system using state-of-the-art Transformer models. It covers both **Abstractive** and **Extractive** summarization techniques, with a custom ensemble approach designed to overcome performance plateaus.

## 📌 Project Overview
The goal is to generate concise summaries from long news articles using the **CNN/DailyMail** dataset. The project includes:
* Fine-tuning a **T5-base** model for abstractive summarization.
* Implementing an **Ensemble Heuristic** combining T5 and BART.
* Applying **Extractive Summarization** using Gensim's TextRank (Bonus Task).
* Evaluating performance using **ROUGE** scores (1, 2, and L).

## 🛠️ Technical Implementation

### 1. Abstractive Summarization (Fine-tuned T5)
* **Model:** `t5-base`.
* **Dataset:** CNN/DailyMail (3.0.0).
* **Training:** Fine-tuned on a subset of 2000 samples for 3 epochs with a learning rate of 3e-4.
* **Performance Observation:** During experimentation, the ROUGE score consistently plateaued around 37. This suggested that the model had reached its optimal capacity for this specific configuration.

### 2. Ensemble PoC (T5 & BART)
* **Motivation:** To address the ROUGE plateau, an ensemble approach was proposed to combine the strengths of T5 and BART.
* **Implementation Status:** The logic was implemented and validated as a **Proof of Concept (PoC) on a single news article**.
* **Selection Heuristic:** The ensemble adopts a length-based heuristic, choosing the longer summary to maximize semantic density and ROUGE overlap.

### 3. Extractive Summarization (Gensim)
* Implemented TextRank-based extraction to provide a comprehensive comparison between neural abstractive summaries and traditional extractive methods (Bonus requirement).

## 📊 Discussion & Analysis

### The "ROUGE vs. Quality" Trade-off
During the development, a key observation was made regarding model output length:
* **Length vs. Score:** Increasing the maximum output length for a single model might artificially boost ROUGE scores by covering more n-grams.
* **The Hallucination Risk:** However, forcing longer outputs often leads to **model hallucinations**, factual inconsistencies, or redundant phrases.
* **The Ensemble Solution:** Instead of pushing a single model to its limits, the **Ensemble approach** was chosen to prioritize coherence.

### ⚠️ Execution Constraints (RAM Limitations)
**Unfortunately, due to severe hardware memory (RAM) constraints in the environment, it was not possible to execute the ensemble logic on the entire dataset.** Loading multiple large transformer models (T5-base and BART-large) simultaneously exceeded the available memory limits. Consequently, the ensemble remains a functional Proof of Concept (PoC) to demonstrate the proposed logic while staying within resource boundaries.

