# 📘 Word2Vec and Word Embedding Techniques

*(From Why We Need Embeddings to Practical Usage)*

---

## 1️⃣ Why Do We Need Word Embeddings? (Bridge from TF-IDF)

### ❌ Problem with Previous Techniques

From the previous lecture:

* One-Hot, BoW, TF-IDF
* High-dimensional
* Sparse vectors
* No true semantic meaning

Example:

```
good → [0,1,0,0,0]
excellent → [0,0,0,1,0]
```

📌 Machine thinks **good ≠ excellent**

---

### ❓ What Humans Expect

Humans know:

```
good ≈ excellent ≈ awesome
```

➡️ **Words with similar meaning should have similar numeric representations**

This is where **Word Embeddings** come in.

---

## 2️⃣ What Is a Word Embedding? (Very Basic)

### 📌 Definition

A **word embedding** is a way of representing words as **dense numeric vectors** such that:

* Similar words → similar vectors
* Related words → close in vector space

Example intuition:

```
king  → [0.21, -0.34, 0.56, ...]
queen → [0.19, -0.30, 0.58, ...]
```

📌 These are **real numbers**, not 0/1.

---

## 3️⃣ Sparse vs Dense Vectors (Critical Basic)

### ❌ Sparse Vector (BoW / TF-IDF)

Vocabulary size = 50,000
Sentence length = 10

Vector:

```
[0,0,0,1,0,0,0,0,0,0,...]
```

Problems:

* Memory waste
* Slower computation
* Curse of dimensionality

---

### ✅ Dense Vector (Word2Vec)

Vector size = 100 or 300

```
[0.21, -0.34, 0.56, 0.89, ...]
```

Benefits:

* Compact
* Meaningful
* Efficient

---

## 4️⃣ What Is Word2Vec?

### 📌 Definition

**Word2Vec** is a **prediction-based word embedding technique** developed by Google (2013–2015) that uses **neural networks** to learn semantic word representations.

📌 It improves over:

* BoW
* TF-IDF

By:

* Learning meaning from **context**
* Producing **dense embeddings**

---

## 5️⃣ Two Types of Word Representation (Big Picture)

| Category         | Idea          | Examples     |
| ---------------- | ------------- | ------------ |
| Frequency-based  | Count words   | BoW, TF-IDF  |
| Prediction-based | Predict words | **Word2Vec** |

📌 Word2Vec learns by **prediction, not counting**.

---

## 6️⃣ Core Idea Behind Word2Vec (Intuition)

> **Words appearing in similar contexts have similar meanings**

Example:

```
I drink coffee
I drink tea
```

📌 coffee and tea appear in **same context**
➡️ Their vectors become similar

---

## 7️⃣ Context Window (Very Basic)

Sentence:

```
I love machine learning very much
```

If window size = 2

For word **machine**, context words:

```
love, learning
```

📌 Word2Vec slides this window across text to learn relationships.

---

## 8️⃣ Word2Vec Architectures

### 1️⃣ CBOW (Continuous Bag of Words)

📌 Predict **target word** from **context words**

Example:

```
Context: I love ___ learning
Target: machine
```

Characteristics:

* Faster
* Works well on large datasets
* Less accurate for rare words

---

### 2️⃣ Skip-Gram

📌 Predict **context words** from **target word**

Example:

```
Target: machine
Predict: love, learning
```

Characteristics:

* Slower
* Better for small datasets
* Better for rare words

---

## 9️⃣ Neural Network View (Simple)

Word2Vec uses a **shallow neural network**:

* Input layer → word index
* Hidden layer → embedding (actual word vector)
* Output layer → predicted word(s)

📌 The **hidden layer weights = word embeddings**

---

## 🔟 Why Word2Vec Is Powerful

### ✅ Semantic Similarity

```
happy ≈ joy
king ≈ queen
```

### ✅ Vector Arithmetic

[
king - man + woman \approx queen
]

This shows **semantic understanding**, not memorization.

---

### ✅ Dense & Efficient

* Fewer dimensions (100–300)
* Faster training
* Less overfitting

---

## 1️⃣1️⃣ Training Word2Vec (High-Level Workflow)

| Step                 | Description            |
| -------------------- | ---------------------- |
| Data Collection      | Large corpus           |
| Preprocessing        | Tokenization, cleaning |
| Vocabulary           | Unique words           |
| Windowing            | Define context         |
| Model Training       | Neural prediction      |
| Embedding Extraction | Vectors                |
| Evaluation           | Similarity & analogy   |

---

## 1️⃣2️⃣ Practical Demonstration (Conceptual)

Using **Gensim**:

* Load pre-trained Google News vectors
* Each word → 300-D vector
* Compute similarity:

```
similarity("man", "woman")
similarity("king", "queen")
```

📌 Vectors are **dense and meaningful**

---

## 1️⃣3️⃣ Domain Example: Game of Thrones

* Train Word2Vec on GoT scripts
* Character names become embeddings
* Similarity examples:

```
Jon Snow ↔ Night Watch
Daenerys ↔ Dragon
```

📌 Model learns **domain-specific meaning**

---

## 1️⃣4️⃣ Improving Word2Vec Models

| Factor             | Effect                  |
| ------------------ | ----------------------- |
| More data          | Better embeddings       |
| Larger vector size | More meaning, more cost |
| Larger window      | Broader context         |
| Bigger vocabulary  | Better coverage         |

---

## 1️⃣5️⃣ Limitations of Word2Vec (Important)

* Same word → same vector in all contexts

  ```
  bank (river) = bank (money) ❌
  ```
* Requires large data
* Not contextual

📌 This leads to **GloVe, FastText, BERT**

---

## 🔚 Final Takeaway

* Word2Vec converts words into **dense semantic vectors**
* Learns meaning from **context**
* Solves major problems of BoW & TF-IDF
* Foundation of **modern NLP**

---
Just tell me what to do next.
