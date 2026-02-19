# Positional Encoding in Transformers  

## 1. What Is Positional Encoding?

Transformers process all tokens at the same time.

Unlike older models (RNNs / LSTMs), they do not read text sequentially.

Because of this:

Transformers do not inherently know word order.

---

Example problem:

"The dog chased the cat."

Could look similar to:

"Chased cat the the dog."

If the model only sees embeddings.

---

Positional Encoding solves this problem.

Definition:

Positional Encoding injects information about token positions into the model.

It tells the model:

- Which token is first  
- Which token is second  
- Which token is tenth  

---

## 2. Why Transformers Need Positional Encoding

Transformers use self-attention, which:

- Looks at all tokens simultaneously  
- Ignores sequence order unless specified  

Without positional information:

The model treats text like a bag of words.

Which is incorrect for language.

---

Language depends on order.

Example:

Dog bites man  
Man bites dog  

Same words → different meaning.

---

## 3. How Positional Encoding Works Conceptually

Each token receives:

1. Token Embedding → Meaning  
2. Positional Encoding → Position  

These two vectors are combined.

---

Final Input Vector:

Token Meaning + Token Position

---

## 4. How Position Is Combined with Embeddings

Very important detail:

We add positional encodings to embeddings.

Not concatenate.

---

Example:

Embedding(token) = [0.2, 0.8, -0.4]  
PositionVector    = [0.5, 0.1,  0.3]

Final Input:

[0.7, 0.9, -0.1]

---

Why addition?

- Keeps dimensionality constant  
- Efficient computation  
- Blends meaning and position  

---

## 5. Why Position Matters

Consider:

"I love AI"

Without positional encoding:

love AI I

Could look statistically similar.

But meaning is broken.

---

Position provides structural understanding.

---

## 6. How Positions Are Represented

There are multiple strategies.

---

### 6.1 Learned Positional Embeddings

- Model learns position vectors  
- Similar to token embeddings  
- Flexible but limited to trained lengths  

---

### 6.2 Sinusoidal Positional Encoding (Original Paper)

The Transformer paper used:

Sine and Cosine functions.

Why?

- Unique pattern per position  
- Encodes relative distances  
- Smooth mathematical structure  
- Works for unseen sequence lengths  

---

## 7. Core Idea of Sinusoidal Encoding

Instead of learning position vectors:

We compute them using sine and cosine waves.

Each dimension uses a different frequency.

---

Mental model:

Each position gets a unique waveform signature.

---

## 8. Why Sine and Cosine Work Well

They provide:

- Unique representation per position  
- Relative distance awareness  
- Continuous smooth structure  
- Extrapolation capability  

---

Example intuition:

Position 5 looks mathematically related to Position 6.

Unlike arbitrary learned vectors.

---

# Hands-On Implementation in Python

Now we build positional encodings manually.

This builds deep intuition.

---

## 9. Step 1 — Install Dependencies

	pip install numpy matplotlib

---

## 10. Step 2 — Implement Positional Encoding

	import numpy as np

	def positional_encoding(position, d_model):
	    pe = np.zeros((position, d_model))
	    
	    for pos in range(position):
	        for i in range(0, d_model, 2):
	            angle = pos / np.power(10000, (i / d_model))
	            
	            pe[pos, i] = np.sin(angle)
	            
	            if i + 1 < d_model:
	                pe[pos, i + 1] = np.cos(angle)
	                
	    return pe

	pe = positional_encoding(10, 6)

	print(pe)

---

## 11. Understanding This Code

We created a matrix:

(number_of_positions, embedding_dimension)

Each row represents one position vector.

Each column represents one embedding dimension.

---

## 12. Step 3 — Visualizing Positional Patterns

	import matplotlib.pyplot as plt

	plt.figure(figsize=(10, 5))
	plt.imshow(pe, aspect='auto')
	plt.colorbar()
	plt.title("Positional Encoding Heatmap")
	plt.xlabel("Embedding Dimensions")
	plt.ylabel("Token Positions")
	plt.show()

Observation:

Each position has a unique pattern.

Nearby positions have similar but slightly shifted values.

---

## 13. Step 4 — Plotting Individual Dimensions

	for dim in range(pe.shape[1]):
	    plt.plot(pe[:, dim], label=f"Dim {dim}")

	plt.legend()
	plt.title("Positional Encoding Waves")
	plt.show()

You will observe sinusoidal waveforms.

Each dimension oscillates at a different frequency.

---

## 14. Why Different Frequencies?

Different dimensions oscillate at different speeds.

This allows the model to encode:

- Absolute positions  
- Relative positions  
- Distance relationships  

---

## 15. Relative Position Understanding

Because sinusoidal functions are smooth:

Vectors for nearby positions are similar.

Vectors for distant positions differ significantly.

Example intuition:

Vector(pos=5) is similar to Vector(pos=6)

But very different from Vector(pos=100)

---

## 16. Why Not Use Raw Position Numbers?

Raw numbers provide very limited representational power.

Sinusoidal encoding transforms positions into rich numerical patterns.

This improves learning stability and generalization.

---

## 17. Learned vs Fixed Positional Encodings

### Fixed (Sinusoidal)

Advantages:

- No learning required  
- Generalizes to longer sequences  

Limitations:

- Less flexible  

---

### Learned

Advantages:

- Task-optimized  
- Flexible representation  

Limitations:

- Cannot extrapolate easily  

---

## 18. Modern Variants

Modern models often use:

- Rotary Positional Embeddings (RoPE)  
- Relative Positional Encoding  
- ALiBi (Attention with Linear Biases)  

These improve long-context performance.

---

## 19. Key Design Insight

Effective positional encoding must:

- Preserve order  
- Support attention mechanisms  
- Scale efficiently  
- Encode distance relationships  

---

## 20. Final Mental Model

Positional Encoding adds positional information into token embeddings.

Final vectors contain:

- What the token represents  
- Where the token appears  

---

## 21. One-Sentence Summary

Positional Encoding enables Transformers to understand sequence order by injecting structured position information into token embeddings.
