# Attention, Self-Attention, and Multi-Head Attention  

## 1. What Is Attention?

At its simplest:

Attention means “focus on what matters.”

Humans naturally use attention when processing language.

Example sentence:

"The cat sat on the mat."

To understand the word "sat", your brain implicitly focuses on:

- "cat" → who performed the action  
- "mat" → where the action happened  

You do not treat every word equally.

Some words are more important for interpreting meaning.

---

### Attention in Machines

Machines cannot rely on intuition.

They must compute importance numerically.

Attention allows a model to:

- Look at all tokens
- Decide which tokens matter most
- Assign weights based on importance

Instead of fixed rules, importance is learned.

---

## 2. Why Attention Was Needed

Before Transformers, models like RNNs:

- Processed tokens sequentially
- Had memory limitations
- Struggled with long-distance relationships

Example difficulty:

"The book that you gave me yesterday is amazing."

RNNs often struggled to connect:

book → is amazing

Attention removes this bottleneck.

---

## 3. What Is Self-Attention?

Self-Attention means:

Each token pays attention to other tokens in the same sequence.

Instead of processing words one by one:

Every token interacts with every other token.

---

### Core Idea

For each token, the model asks:

Which other tokens are important for me?

Example:

"The dog chased the cat."

- "chased" attends to → dog, cat  
- "dog" attends to → chased  
- "cat" attends to → chased  

Each token builds context dynamically.

---

## 4. What Self-Attention Does Internally

Self-attention works using three learned components:

- Query  
- Key  
- Value  

Each token produces all three.

---

### 4.1 Query

Represents:

“What information am I looking for?”

---

### 4.2 Key

Represents:

“What information do I contain?”

---

### 4.3 Value

Represents:

“What information should I contribute?”

---

### The Interaction Process

For each token:

1. Compare its Query with Keys of other tokens  
2. Compute similarity scores  
3. Convert scores into weights  
4. Use weights to mix Values  

Result:

Context-aware representation.

---

## 5. Intuition via Example

Sentence:

"The cat ate the mouse."

When processing "ate":

Important tokens:

- cat (subject)
- mouse (object)

Less important tokens:

- the

Attention computes this importance automatically.

---

## 6. Simplified Mathematical View (No Heavy Math)

Self-attention computes:

Similarity(Query, Key)

Higher similarity → higher influence.

Then:

Weighted sum of Values.

Meaning emerges from interaction.

---

# Hands-On Mini Example (Numerical Intuition)

We simulate a tiny attention mechanism.

This is NOT a full Transformer — just intuition.

---

## 7. Toy Self-Attention in Python

	import numpy as np

	# Example token embeddings (3 tokens, 4 dimensions)
	X = np.array([
	    [1.0, 0.0, 1.0, 0.0],  # Token 1
	    [0.0, 2.0, 0.0, 2.0],  # Token 2
	    [1.0, 1.0, 1.0, 1.0]   # Token 3
	])

	# Random weight matrices (simulating learned parameters)
	W_Q = np.random.randn(4, 4)
	W_K = np.random.randn(4, 4)
	W_V = np.random.randn(4, 4)

	Q = X @ W_Q
	K = X @ W_K
	V = X @ W_V

	# Attention scores
	scores = Q @ K.T

	# Softmax normalization
	def softmax(x):
	    exp_x = np.exp(x - np.max(x, axis=-1, keepdims=True))
	    return exp_x / np.sum(exp_x, axis=-1, keepdims=True)

	weights = softmax(scores)

	# Final attention output
	output = weights @ V

	print("Attention Weights:")
	print(weights)

	print("\nContextualized Output:")
	print(output)

---

## 8. What This Demonstrates

- Tokens compare against each other
- Influence weights are computed
- Values are mixed

This is the core behavior of self-attention.

---

# Multi-Head Attention

---

## 9. What Is Multi-Head Attention?

Multi-Head Attention means:

Multiple independent attention mechanisms run in parallel.

Instead of one attention calculation:

Several attention heads operate simultaneously.

---

## 10. Why Multiple Heads Help

Single attention mechanism:

May focus on limited aspects.

Multiple heads allow specialization.

Example roles:

- Head 1 → Grammar relationships  
- Head 2 → Semantic similarity  
- Head 3 → Long-range dependencies  
- Head 4 → Positional structure  

Each head learns different patterns.

---

## 11. Conceptual Flow

For each head:

- Separate Query / Key / Value projections  
- Independent attention computation  

Outputs are combined.

---

## 12. Mental Model

Single attention:

One viewpoint.

Multi-head attention:

Multiple viewpoints combined.

---

# Concrete Example

---

## 13. Sentence Example

"The quick brown fox jumped over the lazy dog."

Self-attention:

- "quick" attends to → fox  
- "lazy" attends to → dog  

Multi-head:

- One head captures adjective relationships  
- Another captures subject–verb structure  
- Another captures long-distance dependencies  

Together:

Richer understanding.

---

# Why Attention Changed Everything

---

## 14. Key Advantages

Attention enables:

- Direct token-to-token interaction  
- Long-range dependency modeling  
- Parallel computation  
- Better contextual understanding  

---

## 15. Comparison with Older Models

Older sequential models:

- Limited memory  
- Slow training  
- Weak long-context handling  

Attention-based models:

- Global context awareness  
- Efficient scaling  
- Strong language modeling  

---

## 16. Final Mental Model

Attention allows tokens to dynamically determine:

“How much should other tokens influence me?”

Self-attention:

Tokens attend within the same sequence.

Multi-head attention:

Multiple attention mechanisms learn complementary relationships.

---

## 17. One-Sentence Summary

Attention mechanisms allow Transformer models to compute contextual relationships by dynamically weighting interactions between tokens, forming the foundation of modern Large Language Models.
