# Lecture: Vector Indexing and Nearest Neighbor Search

### 1. Motivation

Modern **Generative AI and semantic search systems** work with **embeddings**.
Embeddings convert text into **numerical vectors in high-dimensional space**.

Example:

| Text           | Vector (simplified) |
| -------------- | ------------------- |
| "apple fruit"  | [0.21, 0.44, 0.66]  |
| "banana fruit" | [0.20, 0.41, 0.63]  |
| "iphone phone" | [0.90, 0.10, 0.32]  |

If two vectors are **close in vector space**, their meanings are similar.

But when we have **millions of vectors**, comparing a query vector with every vector becomes **slow**.

To solve this problem we use:

* **Vector Indexing**
* **Nearest Neighbor Search**

---

# 2. What is Vector Indexing?

Vector indexing is a **data structure used to store embeddings efficiently so that similarity search becomes fast.**

Instead of scanning all vectors one by one, the index **organizes vectors in a way that similar vectors are grouped together.**

### Without Index

Dataset size = 1 million vectors

Search process:

```
Query Vector
     ↓
Compare with Vector 1
Compare with Vector 2
Compare with Vector 3
...
Compare with Vector 1,000,000
```

Time complexity:

```
O(N)
```

Very slow.

---

### With Vector Index

Vectors are organized into **clusters or tree structures**.

Search process:

```
Query Vector
     ↓
Find relevant cluster
     ↓
Search only nearby vectors
```

Now the system searches **a small subset** instead of the whole dataset.

This makes retrieval **much faster**.

---

# 3. What is Nearest Neighbor Search?

Nearest Neighbor Search finds the **most similar vectors to a query vector**.

Goal:

```
Given a query vector → find closest vectors
```

Closeness can be measured using:

* Cosine similarity
* Euclidean distance
* Dot product

---

### Mathematical Idea

If we have:

```
Query vector = Q
Dataset vectors = V1, V2, V3 ... Vn
```

The task is:

```
Find Vi such that distance(Q, Vi) is minimum
```

or

```
similarity(Q, Vi) is maximum
```

---

# 4. Example of Nearest Neighbor Search

Suppose we have these embeddings:

| Text         | Vector            |
| ------------ | ----------------- |
| apple fruit  | [0.2, 0.5, 0.6]   |
| mango fruit  | [0.2, 0.45, 0.62] |
| iphone phone | [0.9, 0.1, 0.3]   |

User query:

```
"healthy fruit"
```

Query embedding:

```
Q = [0.22, 0.48, 0.61]
```

Similarity comparison:

| Text         | Cosine Similarity |
| ------------ | ----------------- |
| apple fruit  | 0.99              |
| mango fruit  | 0.98              |
| iphone phone | 0.20              |

Nearest neighbors:

```
1. apple fruit
2. mango fruit
```

The system retrieves **fruit-related results**.

---

# 5. Types of Nearest Neighbor Search

### 1. Exact Nearest Neighbor (ENN)

Searches **all vectors**.

Advantages

* Perfect accuracy

Disadvantages

* Very slow for large datasets

---

### 2. Approximate Nearest Neighbor (ANN)

Searches **only a subset of vectors using smart indexing**.

Advantages

* Very fast
* Scalable

Disadvantages

* Slight accuracy loss

Most modern systems use **ANN**.

---

# 6. Popular Vector Indexing Methods

### 1. KD Tree

Tree structure used for **low dimensional vectors**.

```
          Root
         /    \
     Cluster1 Cluster2
```

Limitation:

Not efficient for **high dimensional embeddings** (like 768 or 1536).

---

### 2. HNSW (Hierarchical Navigable Small World)

One of the **most popular ANN algorithms**.

Idea:

Vectors are connected like a **graph network**.

Search jumps through **nearest nodes** until the best match is found.

Used in:

* search engines
* AI assistants
* recommendation systems

---

### 3. IVF (Inverted File Index)

Vectors are grouped into **clusters**.

Search process:

```
Query → choose closest cluster → search inside cluster
```

Used for **very large datasets**.

---

# 7. Vector Databases

Vector databases store embeddings and perform fast similarity search.

Examples:

| Vector Database | Use                                |
| --------------- | ---------------------------------- |
| Pinecone        | Semantic search                    |
| Weaviate        | AI applications                    |
| Milvus          | Large-scale vector retrieval       |
| FAISS           | Facebook similarity search library |
| Chroma          | RAG applications                   |

These databases implement **vector indexing + ANN search**.

---

# 8. Role in Generative AI Systems

Vector indexing and nearest neighbor search are essential for **Retrieval Augmented Generation (RAG)**.

Workflow:

```
User Query
    ↓
Convert query to embedding
    ↓
Vector database search
    ↓
Retrieve most similar documents
    ↓
Send documents to LLM
    ↓
Generate final answer
```

Example applications:

* ChatGPT knowledge retrieval
* Document search
* Semantic search
* Recommendation systems
* Question answering

---

# 9. Example: Semantic Search System

Dataset:

```
Doc1: Apple is a fruit
Doc2: iPhone is a smartphone
Doc3: Mango is a tropical fruit
```

Step 1: Convert documents into embeddings.

Step 2: Store embeddings in vector index.

Step 3: User query:

```
"healthy fruits"
```

Step 4: Query embedding is compared using nearest neighbor search.

Retrieved results:

```
Doc1
Doc3
```

---

# 10. Summary

| Concept                 | Meaning                               |
| ----------------------- | ------------------------------------- |
| Embedding               | Text converted into vector            |
| Vector Indexing         | Organizing vectors for fast search    |
| Nearest Neighbor Search | Finding closest vectors               |
| ANN                     | Fast approximate search               |
| Vector Database         | System to store and search embeddings |

---
