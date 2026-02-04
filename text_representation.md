# 📘 Text Representation Techniques in Machine Learning

*(From Absolute Basics to TF-IDF)*

---

## 1️⃣ First Principle: What Does a Machine Learning Model Understand?

A machine learning model **does not understand language**.

It only understands **numbers** and performs mathematical operations such as:

[
y = wx + b
]

So when we give text like:

> **“I love machine learning”**

the model **cannot process it directly**.

📌 Therefore, **text must be converted into numbers**.

This conversion process is called:

* **Text Representation**
* **Text Vectorization**
* **Feature Extraction from Text**

---

## 2️⃣ What Is a Feature? (Text Perspective)

In tabular data:

* Columns = **features**
* Rows = **data points**

Example:

| Hours Studied | Marks |
| ------------- | ----- |
| 6             | 70    |

Here, *Hours Studied* is a feature.

---

### ❓ In Text Data, What Is the Feature?

Sentence:

```
"I love ML"
```

Words:

```
I, love, ML
```

📌 These words must become **numeric features**.

---

## 3️⃣ Tokenization and Vocabulary (Foundation Step)

### 🔹 Tokenization

Breaking text into words.

```
"I love ML" → ["I", "love", "ML"]
```

Each word is called a **token**.

---

### 🔹 Vocabulary

The set of **unique tokens** in the dataset.

Dataset:

```
"I love ML"
"I love AI"
```

Vocabulary:

```
["I", "love", "ML", "AI"]
```

📌 Vocabulary size decides **vector dimension**.

---

## 4️⃣ Why Fixed-Length Vectors Are Required?

Machine learning models:

* Expect the **same number of inputs**
* Cannot handle variable-length text

Example:

```
"I love ML" → 3 words
"I really love ML" → 4 words
```

❌ Not acceptable

➡️ Text representation converts all sentences into **fixed-length numeric vectors**.

---

## 5️⃣ Challenges in Text Representation

* Large vocabulary → high dimensional vectors
* **Sparsity** (too many zeros)
* **Out-of-Vocabulary (OOV)** words
* No semantic understanding
* Loss of word order

📌 *Garbage In → Garbage Out* applies strongly here.

---

## 6️⃣ One-Hot Encoding

### 📌 Concept

Each word is represented by a vector with:

* One `1`
* Remaining `0`s

Vocabulary:

```
["I", "love", "ML"]
```

| Word | Vector    |
| ---- | --------- |
| I    | [1, 0, 0] |
| love | [0, 1, 0] |
| ML   | [0, 0, 1] |

### ❌ Limitations

* Very high dimensional
* Sparse vectors
* No meaning or similarity
* Not scalable

---

## 7️⃣ Bag of Words (BoW)

### 📌 Concept

* Count word frequency
* Ignore word order

Example sentences:

```
S1: I love ML
S2: I love AI
```

Vocabulary:

```
["I", "love", "ML", "AI"]
```

| Sentence | Vector       |
| -------- | ------------ |
| S1       | [1, 1, 1, 0] |
| S2       | [1, 1, 0, 1] |

### ✅ Advantages

* Simple
* Fixed-size vectors
* Effective for basic classification

### ❌ Limitations

```
"dog bites man"
"man bites dog"
```

➡️ Same vector, different meaning

---

## 8️⃣ Bag of N-Grams

### 📌 Motivation

To capture **partial word order**.

Example:

```
"not good"
```

Bigrams preserve negation better than unigrams.

### ❌ Drawback

* Vocabulary size increases rapidly
* Higher memory and computation

---

## 9️⃣ TF-IDF (Term Frequency – Inverse Document Frequency)

### 📌 Problem with BoW

Common words like:

```
is, the, and
```

appear everywhere and add noise.

---

### 🔢 Term Frequency (TF)

[
TF = \frac{\text{Word count in document}}{\text{Total words in document}}
]

---

### 🔢 Inverse Document Frequency (IDF)

[
IDF = \log\left(\frac{\text{Total documents}}{\text{Documents containing the word}}\right) + 1
]

---

### 🔢 TF-IDF Score

[
TF\text{-}IDF = TF \times IDF
]

📌 Important words receive **higher weight**.

---

### Example Insight

Documents:

```
D1: ML is powerful
D2: ML is fun
```

| Word | TF-IDF Weight |
| ---- | ------------- |
| ML   | High          |
| is   | Low           |

---

## 🔟 Out-of-Vocabulary (OOV) Problem

Training text:

```
"movie is good"
```

Test text:

```
"movie is excellent"
```

📌 **excellent** not in vocabulary → ignored

---

## 1️⃣1️⃣ Custom / Handcrafted Features

Examples:

* Positive word count
* Negative word count
* Sentence length
* Presence of words like *not*

Hybrid features often improve performance.

---

## 1️⃣2️⃣ Technique Comparison

| Technique | Word Order | Semantics  | Sparsity  |
| --------- | ---------- | ---------- | --------- |
| One-Hot   | ❌          | ❌          | High      |
| BoW       | ❌          | ❌          | High      |
| N-Grams   | ⚠️ Partial | ⚠️ Partial | Very High |
| TF-IDF    | ❌          | ⚠️ Partial | High      |

---

## 1️⃣3️⃣ Why We Learn These Techniques

* Foundation of NLP
* Easy to interpret
* Fast on small datasets
* Common in interviews
* Basis for Word2Vec & BERT

---

## 🔚 Conclusion

Text representation is a **critical step** in any NLP pipeline.
Classical methods like **One-Hot, BoW, N-Grams, and TF-IDF** convert text into numbers but fail to fully capture meaning.

These techniques form the **bridge** to advanced embedding methods, which will be covered next.
