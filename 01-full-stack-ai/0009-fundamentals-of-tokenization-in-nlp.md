# Fundamentals of Tokenization in NLP  

### 1. What Is a Token?

A **token** is a small piece of text that a language model processes as a single unit.

A token could be:

- A whole word  
- Part of a word  
- A punctuation mark  
- A space  
- A single character  
- Even a byte  

Important idea:

A token is simply a **basic building block of text for a model**.

The exact definition depends on the model’s tokenizer.

---

### 2. Why Do Models Use Tokens Instead of Words?

Language models do not understand:

- Words  
- Sentences  
- Languages  

They understand **numbers only**.

So text must be converted into something numerical.

Tokens make this possible.

---

### 3. What Problem Does Tokenization Solve?

Tokenization helps models:

- Handle rare words  
- Support multiple languages  
- Reduce memory usage  
- Make predictions easier  
- Understand text at a finer level  

Example:

The word:

unbelievable

May be split into:

un | believ | able

This is easier for the model to process than one large word.

---

### 4. What Does Tokenization Actually Mean?

**Tokenization = Converting human text into tokens and then into numbers**

Let’s break this down.

---

### 5. Step-by-Step Tokenization Flow

#### Step 1 — User Writes Text

Example:

Hello

---

#### Step 2 — Tokenizer Splits Text

Possible outputs:

["Hello"]  

Or (subword split):

["Hel", "lo"]

---

#### Step 3 — Tokens Become Numbers

Example mapping:

"Hel" → 9182  
"lo" → 2013  

Internally, the model sees:

[9182, 2013]

Not the text.

---

### 6. Detokenization — The Reverse Process

**Detokenization = Numbers → Tokens → Human Text**

Example:

Numbers:

[1302, 354, 794]

Tokens:

["Hello", ",", "world"]

Final Output:

Hello, world

This is how model outputs become readable.

---

### 7. Why Tokenization Differs Between Models

Each model uses its own tokenizer.

This means:

- Different splitting rules  
- Different token vocabularies  
- Different token-to-number mappings  

Example comparison:

| Model         | Tokenizer Type           |
|--------------|--------------------------|
| GPT-2 / GPT-3 | Byte Pair Encoding (BPE) |
| GPT-4         | Modified BPE / tiktoken  |
| LLaMA         | SentencePiece            |
| BERT          | WordPiece                |

There is **no universal tokenizer**.

---

### 8. Why a Token Can Be “Anything”

Because a token is just:

A chunk of text treated as one unit.

Examples:

- "a"  
- "apple"  
- "app"  
- "##le" (subword marker in some models)  
- "!"  
- "नम"  
- "🙂"  

Different tokenizers choose different chunk sizes.

---

### 9. Mapping Tokens to Numbers

Think of a dictionary:

| Token   | ID   |
|--------|------|
| Hello  | 1302 |
| world  | 794  |
| ,      | 354  |

The model processes:

[1302, 354, 794]

Never raw text.

---

### 10. Why Tokenization Is Extremely Important

Tokenization affects:

#### Cost

Most APIs charge **per token**.

More tokens → Higher cost.

---

#### Speed

More tokens → More computation → Slower responses.

---

#### Quality

Poor tokenization → Broken language understanding.

---

#### Length Limits

Models have token limits.

Examples:

- GPT-3.5 → ~4K tokens  
- GPT-4 → ~128K tokens  
- GPT-4.1 → ~1M tokens  

Tokens determine how much text fits in memory.

---

### 11. Practical Example

User Input:

I love Transformers!

Possible tokenization:

"I" → 72  
" love" → 514  
" Transform" → 9918  
"ers" → 2403  
"!" → 0  

Model sees:

[72, 514, 9918, 2403, 0]

Not the sentence.

---

### 12. A Simple Mental Model

Text = Sentence  
Tokens = Lego pieces  
Tokenization = Breaking sentence into Lego pieces  
Detokenization = Rebuilding sentence from pieces  
Model = Understands only Lego numbers  

---

### 13. One-Sentence Summary

Tokenization is the process of breaking text into smaller units that can be converted into numbers so a language model can process them.
