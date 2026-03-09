# Lecture 3 – How Self-Attention Works (Query, Key, Value)

## 1. Introduction

![Image](https://www.researchgate.net/publication/391696986/figure/fig4/AS%3A11431281435777087%401747128418823/Diagram-of-the-query-key-value-and-self-attention-mechanism-The-input-vectors-x-is.ppm)

![Image](https://poloclub.github.io/transformer-explainer/article_assets/attention.png)

![Image](https://cdn-images-1.medium.com/max/2268/1%2A6BEwO4jKy9UC7AzU6nIPPg.png)

![Image](https://media.licdn.com/dms/image/v2/D5612AQFCvbvofKlIlw/article-cover_image-shrink_720_1280/B56ZeSu2YiHoAI-/0/1750513447876?e=2147483647\&t=kqNdYRAIRAa00EQhPgUagiNG2RrsjtPk55QsX-ta9V0\&v=beta)

In the previous lecture we learned:

* Why **self-attention** is needed.
* How it solves the problem of **static word embeddings**.

In this lecture we answer the most important question:

**How does self-attention actually work mathematically?**

Self-attention converts **static embeddings → contextual embeddings** using three vectors:

* **Query (Q)**
* **Key (K)**
* **Value (V)**

These vectors allow each word to **measure its relationship with other words**.

---

# 2. Static vs Contextual Embeddings

Before understanding the mechanism, recall the main problem.

### Static Embeddings

Each word has **one fixed vector**.

Example word:

```
bank
```

Two meanings:

| Sentence                      | Meaning               |
| ----------------------------- | --------------------- |
| I deposited money in the bank | financial institution |
| He sat on the river bank      | river side            |

Static embeddings give the **same vector** for both cases.

---

### Contextual Embeddings

Transformers solve this using **self-attention**.

Example:

Sentence 1

```
I deposited money in the bank
```

Sentence 2

```
The boat reached the river bank
```

Self-attention produces **different embeddings for “bank”** depending on context.

---

# 3. High-Level Idea of Self-Attention

![Image](https://www.researchgate.net/publication/372624535/figure/fig2/AS%3A11431281199403398%401697593740084/The-role-of-self-attention-for-the-example-sentence-Extreme-brightness-of-the-sun-hurts.png)

![Image](https://www.researchgate.net/publication/381876634/figure/fig3/AS%3A11431281257726642%401719862085707/The-heatmap-visualizing-the-attention-scores-of-a-Transformer-model-across-various.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1200/1%2AZPePnPodMZeehez9YFmr9A.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A21312/1%2AR5rsOaTdYLHIJX_fJiqgPw.png)

Self-attention allows **each word to examine every other word** in the sentence.

Example sentence:

```
The animal didn't cross the street because it was tired
```

The word:

```
it
```

must determine its reference.

Self-attention learns:

```
it → animal
```

The model assigns **higher importance (attention weight)** to relevant words.

---

# 4. Step 1 – Input Word Embeddings

Suppose we have a sentence:

```
I love deep learning
```

Each word is converted into an embedding vector.

Example:

| Word     | Embedding (Example) |
| -------- | ------------------- |
| I        | [0.2, 0.5, 0.1]     |
| love     | [0.9, 0.3, 0.4]     |
| deep     | [0.7, 0.8, 0.2]     |
| learning | [0.6, 0.9, 0.3]     |

These embeddings are stored in a matrix:

[
X
]

This is the **input embedding matrix**.

---

# 5. Step 2 – Creating Query, Key, Value

![Image](https://cdn-images-1.medium.com/max/2268/1%2A6BEwO4jKy9UC7AzU6nIPPg.png)

![Image](https://cdn-images-1.medium.com/max/2000/1%2AsQP6cxjpXZ_lxDFYYe9Vdw.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A640/format%3Awebp/1%2AgUxLBgWIh5btuQUIuZIr6g.png)

![Image](https://cdn-images-1.medium.com/max/2000/1%2AmoKYjUdtx-uEyYMbhPWbIw.png)

Each embedding is transformed into **three different vectors**:

* Query (Q)
* Key (K)
* Value (V)

This is done using **learnable weight matrices**:

[
W^Q, W^K, W^V
]

Formulas:

[
Q = XW^Q
]

[
K = XW^K
]

[
V = XW^V
]

These matrices are **learned during training** using **backpropagation**.

---

# 6. Role of Query, Key, Value

Understanding the roles of Q, K, V is crucial.

| Vector | Role                                   |
| ------ | -------------------------------------- |
| Query  | What this word is searching for        |
| Key    | What information this word contains    |
| Value  | The actual information to pass forward |

---

### Intuition

Think of **Google search**.

| Concept          | Self-Attention |
| ---------------- | -------------- |
| Search query     | Query vector   |
| Webpage keywords | Key vectors    |
| Webpage content  | Value vectors  |

The search engine compares **query with keywords** and returns relevant information.

Self-attention works in a similar way.

---

# 7. Step 3 – Compute Attention Scores

![Image](https://www.3blue1brown.com/content/lessons/2024/attention/LinearMap.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A2000/0%2AO6ZGTu_iwE10IhQ7.png)

![Image](https://www.researchgate.net/publication/381876634/figure/fig3/AS%3A11431281257726642%401719862085707/The-heatmap-visualizing-the-attention-scores-of-a-Transformer-model-across-various.png)

![Image](https://www.researchgate.net/publication/338137956/figure/fig3/AS%3A839480810418176%401577159230054/Heatmap-of-Self-Attention-scores-using-Transformer-Encoder-In-this-work-we-employ-n-1.ppm)

Next, we compute **similarity between words**.

Formula:

[
Score = QK^T
]

Explanation:

* Each **query** compares with all **keys**.
* This produces an **attention score matrix**.

Example:

|      | I   | love | deep | learning |
| ---- | --- | ---- | ---- | -------- |
| I    | 1.2 | 0.5  | 0.4  | 0.3      |
| love | 0.7 | 1.5  | 0.8  | 0.9      |

Higher score = stronger relationship.

---

# 8. Step 4 – Scaling and Softmax

Large values in the score matrix can create unstable gradients.

Therefore scores are scaled:

[
Score = \frac{QK^T}{\sqrt{d_k}}
]

Where:

```
d_k = dimension of key vector
```

Next we apply **Softmax**.

Softmax converts scores into **probabilities**.

Example:

| Word     | Attention Weight |
| -------- | ---------------- |
| I        | 0.1              |
| love     | 0.4              |
| deep     | 0.3              |
| learning | 0.2              |

All weights sum to:

```
1
```

---

# 9. Step 5 – Weighted Sum of Values

![Image](https://substackcdn.com/image/fetch/%24s_%21jtT-%21%2Cf_auto%2Cq_auto%3Agood%2Cfl_progressive%3Asteep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff4d7dc94-6f18-4973-a501-de1d5b101c10_1903x856.png)

![Image](https://jalammar.github.io/images/t/transformer_resideual_layer_norm_2.png)

![Image](https://erdem.pl/static/d0e833aab2689ef7be2fed2deaa0c538/cnn-second-timestep.png)

![Image](https://www.researchgate.net/publication/389942224/figure/fig4/AS%3A11431281317054075%401742317369766/Visualization-of-the-channel-attention-mechanism-for-extracting-meaningful-spectral.png)

Final contextual embedding is computed using:

[
Output = AttentionWeights \times V
]

This means:

Each word's representation becomes a **weighted combination of other words**.

Example:

Word:

```
learning
```

Context vector may become:

```
0.1*I + 0.4*love + 0.3*deep + 0.2*learning
```

This creates a **context-aware representation**.

---

# 10. Complete Self-Attention Formula

The full equation used in transformers is:

[
Attention(Q,K,V) =
softmax\left(\frac{QK^T}{\sqrt{d_k}}\right)V
]

This is called **Scaled Dot Product Attention**.

---

# 11. Matrix Computation Advantage

Transformers compute attention using **matrix operations**.

Benefits:

| Advantage            | Explanation                        |
| -------------------- | ---------------------------------- |
| Parallel computation | All words processed simultaneously |
| GPU acceleration     | Matrix operations optimized        |
| Faster training      | Much faster than RNN               |

This is why transformers scale to **billions of parameters**.

---

# 12. Limitation of Basic Self-Attention

Early simplified self-attention produced **general contextual embeddings**.

However real NLP tasks need:

* **task-specific embeddings**

Examples:

| Task               | Required Focus       |
| ------------------ | -------------------- |
| Translation        | grammar + alignment  |
| Sentiment analysis | emotional words      |
| Question answering | entity relationships |

To achieve this, models learn **trainable parameters**.

---

# 13. Learnable Parameters

The matrices:

```
WQ
WK
WV
```

are **trainable parameters**.

They are updated using:

```
Backpropagation
Gradient Descent
```

During training, the model learns:

* which words matter
* how much attention to assign
* how to represent context

---

# 14. Real-World Analogy (Matchmaking Website)

Example analogy from the lecture.

| Concept            | Matchmaking System | Self-Attention |
| ------------------ | ------------------ | -------------- |
| Profile            | User profile       | Word embedding |
| Search preference  | Query              | Query vector   |
| Candidate profiles | Keys               | Key vectors    |
| Recommended match  | Result             | Value vectors  |

Matching happens by comparing **query with keys**.

---

# 15. Self-Attention Pipeline (Step Summary)

Complete process:

```
Sentence
 ↓
Word Embeddings
 ↓
Generate Q, K, V
 ↓
Compute QK^T similarity
 ↓
Scale and apply softmax
 ↓
Weighted sum of V
 ↓
Contextual Embeddings
```

---

# 16. Why Self-Attention is Powerful

Self-attention solves many NLP problems:

| Problem               | Solution                |
| --------------------- | ----------------------- |
| Long dependency       | Global attention        |
| Parallel training     | Matrix computation      |
| Context understanding | Contextual embeddings   |
| Word ambiguity        | Dynamic representations |

---

# 17. Key Takeaways

Important points:

1. Self-attention converts **static embeddings → contextual embeddings**.
2. Each word creates **Query, Key, Value vectors**.
3. Similarity is computed using **dot product**.
4. Softmax produces **attention weights**.
5. Weighted sum of values generates **final contextual representation**.

---

# 18. Final Conclusion

Self-attention is the **core mathematical engine of transformers**.

It enables models to:

* understand context
* model relationships between words
* process sequences efficiently

The entire generative AI revolution including:

* GPT models
* BERT
* ChatGPT
* translation systems

is built on this mechanism.

---
