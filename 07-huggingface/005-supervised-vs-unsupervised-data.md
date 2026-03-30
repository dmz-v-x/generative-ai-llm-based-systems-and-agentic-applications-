## Supervised Dataset vs Unsupervised Dataset

### 1. Introduction to Dataset Types

In machine learning, everything starts with data.

The type of dataset you use determines:

- How the model learns
- What kind of problem you can solve
- Which algorithms you can apply

The two most fundamental dataset types are:

- Supervised Dataset  
- Unsupervised Dataset  

The key difference is the presence or absence of labels.

---

### 2. What is a Supervised Dataset

#### Step 0: Core Idea

A supervised dataset contains:

Input data + Corresponding correct output (labels)

---

#### Step 1: Definition

A supervised dataset is a dataset where each data point has an associated label or target value that the model is expected to learn.

---

#### Step 2: Structure

Each row in the dataset looks like:

```
Input → Output
```

---

#### Step 3: Examples

##### Example 1: Sentiment Analysis

| Text | Label |
|------|-------|
| "I love this product" | Positive |
| "This is bad" | Negative |

---

##### Example 2: Spam Detection

| Email | Label |
|-------|-------|
| "Win money now" | Spam |
| "Meeting at 5 PM" | Not Spam |

---

##### Example 3: Regression

| House Size | Price |
|------------|-------|
| 1000 sq ft | 50,000 |
| 2000 sq ft | 90,000 |

---

#### Step 4: Key Characteristics

- Labels are present
- Clear input-output mapping
- Used for prediction tasks
- Easy to evaluate performance

---

#### Step 5: How It Is Used

The model learns:

Given input → predict output

---

### 3. What is an Unsupervised Dataset

#### Step 0: Core Idea

An unsupervised dataset contains:

Only input data (no labels)

---

#### Step 1: Definition

An unsupervised dataset is a dataset where data points do not have associated labels, and the model must discover patterns or structure on its own.

---

#### Step 2: Structure

Each row looks like:

```
Input only
```

---

#### Step 3: Examples

##### Example 1: Customer Data

| Age | Income | Spending Score |
|-----|--------|----------------|
| 25 | 40,000 | 60 |
| 45 | 80,000 | 30 |

(No labels like "High Value Customer")

---

##### Example 2: Text Data

| Text |
|------|
| "Football match today" |
| "Stock market falls" |
| "New phone launched" |

(No predefined categories)

---

#### Step 4: Key Characteristics

- No labels
- Hidden patterns must be discovered
- Used for exploration and grouping
- Harder to evaluate

---

#### Step 5: How It Is Used

The model learns:

Find structure → group similar data → identify patterns

---

### 4. Key Differences

| Feature | Supervised Dataset | Unsupervised Dataset |
|--------|-------------------|---------------------|
| Labels | Present | Not present |
| Structure | Input + Output | Input only |
| Purpose | Prediction | Pattern discovery |
| Evaluation | Easy (accuracy, etc.) | Difficult |
| Example Task | Classification, Regression | Clustering |

---

### 5. Real-World Understanding

#### Supervised Dataset Example

Think of a teacher giving:

- Questions + correct answers

You learn by comparing your answers.

---

#### Unsupervised Dataset Example

Think of exploring data without guidance:

- No answers provided
- You must find patterns yourself

---

### 6. When to Use Each Dataset Type

#### Use Supervised Dataset When:

- You have labeled data
- You want predictions
- You know the target outcome

Examples:
- Spam detection
- Sentiment analysis
- Price prediction

---

#### Use Unsupervised Dataset When:

- You do not have labels
- You want to explore data
- You want to discover hidden structure

Examples:
- Customer segmentation
- Topic grouping
- Anomaly detection

---

### 7. Final Mental Model

Supervised Dataset:
Input + Label → Learn Mapping → Predict Output  

Unsupervised Dataset:
Input Only → Discover Patterns → Group Data  
