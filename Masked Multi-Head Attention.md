# 🎓 Lecture 2: Masked Multi-Head Attention (Decoder Deep Dive)

## 🎬 Introduction (Hook)

> **“Hi guys, my name is Nitesh, and welcome back to Day 11 of Deep Learning playlist!”**

Aaj hum Transformers ka **decoder part** start kar rahe hain — and trust me, yeh thoda tricky hone wala hai 😄
But don’t worry — hum step-by-step build karenge.

---

## 🔁 Quick Recap (Previous Progress)

Ab tak humne:

* ✅ Transformer architecture overview
* ✅ Encoder architecture (complete)
* ✅ Self-Attention & Multi-Head Attention
* ✅ Positional Encoding
* ✅ Add & Norm layers

👉 **Conclusion:**
Encoder = ✔️ Done
Decoder = 🔥 Start now

---

## 🧩 Decoder: What’s New?

Decoder mein mostly cheezein repeat hoti hain:

* Multi-head attention
* Feed-forward network
* Add & Norm

❗ But 2 **new components**:

1. **Masked Multi-Head Attention**
2. **Cross Attention**

👉 Aaj ka focus:

> **Masked Multi-Head Attention**

---

## 🧠 Core Statement (Most Important Concept)

> **“Transformer decoder is auto-regressive at inference time but non-auto-regressive during training.”**

Yahi pura lecture ka heart hai 💡

---

## 📌 Step 1: What is “Auto-Regressive”?

### Simple Meaning:

> Next output depends on previous outputs

### Example:

Sentence generation:

```
"I am fine"
```

Model generates like:

* Step 1 → “I”
* Step 2 → “am” (depends on “I”)
* Step 3 → “fine” (depends on “I am”)

👉 **Sequential dependency = Auto-regressive**

---

## ⚙️ Why Auto-Regressive is Necessary?

Because:

* Language = Sequential data
* Future words depend on past words

❌ You **cannot generate full sentence at once**

---

## 🔍 Training vs Inference Difference

### 🔹 Inference (Prediction Time)

* Model does:

```
previous output → next input
```

👉 Fully **auto-regressive**

---

### 🔹 Training Time

We use:

> **Teacher Forcing**

Meaning:

* Model ka output ignore karo
* Dataset ka correct word use karo

---

### ⚡ Result:

👉 Training becomes **parallelizable**

---

## 🚨 Problem 1: If Training is Auto-Regressive

* Sequential processing
* Very slow ❌

Example:

* 300-word sentence → 300 steps

👉 Not scalable

---

## 🚨 Problem 2: If Training is Fully Parallel

* Faster ✅
* BUT…

👉 Model sees **future words**

### Example:

While predicting “आप”:

* It also sees “कैसे” and “हैं”

👉 ❌ **Data Leakage**

---

## 😵 Problem Summary

| Approach                 | Issue        |
| ------------------------ | ------------ |
| Auto-regressive training | Slow         |
| Parallel training        | Data leakage |

---

## 💡 Solution: Masked Self Attention

👉 **Best of both worlds**

* ✔ Parallel computation
* ✔ No future information leakage

---

## 🔬 How Masking Works (Core Idea)

Self-attention normally:

* Each word attends to **all words**

### ❌ Problem:

Future tokens bhi include ho jaate hain

---

### ✅ Solution: Apply Mask

We create a **mask matrix**:

```
Allowed:
[✔ past, ✔ current]

Blocked:
[❌ future]
```

---

## 🧮 Conceptual View

For sentence:

```
आप कैसे हैं
```

### Without Mask:

```
आप → sees कैसे, हैं ❌
कैसे → sees हैं ❌
```

---

### With Mask:

```
आप → sees only आप ✔
कैसे → sees आप + कैसे ✔
हैं → sees all ✔
```

---

## ⚙️ Technical Trick (Important)

Mask matrix me:

* Allowed positions → 0
* Blocked positions → **-∞ (minus infinity)**

Then:

👉 Apply **Softmax**

### Result:

```
softmax(-∞) = 0
```

👉 Future attention automatically becomes zero

---

## 🎯 Final Understanding

Masked attention ensures:

* ❌ No cheating (no future info)
* ✅ Parallel computation
* ✅ Faster training
* ✅ Correct inference behavior

---

## 🧠 Big Picture

| Stage     | Behavior                     |
| --------- | ---------------------------- |
| Training  | Parallel + Masked            |
| Inference | Sequential (Auto-regressive) |

---

## 🚀 Intuition Summary

> “Training mein model ko future nahi dikhana, but speed bhi maintain karni hai.”

👉 Masking = Smart restriction

---

## 📌 Real Insight (Interview Level)

👉 Masked attention solves:

* Data leakage
* Training inefficiency

👉 This is **core reason why Transformers scale so well**

---

