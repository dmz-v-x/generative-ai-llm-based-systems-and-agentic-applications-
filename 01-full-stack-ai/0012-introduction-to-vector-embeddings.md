# What Are Vector Embeddings?  

## 1. What Is a Vector Embedding?

A **vector embedding** is a way to convert something that is not numerical (like text) into a list of numbers.

Example of a vector:

[0.12, 3.98, -1.44, 5.77]

Why this matters:

Machine learning models understand **numbers only**.

So embeddings act as the bridge:

Human Data → Numbers → Machine Processing

---

## 2. Why Do We Need Embeddings?

Computers do not understand meaning.

Humans instantly know:

cat and dog → similar  
cat and car → different

A computer only sees characters unless we represent meaning numerically.

Embeddings solve this by placing similar items near each other in a mathematical space.

---

## 3. What Is a Vector?

A vector is simply an ordered list of numbers.

Each number represents some learned feature.

You do not manually define these features — the model learns them.

---

## 4. What Do Embeddings Actually Do?

Embeddings place items into a multi-dimensional space.

Core idea:

Similar meaning → Vectors close together  
Different meaning → Vectors far apart

Example intuition:

cat → close to → dog  
cat → far from → car

---

## 5. Real-World Analogy

Imagine a large room:

cat → standing at one position  
dog → standing nearby  
car → standing far away

Distance represents similarity.

Closer = more similar

---

## 6. Why Embeddings Matter in NLP & LLMs

In language models:

raw text → tokens → embeddings → neural network

Embeddings are the **first numerical representation of meaning**.

Without embeddings, the model cannot process language.

---

## 7. Simple Conceptual Example

Suppose we imagine only two features:

Feature 1 → animal vs non-animal  
Feature 2 → common pet vs not pet

Then hypothetical vectors:

| Word | Vector     |
|------|------------|
| cat  | [0.9, 0.8] |
| dog  | [0.9, 0.8] |
| car  | [0.2, 0.1] |

cat and dog → close  
car → far

Real embeddings use hundreds or thousands of dimensions.

---

# Why Similar Words End Up Close

---

## 8. The Key Principle: Distributional Hypothesis

Core linguistic idea:

Words appearing in similar contexts tend to have similar meanings.

Models learn similarity from **usage patterns**, not definitions.

---

## 9. Example Language Patterns

Training text may contain:

"The cat sat on the mat."  
"The dog chased the ball."  
"I pet my cat."  
"The dog is a good pet."

Observation:

cat and dog appear near similar words:

pet, animal, food, play

This repeated context similarity shapes embeddings.

---

## 10. How Training Creates Meaningful Embeddings

Embeddings do NOT start meaningful.

They start random.

---

### Step 1 — Random Initialization

Initially:

cat → random numbers  
dog → random numbers  
car → random numbers

No meaning exists yet.

---

### Step 2 — Training Begins

Example training task:

Predict neighboring words.

Sentence:

"The cat chased the mouse."

Model learns:

cat → relates to → chased, mouse

Repeated across millions of examples.

---

### Step 3 — Gradual Adjustment

If predictions are wrong:

Vectors are slightly adjusted.

Over time:

Words with similar contexts → receive similar adjustments → move closer

---

## 11. Life Cycle of Embeddings

Before training:

All vectors random.

During training:

Vectors shift based on prediction accuracy.

After training:

Semantic structure emerges.

Similarity reflects usage patterns.

---

# Hands-On Example — Build a Tiny Embedding System

We will simulate embedding learning using a toy dataset.

This is NOT a real LLM — just intuition-building.

---

## 12. Step 1 — Install Dependencies

```bash
pip install numpy
```

---

## 13. Step 2 — Create Vocabulary

```python
import numpy as np

vocab = ["cat", "dog", "car", "apple"]
embedding_dim = 3

embeddings = {
    word: np.random.randn(embedding_dim)
    for word in vocab
}

print(embeddings)
```

Output:

Random vectors.

---

## 14. Step 3 — Define Similarity Function

```python
def cosine_similarity(v1, v2):
    return np.dot(v1, v2) / (np.linalg.norm(v1) * np.linalg.norm(v2))
```

---

## 15. Step 4 — Measure Initial Similarities

```python
print("cat vs dog:", cosine_similarity(embeddings["cat"], embeddings["dog"]))
print("cat vs car:", cosine_similarity(embeddings["cat"], embeddings["car"]))
```

Results are random.

No structure yet.

---

## 16. Step 5 — Simulate Training Adjustment

We manually push related words closer.

```python
embeddings["dog"] += embeddings["cat"] * 0.5
```

Recalculate:

```python
print("cat vs dog:", cosine_similarity(embeddings["cat"], embeddings["dog"]))
```

Similarity increases.

This mimics training behavior conceptually.

---

# How Models Actually Learn Embeddings

---

## 17. What Changes the Weights?

Humans do NOT adjust embeddings manually.

The model updates itself using:

- Loss Function
- Backpropagation
- Optimization Algorithms

---

## 18. Step-by-Step Learning Cycle

---

### Step 1 — Model Predicts

Example:

"The cat sat on the ___"

Prediction:

dog

True token:

mat

---

### Step 2 — Loss Computed

Loss measures:

How wrong was the prediction?

Large mistake → large loss

---

### Step 3 — Backpropagation

Model calculates:

Which parameters caused the error?

---

### Step 4 — Optimizer Updates Parameters

Rule:

parameter ← parameter − adjustment

Millions of tiny updates → learning emerges.

---

# Self-Supervised Learning (Critical Concept)

---

## 19. Where Does the “Correct Answer” Come From?

In LLMs:

The dataset itself provides labels.

Sentence:

"The cat sat on the mat."

Training pairs:

"The" → "cat"  
"The cat" → "sat"

No human labels needed.

---

## 20. Why This Works

The next token already exists in text.

The model learns by predicting known tokens.

This is called **self-supervised learning**.

---

# Full Training Mini Walkthrough

---

## 21. Example Sentence

"Hello world!"

---

### Step 1 — Tokenize

["Hello", "world", "!"]

---

### Step 2 — Create Training Pairs

["Hello"] → "world"  
["Hello", "world"] → "!"

---

### Step 3 — Prediction + Loss + Update

Repeated millions of times.

Gradual improvement.

---

# Final Mental Model

---

## 22. Embeddings Explained Simply

Embeddings:

Start random →  
Shift via training →  
Become structured →  
Capture similarity via context patterns

---

## 23. One-Sentence Summary

Vector embeddings are numerical representations that encode meaning by placing similar items close together in a mathematical space, learned automatically through training.
