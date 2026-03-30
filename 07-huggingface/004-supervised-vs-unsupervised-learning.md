## Supervised Learning vs Unsupervised Learning

### 1. Introduction to Machine Learning Learning Types

Machine Learning can be broadly divided based on how models learn from data.

The two most fundamental types are:

- Supervised Learning  
- Unsupervised Learning  

The key difference lies in the availability of labels in the data.

---

### 2. What is Supervised Learning

#### Step 0: Core Idea

In supervised learning, the model learns from labeled data.

This means:

Each input has a corresponding correct output.

---

#### Step 1: Definition

Supervised Learning is a type of machine learning where the model is trained on input-output pairs, learning to map inputs to correct outputs.

---

#### Step 2: Simple Analogy

Think of it like learning with a teacher:

- Teacher gives a question (input)
- Teacher also provides the correct answer (label)
- You learn by comparing your answer with the correct one

---

#### Step 3: Example

Dataset:

| Input (Text) | Output (Label) |
|-------------|----------------|
| "I love this product" | Positive |
| "This is terrible" | Negative |

---

#### Step 4: How It Works

1. Input data is given
2. Model makes prediction
3. Prediction is compared with actual label
4. Error is calculated
5. Model updates itself

---

#### Step 5: Types of Supervised Learning

##### Classification

Output is categorical.

Examples:
- Spam vs Not Spam
- Positive vs Negative

---

##### Regression

Output is continuous (numeric).

Examples:
- House price prediction
- Temperature prediction

---

#### Step 6: Common Algorithms

- Linear Regression
- Logistic Regression
- Decision Trees
- Random Forest
- Neural Networks

---

### 3. What is Unsupervised Learning

#### Step 0: Core Idea

In unsupervised learning, the model works with unlabeled data.

There are no predefined correct answers.

---

#### Step 1: Definition

Unsupervised Learning is a type of machine learning where the model tries to find patterns, structure, or relationships in data without labeled outputs.

---

#### Step 2: Simple Analogy

Think of it like exploring without a teacher:

- You are given data
- No answers are provided
- You try to find patterns yourself

---

#### Step 3: Example

Dataset:

| Input |
|------|
| "Football match today" |
| "Stock market crash" |
| "New smartphone release" |

The model groups them into categories automatically.

---

#### Step 4: How It Works

1. Input data is given
2. Model identifies patterns
3. Groups or structures data based on similarity

---

#### Step 5: Types of Unsupervised Learning

##### Clustering

Grouping similar data points.

Examples:
- Customer segmentation
- Document grouping

---

##### Dimensionality Reduction

Reducing number of features while preserving information.

Examples:
- PCA (Principal Component Analysis)

---

#### Step 6: Common Algorithms

- K-Means Clustering
- Hierarchical Clustering
- DBSCAN
- PCA

---

### 4. Key Differences

| Feature | Supervised Learning | Unsupervised Learning |
|--------|--------------------|----------------------|
| Data | Labeled | Unlabeled |
| Goal | Predict output | Find patterns |
| Guidance | Has correct answers | No correct answers |
| Output | Known categories or values | Hidden structure |
| Complexity | Easier to evaluate | Harder to evaluate |

---

### 5. When to Use Supervised Learning

Use supervised learning when:

- You have labeled data
- You want predictions
- You need measurable accuracy

Examples:
- Spam detection
- Sentiment analysis
- Price prediction

---

### 6. When to Use Unsupervised Learning

Use unsupervised learning when:

- You do not have labels
- You want to explore data
- You want to discover hidden patterns

Examples:
- Customer segmentation
- Topic grouping
- Anomaly detection

---

### 7. Real-World Examples

#### Supervised Learning

- Email spam classification
- Credit risk prediction
- Medical diagnosis

---

#### Unsupervised Learning

- Grouping users by behavior
- Market basket analysis
- Clustering news articles

---

### 8. Final Mental Model

Supervised Learning:
Input + Correct Output → Learn Mapping → Predict  

Unsupervised Learning:
Input Only → Find Patterns → Discover Structure  
