## 1. Introduction – Why Do We Need Self-Attention?

**Self-Attention**

To understand why self-attention was invented, we must understand the **evolution of text representation in NLP**.

Computers cannot understand text directly.

They only process **numbers**.

Therefore, the first step in any NLP system is:

**Convert words into numbers.**

This process is called **Word Vectorization**.

---

# 2. Word Vectorization

Word vectorization converts text into **numerical vectors**.

Example sentence:

```text
I love machine learning
```

A computer must convert this into numeric representation before processing.

---

# 3. One-Hot Encoding

![Image](https://www.researchgate.net/profile/Mohammad-Reza-Faisal/publication/301703031/figure/fig2/AS%3A669970149158914%401536744739074/Example-of-text-representation-by-one-hot-vector.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/0%2A4QWLdmNkB87GPi_S)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1200/1%2AGsKLFAlzoNeIKo-1gz1h_Q.png)

![Image](https://s-ai-f.github.io/Natural-Language-Processing/images/one-hot.png)

One of the earliest techniques used in NLP is **One-Hot Encoding**.

Example vocabulary:

| Word     | Vector    |
| -------- | --------- |
| I        | [1,0,0,0] |
| Love     | [0,1,0,0] |
| Machine  | [0,0,1,0] |
| Learning | [0,0,0,1] |

Each word is represented by a vector containing:

* one **1**
* remaining **0s**

Example sentence representation:

```text
I love AI
```

Vectors:

```
I → [1,0,0]
Love → [0,1,0]
AI → [0,0,1]
```

### Problems of One-Hot Encoding

1. Very **sparse vectors**
2. Vocabulary becomes **huge**
3. No **semantic meaning**

Example:

```
King → [0,0,0,1]
Queen → [0,1,0,0]
```

Even though the meanings are similar, vectors have **no relationship**.

---

# 4. Bag of Words (BoW)

![Image](https://miro.medium.com/1%2AaxffCQ9ae0FHXxhuy66FbA.png)

![Image](https://miro.medium.com/1%2A3K9GIOVLNu0cRvQap_KaRg.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2Av7bM3U4nNc3xStnA_i2ZrQ.png)

![Image](https://www.analyticssteps.com/backend/media/uploads/2019/09/06/image-20190906164045-2.jpeg)

Bag of Words improves representation slightly.

Instead of individual vectors, we count **word frequency**.

Example sentence:

```
I love AI and I love data
```

Vocabulary:

| Word | Count |
| ---- | ----- |
| I    | 2     |
| love | 2     |
| AI   | 1     |
| data | 1     |

Vector representation:

```
[2,2,1,1]
```

### Problem of Bag of Words

1. **Word order ignored**

Example:

```
Dog bites man
Man bites dog
```

Both produce the same representation.

2. **Context is lost**

---

# 5. TF-IDF (Term Frequency – Inverse Document Frequency)

![Image](https://www.researchgate.net/publication/344335518/figure/fig1/AS%3A938415151394817%401600747015701/TF-IDF-vectorization-process.ppm)

![Image](https://www.researchgate.net/publication/376247075/figure/fig2/AS%3A11431281209841725%401701888441866/TF-IDFTerm-Frequency-Inverse-Document-Frequency.ppm)

![Image](https://assets.zilliz.com/TF_IDF_table_62a64f4dc1.png)

![Image](https://mallahyari.github.io/ml_tutorial/images/tfidf_ex3.png)

TF-IDF improves Bag of Words by weighting words based on importance.

Formula:

[
TF-IDF = TF \times IDF
]

Where:

TF = Term Frequency
IDF = Inverse Document Frequency

Example:

Common words like:

```
the
is
and
```

receive **low importance**.

Rare but meaningful words receive **higher weight**.

### Problem with TF-IDF

Still has major limitations:

1. No **semantic understanding**
2. Cannot capture **relationships between words**
3. No **context awareness**

---

# 6. Word Embeddings

![Image](https://www.researchgate.net/publication/332679657/figure/fig1/AS%3A809485488640000%401570007788866/The-classical-king-woman-man-queen-example-of-neural-word-embeddings-in-2D-It.png)

![Image](https://serokell.io/files/6f/6fq4jm7j.pic1_Word2Vec.png)

![Image](https://miro.medium.com/1%2AiV-kVEuRcz_Qpl2AJxiKMA.jpeg)

![Image](https://corpling.hypotheses.org/files/2018/04/Screen-Shot-2018-04-25-at-13.21.44.png)

A major breakthrough came with **Word Embeddings**.

Instead of sparse vectors, words are represented by **dense vectors**.

Example:

```
King → [0.25, -0.13, 0.88, ...]
Queen → [0.24, -0.11, 0.91, ...]
```

Typical dimensions:

* 100
* 256
* 512
* 768

### Key Idea

Words with **similar meaning appear close in vector space**.

Example relationships:

```
King − Man + Woman ≈ Queen
```

Embedding models:

| Model    | Description                 |
| -------- | --------------------------- |
| Word2Vec | Predict surrounding words   |
| GloVe    | Global co-occurrence matrix |
| FastText | Uses character subwords     |

---

# 7. How Embeddings Capture Meaning

Each dimension represents **latent features**.

Example (conceptual):

| Dimension | Meaning    |
| --------- | ---------- |
| 1         | Royalty    |
| 2         | Gender     |
| 3         | Age        |
| 4         | Profession |

Example vectors:

| Word  | Royalty | Gender | Human |
| ----- | ------- | ------ | ----- |
| King  | High    | Male   | Yes   |
| Queen | High    | Female | Yes   |
| Apple | None    | None   | No    |

Note:

These features are **not explicitly labeled**.

They are learned automatically by the model.

---

# 8. Problem with Static Embeddings

![Image](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9b/Word%2C_object%2C_and_thought.svg/512px-Word%2C_object%2C_and_thought.svg.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1200/1%2A4sgOrpS1aPpAN01xAk68Ag.png)

![Image](https://devimages-cdn.apple.com/wwdc-services/images/48/2614/2614_wide_250x141_2x.jpg)

![Image](https://ik.imagekit.io/upgrad1/abroad-images/imageCompo/images/__visual_selection_22_0LZD1K.png)

Traditional embeddings are **static**.

This means each word has **one fixed vector**.

Example word:

```
Apple
```

Two meanings:

1. Fruit
2. Technology company

Example sentences:

```
Apple is my favorite fruit
Apple launched a new iPhone
```

Static embeddings produce **the same vector for both cases**.

This creates confusion.

---

# 9. Need for Contextual Embeddings

Real language understanding requires **context awareness**.

Example sentence:

```
Apple launched a new phone while I was eating an orange
```

Here:

```
Apple → company
orange → fruit
```

A model must distinguish meanings based on **context**.

This is where **Self-Attention** becomes important.

---

# 10. Self-Attention Concept

![Image](https://miro.medium.com/v2/resize%3Afit%3A1200/1%2AZPePnPodMZeehez9YFmr9A.png)

![Image](https://raw.githubusercontent.com/jessevig/bertviz/master/images/head-view.gif)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AGd6nqg1uHAHw3Fcz2ilLtQ.gif)

![Image](https://www.researchgate.net/publication/338426630/figure/fig2/AS%3A872348379017217%401584995469709/Self-attention-based-context-aware-word-embedding-S-sentence-end-symbol_Q320.jpg)

Self-Attention solves the context problem.

Idea:

Each word **looks at every other word in the sentence**.

Example sentence:

```
The animal didn't cross the street because it was tired
```

Question:

What does **"it"** refer to?

Self-attention learns:

```
it → animal
```

---

# 11. What Self-Attention Does

Self-attention takes **word embeddings** as input.

Then it produces **new contextual embeddings**.

Process:

```
Static Embedding
      ↓
Self Attention
      ↓
Contextual Embedding
```

Example:

Word:

```
Apple
```

Output embeddings:

| Context     | Embedding Meaning |
| ----------- | ----------------- |
| Apple fruit | Fruit embedding   |
| Apple phone | Company embedding |

---

# 12. Simple Intuition

Think of self-attention as a **smart calculator**.

It examines:

```
All words in the sentence
```

Then determines:

```
Which words are important for each word
```

Example sentence:

```
I love deep learning because it is powerful
```

Self-attention connects:

```
it → deep learning
```

---

# 13. Key Takeaways

Important points from this lecture:

1. Computers cannot process text directly.
2. Words must be converted into **vectors**.
3. Early techniques include:

   * One-Hot Encoding
   * Bag of Words
   * TF-IDF
4. Word embeddings introduced **semantic understanding**.
5. Static embeddings fail for **multiple meanings**.
6. Self-attention produces **contextual embeddings**.

---

# 14. What Comes Next

This lecture explains **why self-attention is needed**.

The next lecture explains:

### How Self-Attention Works Internally

Topics include:

* Query vectors
* Key vectors
* Value vectors
* Attention score
* Attention matrix
* Multi-Head Attention

---

# Final Summary

Self-attention is one of the most important innovations in modern AI.

It allows models to:

* understand **context**
* resolve **word ambiguity**
* create **dynamic word representations**

This concept is the **foundation of Transformers and Large Language Models**.

Without self-attention, modern systems like:

* ChatGPT
* GPT models
* BERT
* Translation systems

would not exist.

---
