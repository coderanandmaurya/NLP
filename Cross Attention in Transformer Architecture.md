# 🎯 Lecture: Cross Attention in Transformer Architecture

## 1. Introduction & Plan of Action

Before diving into today’s topic, let’s briefly align on our learning strategy.

We have been studying the **Transformer architecture** over multiple sessions. Instead of covering everything in a single lecture, we are taking a **modular and layered approach** because the architecture is complex.

### What we’ve covered so far:

* Encoder architecture ✅

  * Embeddings
  * Positional Encoding
  * Self-Attention
  * Multi-Head Attention
  * Normalization

* Decoder (started recently) ✅

  * Masked Self-Attention

### Today’s Focus:

👉 A **critical component of the decoder** — **Cross Attention**

---

## 2. Where Cross Attention Fits

In the decoder architecture, the **second attention block** is slightly different from the others.

### Key Observation:

* In standard **self-attention**:

  * Query, Key, Value → come from the *same sequence*

* In this block:

  * Some inputs come from the **encoder**
  * Some come from the **decoder**

👉 This is called **Cross Attention**

---

## 3. What is Cross Attention?

### Definition:

Cross Attention is a mechanism used in Transformer architectures (especially in sequence-to-sequence tasks) that allows the model to **focus on relevant parts of the input sequence while generating the output sequence**.

---

## 4. Intuition via Example (Machine Translation)

Let’s understand using a simple example:

### Task:

Translate English → Hindi

**Input (Encoder):**
"I like eating ice cream"

**Output (Decoder):**
Generated step-by-step:

* Step 1 → "I"
* Step 2 → "ice cream"
* Step 3 → "eat"
* ...

---

## 5. Key Question

At any decoding step, say step 3:

👉 **What determines the next word?**

### Two factors:

1. **Previously generated output**
2. **Input sentence (from encoder)**

---

## 6. Role of Attention Types

### 1. Self-Attention (in Decoder)

* Captures relationships within the **generated output so far**
* Example:

  * Helps decide next word based on previous words

---

### 2. Cross Attention

* Captures relationships between:

  * **Input sequence (encoder)**
  * **Output sequence (decoder)**

👉 It answers:

> “Which input word is most relevant to the current output word?”

---

## 7. Core Idea of Cross Attention

* Self-attention → relationships **within one sequence**
* Cross-attention → relationships **between two sequences**

---

## 8. How Cross Attention Works

### Step 1: Inputs

Unlike self-attention:

| Attention Type  | Input         |
| --------------- | ------------- |
| Self-Attention  | One sequence  |
| Cross Attention | Two sequences |

---

### Step 2: Key Difference in Q, K, V

| Component | Source                    |
| --------- | ------------------------- |
| Query (Q) | Decoder (output sequence) |
| Key (K)   | Encoder (input sequence)  |
| Value (V) | Encoder (input sequence)  |

---

### Step 3: Computation Flow

1. Generate embeddings for both sequences
2. Compute:

   * Q from decoder
   * K and V from encoder
3. Compute attention scores:

   * Q × K
4. Apply softmax → attention weights
5. Multiply with V → get output

---

## 9. Output of Cross Attention

### Important Rule:

Number of output vectors =
👉 Number of tokens in the **decoder (output sequence)**

Each output embedding:

* Represents how much each input word contributes to that output word

---

## 10. Comparison: Self vs Cross Attention

| Aspect  | Self Attention        | Cross Attention          |
| ------- | --------------------- | ------------------------ |
| Input   | Single sequence       | Two sequences            |
| Q, K, V | Same source           | Different sources        |
| Purpose | Internal context      | Input-output alignment   |
| Output  | Contextual embeddings | Cross-context embeddings |

---

## 11. Connection to Earlier Models

Cross Attention is conceptually similar to:

👉 **Bahdanau Attention**
👉 **Luong Attention**

In earlier RNN-based encoder-decoder models:

* We computed similarity between decoder state and encoder outputs

👉 Cross Attention is the **Transformer equivalent** of that idea.

---

## 12. Why Cross Attention is Needed

Without cross attention:

* Decoder would only rely on its own generated words
* It would **lose connection with input meaning**

Cross Attention ensures:
✔ Proper alignment
✔ Context preservation
✔ Accurate generation

---

## 13. Applications of Cross Attention

### Sequence-to-Sequence Tasks:

* Machine Translation
* Text Summarization
* Question Answering

### Multimodal Tasks:

* Image Captioning (Image → Text)
* Text-to-Image Generation
* Text-to-Speech

---

## 14. Final Takeaways

* Cross Attention connects **encoder and decoder**
* It enables **alignment between input and output**
* It is **essential for Transformer performance**

---
