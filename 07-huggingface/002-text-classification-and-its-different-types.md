## Text Classification and its different types

### 1. What is Text Classification

#### Step 0: Understanding the Core Problem

In many real-world applications, we deal with text data such as:

- Emails
- Messages
- Reviews
- Articles
- Documents

The problem is:

How do we make a computer understand what this text means?

More specifically:
How do we automatically assign a category to a piece of text?

---

#### Step 1: Definition of Text Classification

Text Classification is the process of:

Categorizing text into one or more predefined classes or labels.

---

#### Step 2: Types of Text Inputs

Text classification can be applied to:

- A single word  
- A sentence  
- A paragraph  
- A full document  

---

#### Step 3: Types of Outputs

The output can be:

- A single category (e.g., "positive")
- Multiple categories (e.g., ["sports", "news"])

---

#### Step 4: Examples

| Input Text | Output Label |
|------------|-------------|
| "I love this product" | Positive |
| "This is spam message" | Spam |
| "Stock market crashes today" | Finance |
| "Football match was amazing" | Sports |

---

#### Step 5: Simple Example Using Hugging Face

```python
from transformers import pipeline

classifier = pipeline("text-classification")
classifier("This product is amazing")
```

---

### 2. When to Use Text Classification Models

Text classification is used when:

- You want to organize large amounts of text
- You need automatic decision-making based on text
- You want to extract meaning without manual effort

---

#### Common Scenarios

- Spam detection (Spam vs Not Spam)
- Sentiment analysis (Positive/Negative/Neutral)
- Topic classification (Sports, Politics, Tech)
- Intent detection (Chatbots understanding user intent)
- Content moderation (Offensive vs Safe)

---

#### Key Signal

If your problem can be framed as:

"Given this text → assign a label"

Then it is a text classification problem.

---

### 3. Binary Classification Example Model

#### What is Binary Classification

Binary classification means:

There are only two possible output classes.

---

#### Examples

- Spam vs Not Spam
- Positive vs Negative
- Fraud vs Not Fraud

---

#### Example Dataset

| Text | Label |
|------|------|
| "Win a free iPhone now" | Spam |
| "Let's meet tomorrow" | Not Spam |

---

#### Model Example

```python
from transformers import AutoModelForSequenceClassification

model = AutoModelForSequenceClassification.from_pretrained("distilbert-base-uncased")
```

---

#### How It Works

- Input text is tokenized
- Converted into numerical form
- Model outputs probability for two classes

Example Output:

```
[Spam: 0.92, Not Spam: 0.08]
```

---

### 4. Multi-label Classification Example Model

#### What is Multi-label Classification

A single input can belong to multiple classes at the same time.

---

#### Examples

Text:
"New AI technology in football analytics"

Labels:
- Technology
- Sports

---

#### Key Difference

Unlike binary or multi-class:
- More than one label can be true simultaneously

---

#### Example Dataset

| Text | Labels |
|------|--------|
| "AI in healthcare improves diagnosis" | ["AI", "Healthcare"] |
| "New movie released this week" | ["Entertainment"] |

---

#### Model Behavior

Output is usually:

```
AI: 0.85
Healthcare: 0.78
Sports: 0.10
```

Then a threshold is applied to decide final labels.

---

#### Model Example

```python
from transformers import AutoModelForSequenceClassification

model = AutoModelForSequenceClassification.from_pretrained("bert-base-uncased")
```

---

### 5. Multi-class Classification Example Model

#### What is Multi-class Classification

Each input belongs to exactly one class out of many possible classes.

---

#### Examples

- News classification:
  - Sports
  - Politics
  - Technology
  - Business

---

#### Example Dataset

| Text | Label |
|------|------|
| "Government passes new law" | Politics |
| "Team wins championship" | Sports |
| "New smartphone released" | Technology |

---

#### Key Rule

Only one label is correct for each input.

---

#### Model Behavior

Output probabilities:

```
Sports: 0.10
Politics: 0.80
Technology: 0.05
Business: 0.05
```

Final label:
Politics

---

#### Model Example

```python
from transformers import AutoModelForSequenceClassification

model = AutoModelForSequenceClassification.from_pretrained("bert-base-uncased")
```

---

### 6. Where is Text Classification Used in Real Life

Text classification is widely used across industries.

---

#### 6.1 Email Systems

- Spam detection
- Priority inbox sorting

---

#### 6.2 E-commerce

- Product review sentiment analysis
- Categorizing products

---

#### 6.3 Social Media

- Content moderation
- Hate speech detection
- Topic tagging

---

#### 6.4 Customer Support

- Ticket classification
- Intent detection for chatbots

---

#### 6.5 News and Media

- Article categorization
- Fake news detection

---

#### 6.6 Healthcare

- Medical report classification
- Diagnosis prediction support

---

#### 6.7 Finance

- Fraud detection
- Document classification

---

### Final Mental Model

Input Text  
→ Tokenization  
→ Convert to Numbers (Tensors)  
→ Model Prediction  
→ Output Label(s)  
