# Text Classification in Machine Learning

## 1. Introduction

Text classification is one of the **most fundamental and widely used tasks** in Natural Language Processing (NLP). It enables machines to **automatically assign categories to text** such as emails, reviews, articles, or messages.

This lecture focuses specifically on **machine learning–based text classification**. Deep learning approaches (RNN, LSTM, Transformers) are acknowledged but intentionally postponed to a later session so that learners can first build a **strong conceptual foundation using ML**.

---

## 2. What Is Text Classification?

### Definition

**Text Classification** is a **supervised machine learning problem** where:

* **Input** → Text (word, sentence, paragraph, or document)
* **Output** → One or more predefined class labels

📌 **Example:**

```
Text: "This movie was fantastic!"
Output: Positive
```

---

## 3. Types of Text Classification

### 3.1 Binary Classification

Two possible classes.

📌 **Examples:**

* Spam / Not Spam
* Positive / Negative
* Fake / Real

---

### 3.2 Multi-Class Classification

More than two classes.

📌 **Example: News Categorization**

| Text                              | Category |
| --------------------------------- | -------- |
| "India wins cricket match"        | Sports   |
| "Stock market crashes"            | Business |
| "New government policy announced" | Politics |

---

### 3.3 Multi-Label Classification

Multiple labels can be assigned simultaneously.

📌 **Example:**

```
Article: "Cricket world cup final highlights"
Labels: [Sports, Cricket]
```

---

## 4. Real-World Applications of Text Classification

### Common Industry Use Cases

* **Email Spam Filtering**
* **Customer Support Ticket Routing**
* **Sentiment Analysis**
* **Language Detection**
* **Fake News Detection**
* **Content Moderation**

📌 **Example (Customer Support):**

```
"I want to cancel my order"
→ Routed to: Support Team
```

---

## 5. Text Classification Pipeline (End-to-End)

Text classification follows a structured pipeline:

| Stage              | Description             |
| ------------------ | ----------------------- |
| Data Acquisition   | Collect labeled text    |
| Data Cleaning      | Remove noise            |
| Text Preprocessing | Normalize text          |
| Feature Extraction | Convert text to numbers |
| Modeling           | Train ML model          |
| Evaluation         | Measure performance     |
| Deployment         | Use model in real-world |

📌 **Key Insight:**
Skipping any step weakens the final system.

---

## 6. Machine Learning Approach to Text Classification

This lecture emphasizes **machine learning models**, which are:

* Easier to interpret
* Faster to train
* Suitable for small-to-medium datasets

---

## 7. Data Acquisition Example

### IMDB Movie Reviews Dataset

* 50,000 labeled reviews
* Binary sentiment: Positive / Negative
* Balanced dataset

📌 **Sample Data:**

| Review              | Sentiment |
| ------------------- | --------- |
| "Amazing movie!"    | Positive  |
| "Worst acting ever" | Negative  |

---

## 8. Data Cleaning and Preprocessing

### Common Steps

* Remove duplicates
* Convert text to lowercase
* Remove punctuation
* Remove stopwords
* Tokenization
* Stemming or lemmatization

📌 **Before Cleaning:**

```
"This movie!!! was AMAZING 😍"
```

📌 **After Cleaning:**

```
"movie amazing"
```

---

## 9. Feature Extraction (Most Important Step)

ML models **cannot understand text directly**.

📌 **Text:**

```
"I love this movie"
```

📌 **Converted to numbers:**

```
[0.4, 0.7, 0.9]
```

---

### Common Feature Extraction Methods

#### 9.1 Bag of Words (BoW)

Counts word frequency.

📌 **Example Vocabulary:**

```
["good", "bad", "movie"]
```

📌 **Sentence:**
"good movie"

📌 **Vector:**

```
[1, 0, 1]
```

---

#### 9.2 n-grams

Captures word sequences.

📌 **Example:**

* Unigram: good
* Bigram: good movie

---

#### 9.3 TF-IDF

Measures word importance.

* Penalizes common words
* Highlights informative words

---

## 10. Machine Learning Algorithms Used

### 10.1 Naive Bayes

* Simple
* Fast
* Strong baseline

📌 Works well for text due to word independence assumption.

---

### 10.2 Random Forest

* Ensemble of decision trees
* Handles non-linearity
* Better accuracy than Naive Bayes in many cases

📌 **Example Performance:**
~84.8% accuracy on IMDB dataset

---

### 10.3 Support Vector Machine (SVM)

* Effective for high-dimensional text data
* Works well with TF-IDF features

---

## 11. Model Evaluation Metrics

Evaluation ensures model reliability.

| Metric           | Meaning                       |
| ---------------- | ----------------------------- |
| Accuracy         | Overall correctness           |
| Precision        | Correct positive predictions  |
| Recall           | Coverage of actual positives  |
| F1-Score         | Balance of precision & recall |
| Confusion Matrix | Error breakdown               |

📌 **Example:**
Spam detection must prioritize **precision** to avoid misclassifying real emails.

---

## 12. Deep Learning (Preview Only)

Deep learning models include:

* RNN
* LSTM
* CNN
* Transformers (BERT)

📌 **Instructor Advice:**
Start with ML first, then move to DL.

DL requires:

* More data
* More compute
* More tuning

---

## 13. Practical Advice from the Lecture

* Always check **class balance**
* Combine handcrafted + automated features
* Tune hyperparameters
* Solve multiple small projects
* Do not blindly use deep learning
* Use rule-based methods only as last resort
* Use cloud APIs for fast prototyping (with cost awareness)

---

## 14. Using Third-Party NLP APIs

Examples:

* Google Cloud NLP
* AWS Comprehend

📌 **Pros:**

* Fast
* No training needed

📌 **Cons:**

* Cost
* Limited customization

---

## 15. Quantitative Performance Comparison

| Algorithm     | Observations                 |
| ------------- | ---------------------------- |
| Naive Bayes   | Good baseline                |
| Random Forest | Better accuracy (~84.8%)     |
| Deep Learning | Potentially best, but costly |

---

## 16. Key Takeaways

* Text classification is a **core NLP task**
* ML models are ideal starting point
* Feature extraction is critical
* Pipeline thinking is essential
* Deep learning is powerful but optional initially
* Practical projects build mastery

---

## 17. Final Conclusion

Text classification combines **language understanding and statistical learning**. This lecture emphasizes mastering:

* Data
* Features
* Models
* Evaluation

before moving to complex architectures.

### Final Message

> **Strong fundamentals in machine learning lead to better deep learning later.**

---
