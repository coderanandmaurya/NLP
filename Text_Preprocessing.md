# Text Preprocessing for Natural Language Processing (NLP)

### Lecture Notes with Examples and Practical Implementation

## 1. Introduction

Text preprocessing is one of the **most critical stages** in the NLP pipeline. It lies **after data acquisition** and **before feature engineering**. The quality of preprocessing directly impacts model accuracy, robustness, and scalability.

Real-world text data is **messy, noisy, and inconsistent**. It may contain:

* HTML tags
* URLs
* Emojis
* Slang and abbreviations
* Spelling errors

This lecture focuses on **basic and essential preprocessing techniques** required for machine learning–based NLP tasks. Advanced linguistic tasks such as **POS tagging and coreference resolution** are intentionally excluded and addressed separately.

---

## 2. Role of Text Preprocessing in NLP Pipeline

### NLP Pipeline Context

```
Data Acquisition → Text Preprocessing → Feature Engineering → Modeling → Deployment
```

📌 **Key Objective:**
Transform raw human language into **clean, consistent, and machine-friendly text**, without losing meaningful information.

---

## 3. Core Preprocessing Steps (with Examples)

---

## 3.1 Lowercasing Text

### Why Lowercasing Is Needed

Computers treat words with different cases as different tokens.

📌 **Example:**

```
"Hello", "hello", "HELLO"
```

Without lowercasing → treated as 3 different words
With lowercasing → all become:

```
"hello"
```

### Python Example

```python
text = "I Love NLP"
text.lower()
```

📌 **Result:**

```
"i love nlp"
```

Lowercasing reduces vocabulary size and improves model efficiency.

---

## 3.2 Removing HTML Tags

### Problem

Web-scraped text often contains HTML formatting that carries **no linguistic meaning**.

📌 **Example:**

```
"<p>This movie is <b>amazing</b></p>"
```

### After HTML Removal:

```
"This movie is amazing"
```

### Technique Used

* **Regular Expressions (Regex)** using Python’s `re` module.

📌 **Important Insight:**
Regex is a **fundamental skill** for NLP preprocessing due to its flexibility in pattern matching.

---

## 3.3 Removing URLs

### Why Remove URLs?

URLs rarely contribute to sentiment or classification tasks.

📌 **Example:**

```
"Check this out https://example.com"
```

After removal:

```
"Check this out"
```

Regex patterns are commonly used to identify and remove URLs efficiently.

---

## 3.4 Removing Punctuation

### Purpose

Punctuation often creates **irrelevant tokens**.

📌 **Example:**

```
"Wow!!! Amazing product!!!"
```

After punctuation removal:

```
"Wow Amazing product"
```

---

### Methods Compared

#### 1. Manual Replacement (Slow)

Looping and replacing punctuation one by one.

#### 2. `str.translate()` (Fast – Recommended)

Uses `string.punctuation` and translation tables.

📌 **Performance Insight:**
`str.translate()` is ~3× faster and suitable for **large datasets**.

---

## 3.5 Expanding Contractions and Chat Abbreviations

### Why This Matters

Social media and chat data contain many abbreviations.

📌 **Examples:**

| Abbreviation | Expanded Form        |
| ------------ | -------------------- |
| IMHO         | in my honest opinion |
| BTW          | by the way           |
| LOL          | laughing out loud    |

📌 **Before Expansion:**

```
"IMHO this movie is great"
```

📌 **After Expansion:**

```
"in my honest opinion this movie is great"
```

Expansion improves semantic clarity for models.

---

## 3.6 Spell Correction

### Problem

Typos introduce unnecessary noise.

📌 **Example:**

```
"Ths product is amazng"
```

After correction:

```
"This product is amazing"
```

### Tools

* TextBlob
* pyspellchecker

📌 **Important Note:**
Domain-specific terms (medical, regional words) may require **custom spell checkers**.

---

## 3.7 Stopword Removal

### What Are Stopwords?

Common words that appear frequently but add little meaning.

📌 **Examples:**
is, the, and, of, to

📌 **Example:**

```
"I am learning NLP"
```

After stopword removal:

```
["learning", "NLP"]
```

### Tools

* NLTK stopword list (customizable)

