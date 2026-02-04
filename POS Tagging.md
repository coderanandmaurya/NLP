# Part-of-Speech (POS) Tagging
---

## Summary: Part-of-Speech (POS) Tagging using Hidden Markov Models

This lecture explains **Part-of-Speech (POS) Tagging**, a fundamental **Natural Language Processing (NLP)** preprocessing technique, and demonstrates its implementation using **Hidden Markov Models (HMM)** optimized with the **Viterbi algorithm**. Both theoretical foundations and practical tools (SpaCy) are covered.

---

## 1. Part-of-Speech (POS) Tagging

**POS Tagging** is the task of assigning grammatical labels (noun, verb, adjective, etc.) to words in a sentence based on **context**, not just dictionary meaning.

**Example:**

> *“I will Google campus”*

* I → Pronoun
* will → Verb
* Google → Verb/Noun (context-dependent)
* campus → Noun

This contextual dependency makes POS tagging a **sequence prediction problem**.

---

## 2. Importance and Applications of POS Tagging

POS tagging is a **core preprocessing step** in NLP pipelines and supports:

* **Named Entity Recognition (NER)** (person, location, date, organization)
* **Word Sense Disambiguation**
* **Question Answering Systems**
* **Chatbots and Voice Assistants**
* **Information Retrieval**
* **Text Parsing and Syntax Analysis**

Without POS tagging, higher-level NLP tasks become unreliable.

---

## 3. Practical POS Tagging using SpaCy

The lecture demonstrates POS tagging using the **SpaCy** Python library.

### Key Features of SpaCy POS Tagging:

* Tokenization and POS tagging in a single pipeline
* Two tag levels:

  * **Coarse-grained POS tags** (NOUN, VERB, ADJ)
  * **Fine-grained POS tags** (VBG, VBD, NNS, etc.)
* Easy iteration over tokens to inspect:

  * POS tag
  * Detailed tag
  * Tag explanations
* Visualization support for syntactic structure

SpaCy enables **fast prototyping** without manually implementing tagging algorithms.

---

## 4. POS Tagging as a Sequence Labeling Problem

POS tagging is modeled as a **sequence labeling task**, where:

* Input: Sequence of words
* Output: Sequence of POS tags

The goal is to find the **most probable tag sequence** for a given sentence.

---

## 5. Hidden Markov Model (HMM) for POS Tagging

An **HMM** is used where:

* **Observed states:** Words in the sentence
* **Hidden states:** POS tags

### Two Core Probabilities:

| Probability Type       | Description      | Example            |
| ---------------------- | ---------------- | ------------------ |
| Emission Probability   | P(word | tag)    | P("Google" | NOUN) |
| Transition Probability | P(tagᵢ | tagᵢ₋₁) | P(VERB | NOUN)     |

### Model Requirements:

* Labeled training dataset
* Frequency counts of:

  * Word–tag pairs
  * Tag-to-tag transitions
* Conversion of frequencies into probabilities

---

## 6. Manual Dataset Preparation

To explain the algorithm clearly, the lecturer:

* Manually tags a small dataset
* Computes:

  * Emission probabilities
  * Transition probabilities
* Builds lookup tables for efficient access

This step clarifies how statistical POS taggers work internally.

---

## 7. Viterbi Algorithm for Optimization

Brute-force evaluation of all possible tag sequences is computationally infeasible.

The **Viterbi algorithm**:

* Uses **dynamic programming**
* Stores only the most probable path to each tag at each step
* Eliminates low-probability paths early (pruning)
* Ensures optimal tagging efficiently

### Viterbi Steps:

1. Initialization (start probabilities)
2. Recursion (transition + emission probabilities)
3. Termination (select max probability)
4. Backtracking (retrieve best tag sequence)

---

## 8. Key Insights

* POS tagging is **foundational to NLP**
* HMM provides a clear probabilistic framework
* Computational complexity grows rapidly without optimization
* Viterbi algorithm makes large-scale POS tagging feasible
* SpaCy abstracts complexity while retaining accuracy
* Understanding HMM-based tagging improves model interpretability

---
## 9. Keywords

* POS Tagging
* Natural Language Processing
* Hidden Markov Model
* Viterbi Algorithm
* Emission Probability
* Transition Probability
* Sequence Labeling
* SpaCy
* Named Entity Recognition

---

## Conclusion

This lecture delivers a **complete conceptual and practical understanding of POS tagging**, bridging theory (HMM + Viterbi) with practice (SpaCy). It equips learners to both **use existing NLP tools** and **build custom POS taggers**, making it highly valuable for students and practitioners in NLP and machine learning.

---
