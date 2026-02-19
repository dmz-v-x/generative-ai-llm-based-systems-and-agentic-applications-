# Implementing Tokenization in Python Using tiktoken  

This guide walks you step by step through setting up a Python environment and working with tokenization using the tiktoken library.

Important clarification:

This is NOT building a tokenizer from scratch.  
This is using a production-grade tokenizer — exactly what real LLM applications do.

---

## 1. Environment Setup

### 1.1 Create a Virtual Environment

```bash
python -m venv venv
```

This creates an isolated Python environment.

---

### 1.2 Activate the Environment

Mac / Linux:

```bash
source venv/bin/activate
```

Windows (PowerShell):

```bash
venv\Scripts\Activate.ps1
```

---

### 1.3 Install tiktoken

```bash
pip install tiktoken
```

---

### 1.4 Save Dependencies

```bash
pip freeze > requirements.txt
```

---

## 2. Basic Tokenization Example

### 2.1 Encoding Text → Tokens

```python
import tiktoken

enc = tiktoken.encoding_for_model("gpt-4o")

text = "Hey there"
tokens = enc.encode(text)

print("Tokens:", tokens)
```

Example output:

```
Tokens: [15496, 612]
```

Important idea:

The model sees numbers, not text.

---

### 2.2 Decoding Tokens → Text

```python
decoded = enc.decode(tokens)

print("Decoded:", decoded)
```

Output:

```
Decoded: Hey there
```

---

## 3. Multiple Examples

---

### Example 1 — Simple Sentence

```python
text = "I love transformers"
tokens = enc.encode(text)

print(tokens)
print(enc.decode(tokens))
```

---

### Example 2 — Large Word Splitting

```python
text = "unbelievable"
tokens = enc.encode(text)

print(tokens)
print(enc.decode(tokens))
```

Large words are often split internally.

---

### Example 3 — Punctuation Matters

```python
print(enc.encode("Hello"))
print(enc.encode("Hello!"))
```

Small changes → different tokens.

---

### Example 4 — Spaces Matter

```python
print(enc.encode("Hello"))
print(enc.encode(" Hello"))
```

Leading spaces change tokens.

---

### Example 5 — Emojis

```python
text = "Hello 🙂"
tokens = enc.encode(text)

print(tokens)
print(enc.decode(tokens))
```

Emojis may map to multiple tokens.

---

### Example 6 — Multilingual Text

```python
text = "नमस्ते world"
tokens = enc.encode(text)

print(tokens)
print(enc.decode(tokens))
```

Tokenizers handle multiple languages.

---

## 4. Counting Tokens (Very Important)

```python
text = "Explain Kubernetes in simple words"

tokens = enc.encode(text)

print("Token Count:", len(tokens))
```

Why this matters:

Costs and limits depend on tokens.

---

## 5. Comparing Encodings

```python
enc1 = tiktoken.get_encoding("cl100k_base")
enc2 = tiktoken.get_encoding("p50k_base")

text = "Hello world"

print(enc1.encode(text))
print(enc2.encode(text))
```

Different encodings → different splits.

---

## 6. Edge Cases

---

### 6.1 Very Long Text

```python
text = "hello " * 1000
tokens = enc.encode(text)

print(len(tokens))
```

More text → more tokens → more cost.

---

### 6.2 Decoding Arbitrary Tokens

```python
decoded = enc.decode([23452, 234, 0, 23523])

print(decoded)
```

Not all token sequences decode cleanly.

---

## 7. Practical Mini Project — Token Counter Tool

```python
import tiktoken

enc = tiktoken.encoding_for_model("gpt-4o")

def estimate_tokens(text):
    return len(enc.encode(text))

while True:
    user_input = input("Enter text: ")

    count = estimate_tokens(user_input)

    print("Token Count:", count)
    print("----------------------")
```

What this teaches:

- Prompt cost awareness  
- Token budgeting  
- Real-world intuition  

---

## 8. Key Mental Models

Tokenization:

Text → Tokens → Numbers

Detokenization:

Numbers → Tokens → Text

Models understand numbers only.

---

## 9. Common Beginner Misunderstandings

Tokens are NOT:

- Words  
- Characters  
- Fixed-length units  

Tokens are model-specific chunks.

---

## 10. One-Sentence Summary

tiktoken allows you to convert text into model-understandable numerical tokens and convert them back into readable text.