⚠️ **Caution:**
Stopwords should **not** always be removed (e.g., POS tagging, syntax analysis).

---

## 3.8 Handling Emojis

### Importance of Emojis

Emojis convey emotion but are difficult for models to interpret.

📌 **Example:**

```
"I love this phone 😍"
```

### Two Strategies

1. **Remove Emojis**

```
"I love this phone"
```

2. **Replace with Meaning**

```
"I love this phone smile"
```

Emoji replacement preserves sentiment information.

---

## 3.9 Tokenization and Text Segmentation

### Definition

Tokenization splits text into **smaller units**.

---

### Word Tokenization Example

```
"I love NLP"
```

→

```
["I", "love", "NLP"]
```

---

### Sentence Tokenization Challenge

```
"Dr. Smith is here. He teaches NLP."
```

Simple splitting fails due to abbreviations.

📌 **Libraries Used:**

* NLTK
* spaCy

These libraries handle edge cases more accurately.

---

## 4. Advanced Text Normalization

---

## 4.1 Inflection in Language

Words appear in multiple forms:

| Base | Variants               |
| ---- | ---------------------- |
| walk | walks, walking, walked |

---

## 4.2 Stemming

### Definition

Reduces words to their stem.

📌 **Example:**

| Word    | Stem  |
| ------- | ----- |
| walking | walk  |
| studies | studi |

⚠️ Output may **not be a real word**.

---

## 4.3 Lemmatization

### Definition

Reduces words to **dictionary form (lemma)**.

📌 **Example:**

| Word    | Lemma |
| ------- | ----- |
| walking | walk  |
| better  | good  |

---

### Stemming vs Lemmatization

| Aspect   | Stemming       | Lemmatization |
| -------- | -------------- | ------------- |
| Speed    | Fast           | Slower        |
| Accuracy | Lower          | Higher        |
| Output   | May be invalid | Valid word    |

📌 **Choice depends on:**

* Task type
* Output readability requirement

---

## 5. Practical Assignment Explained

### Task

Create a **multi-class text classification dataset**.

---

### Example Use Case: Movie Genre Classification

1. Fetch top-rated movie data via APIs
2. Extract descriptions + genres
3. Apply preprocessing:

   * Lowercasing
   * HTML removal
   * URL removal
   * Punctuation removal
   * Spell correction
   * Stopword removal
   * Emoji handling
   * Tokenization

📌 This reinforces **end-to-end preprocessing skills**.

---

## 6. Summary Table: Text Preprocessing Techniques

| Step                   | Purpose             | Tools             | Notes              |
| ---------------------- | ------------------- | ----------------- | ------------------ |
| Lowercasing            | Normalize case      | `str.lower()`     | Reduces vocabulary |
| HTML Removal           | Clean web data      | Regex             | Removes tags       |
| URL Removal            | Remove noise        | Regex             | Improves focus     |
| Punctuation Removal    | Reduce noise        | `str.translate()` | Fast               |
| Abbreviation Expansion | Normalize chat text | Dictionary        | Social data        |
| Spell Correction       | Fix typos           | TextBlob          | Improves accuracy  |
| Stopword Removal       | Remove filler       | NLTK              | Task-dependent     |
| Emoji Handling         | Manage sentiment    | Regex/emoji libs  | Optional           |
| Tokenization           | Text segmentation   | NLTK/spaCy        | Word/sentence      |
| Stemming/Lemmatization | Normalize forms     | Porter, WordNet   | Speed vs quality   |

---

## 7. Key Insights

* Text preprocessing is **task-specific**
* Regex is a **core NLP skill**
* Efficient coding matters for large datasets
* Informal text needs special handling
* Tokenization and normalization strongly affect model performance
* Stemming and lemmatization serve different purposes
* NLP libraries simplify reliable preprocessing

---

## 8. Conclusion

This lecture establishes a **strong foundation in text preprocessing**, bridging raw data and effective modeling. Proper preprocessing leads to:

* Better features
* Faster training
* Higher accuracy

The assignment ensures hands-on mastery of preprocessing workflows. Future lectures will expand into **advanced linguistic NLP techniques**.

---

### Final Takeaway

> **Clean data is not optional in NLP — it is the model’s foundation.**

---
