# Zero-Shot Prompting with OpenAI Models

## 1. What Is Zero-Shot Prompting?

Zero-shot prompting means:

You give the model instructions, but you do NOT give examples.

In simple terms:

Zero-shot prompting means:

- Tell the model what to do  
- Do NOT show examples of desired output  

The model must rely entirely on its pretrained knowledge.

This works because GPT models are trained on massive text data and already understand language patterns, grammar, reasoning structures, and task behaviors.

---

## 2. Why Is It Called "Zero-Shot"?

The term comes from machine learning.

Zero-shot learning refers to solving tasks without seeing labeled examples of that task during training.

In prompting:

- Zero-shot → No examples provided  
- Few-shot → A few examples provided  
- One-shot → Only one example provided  

Zero-shot simply means:

Zero examples in the prompt.

---

## 3. How Zero-Shot Works Internally

When you send a zero-shot prompt:

1. The model reads your instruction.
2. It interprets the task using patterns learned during pretraining.
3. It generates output based on probabilities.
4. No weights are updated (this is inference only).

Important idea:

The model is NOT learning during prompting.

It is applying existing knowledge.

---

## 4. Zero-Shot vs Few-Shot Prompting

| Aspect | Zero-Shot | Few-Shot |
|--------|-----------|-----------|
| Examples in prompt | None | Some |
| Prompt length | Short | Longer |
| Format reliability | Can vary | More stable |
| Setup effort | Minimal | Requires examples |

Zero-shot is simpler.

Few-shot is more guided.

---

## 5. Common Zero-Shot Use Cases

Zero-shot prompting works well for:

- Sentiment classification  
- Translation  
- Summarization  
- Question answering  
- Categorization  
- Brainstorming ideas  
- Explanation tasks  

It may struggle with highly specialized or rigid formatting tasks.

---

# Part 1 — Environment Setup

Before writing code, ensure:

- Python installed  
- Virtual environment created  
- OpenAI API key stored in `.env`  

---

# Part 2 — Installing Dependencies

Install required packages:

	pip install openai python-dotenv

This provides:

- openai → OpenAI Python SDK  
- python-dotenv → Secure environment variable handling  

---

# Part 3 — Storing API Key Securely

Create `.env` file:

	OPENAI_API_KEY=sk-XXXXXXXXXXXXXXXXXXXX

Never hardcode API keys.

Always use environment variables.

---

# Part 4 — Zero-Shot Prompting in Python

We now walk through multiple examples.

---

## Example 1 — Sentiment Classification

Create file: `zero_shot_sentiment.py`

	from dotenv import load_dotenv
	import os
	from openai import OpenAI

	load_dotenv()

	client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))

	prompt = """Classify the sentiment of the following review as Positive, Neutral, or Negative:
	Review: "I thought the movie was decent but a bit slow."
	Sentiment:"""

	response = client.chat.completions.create(
	    model="gpt-4o-mini",
	    messages=[
	        {"role": "user", "content": prompt}
	    ],
	    max_tokens=10
	)

	print("Sentiment:", response.choices[0].message.content.strip())

---

### Step-by-Step Explanation

**load_dotenv()**

Loads API key from `.env`.

---

**OpenAI Client**

	client = OpenAI(...)

Creates authenticated connection.

---

**Prompt**

Describes task clearly.

No examples included → Zero-shot.

---

**chat.completions.create**

Sends request to GPT model.

---

**model**

Specifies which GPT model to use.

---

**messages**

Represents conversation input.

---

**max_tokens**

Limits response length.

---

**choices[0].message.content**

Extracts generated output.

---

## Example 2 — Translation (Zero-Shot)

Create file: `zero_shot_translation.py`

	from dotenv import load_dotenv
	import os
	from openai import OpenAI

	load_dotenv()

	client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))

	prompt = """Translate the following text into Spanish:
	Text: "I am learning how to code"
	Translation:"""

	response = client.chat.completions.create(
	    model="gpt-4o-mini",
	    messages=[
	        {"role": "user", "content": prompt}
	    ]
	)

	print(response.choices[0].message.content.strip())

Explanation:

Instruction only → No examples → Zero-shot.

---

## Example 3 — Summarization

	from dotenv import load_dotenv
	import os
	from openai import OpenAI

	load_dotenv()

	client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))

	text = "Artificial Intelligence is transforming industries through automation."

	prompt = f"""Summarize this sentence:
	{text}
	Summary:"""

	response = client.chat.completions.create(
	    model="gpt-4o-mini",
	    messages=[
	        {"role": "user", "content": prompt}
	    ]
	)

	print(response.choices[0].message.content.strip())

---

## Example 4 — Brainstorming (Creative Task)

	prompt = "Generate 10 startup ideas using AI."

	response = client.chat.completions.create(
	    model="gpt-4o-mini",
	    messages=[
	        {"role": "user", "content": prompt}
	    ],
	    max_tokens=150
	)

	print(response.choices[0].message.content.strip())

Creative tasks work naturally with zero-shot prompts.

---

# Part 5 — Key Code Components Explained

---

## load_dotenv()

Loads environment variables.

Without this → API key unavailable.

---

## OpenAI Client

Handles:

- Authentication  
- API communication  
- Request management  

---

## Prompt

Defines task behavior.

Clarity determines quality.

---

## Messages Structure

Each message has:

- role → system / user / assistant  
- content → instruction / input  

---

## Model Parameter

Chooses GPT model variant.

Different models → Different capabilities.

---

## Response Object

Contains generated outputs.

Access via:

	response.choices[0].message.content

---

# Part 6 — Improving Zero-Shot Prompts

---

## Use Clear Instructions

Bad:

	Tell me something about this text.

Better:

	Summarize this text in one sentence.

---

## Specify Format When Needed

Example:

	Return the answer as JSON.

---

## Provide Constraints

Example:

	Explain in exactly one sentence.

---

# Part 7 — Pros & Cons

---

## Pros

- Very simple  
- No examples needed  
- Fast prompt construction  
- Flexible across tasks  

---

## Cons

- Can be less accurate  
- Sensitive to prompt wording  
- Less reliable for rigid formats  

---

# Part 8 — One-Sentence Summary

Zero-shot prompting means instructing a language model to perform a task using only descriptive instructions and no examples, relying entirely on pretrained knowledge.
