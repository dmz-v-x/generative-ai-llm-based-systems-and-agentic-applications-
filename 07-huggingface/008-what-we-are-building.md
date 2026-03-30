## Project: Food vs Not Food Text Classification Project

### 1. Project Overview

We are building a complete machine learning project from scratch to deployment.

#### Goal

Build a binary text classification model that predicts:

- Food  
- Not Food  

based on image caption text.

---

#### Full Pipeline

Data (Image Caption Text + Labels)  
→ Dataset (Hugging Face Datasets)  
→ Tokenization  
→ Model Training (Transformers)  
→ Upload Model (Hugging Face Hub)  
→ Demo (Gradio + Spaces)

---

#### Dataset Details

- Type: Text (image captions)
- Size: ~250 samples
- Labels:
  - 0 → Not Food  
  - 1 → Food  
- Source: Generated using LLMs

---

### 2. Step 1: Creating the Dataset

---

#### Step 2.1: Example Data Format

Your dataset should look like this:

| text | label |
|------|------|
| "A plate of pasta with cheese" | 1 |
| "A dog running in the park" | 0 |
| "Freshly baked chocolate cake" | 1 |
| "A car parked on the street" | 0 |

---

#### Step 2.2: Creating Dataset in Code

```python
from datasets import Dataset

data = {
    "text": [
        "A plate of pasta with cheese",
        "A dog running in the park",
        "Freshly baked chocolate cake",
        "A car parked on the street"
    ],
    "label": [1, 0, 1, 0]
}

dataset = Dataset.from_dict(data)
```

---

#### Step 2.3: Train/Test Split

```python
dataset = dataset.train_test_split(test_size=0.2)
```

---

### 3. Step 2: Tokenization (Preparing Text for Model)

---

#### Why Tokenization

Models do not understand text directly.

We convert:

Text → Tokens → IDs → Tensors

---

#### Step 3.1: Load Tokenizer

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("distilbert-base-uncased")
```

---

#### Step 3.2: Tokenization Function

```python
def tokenize(example):
    return tokenizer(example["text"], truncation=True, padding="max_length")
```

---

#### Step 3.3: Apply Tokenization

```python
tokenized_dataset = dataset.map(tokenize, batched=True)
```

---

### 4. Step 3: Model Creation and Training

---

#### Step 4.1: Load Model

```python
from transformers import AutoModelForSequenceClassification

model = AutoModelForSequenceClassification.from_pretrained(
    "distilbert-base-uncased",
    num_labels=2
)
```

---

#### Step 4.2: Training Setup

```python
from transformers import TrainingArguments

training_args = TrainingArguments(
    output_dir="./results",
    per_device_train_batch_size=8,
    per_device_eval_batch_size=8,
    num_train_epochs=3,
    evaluation_strategy="epoch",
    logging_dir="./logs"
)
```

---

#### Step 4.3: Trainer

```python
from transformers import Trainer

trainer = Trainer(
    model=model,
    args=training_args,
    train_dataset=tokenized_dataset["train"],
    eval_dataset=tokenized_dataset["test"]
)
```

---

#### Step 4.4: Train Model

```python
trainer.train()
```

---

### 5. Step 4: Evaluate Model

```python
trainer.evaluate()
```

You can also add metrics like accuracy later.

---

### 6. Step 5: Save and Upload Model

---

#### Step 6.1: Save Locally

```python
model.save_pretrained("./food-not-food-model")
tokenizer.save_pretrained("./food-not-food-model")
```

---

#### Step 6.2: Login to Hugging Face

```bash
huggingface-cli login
```

---

#### Step 6.3: Upload to Hub

```python
model.push_to_hub("food-not-food-model")
tokenizer.push_to_hub("food-not-food-model")
```

---

### 7. Step 6: Build Demo with Gradio

---

#### Step 7.1: Create Prediction Function

```python
from transformers import pipeline

classifier = pipeline(
    "text-classification",
    model="your-username/food-not-food-model"
)

def predict(text):
    result = classifier(text)[0]
    return result
```

---

#### Step 7.2: Gradio Interface

```python
import gradio as gr

interface = gr.Interface(
    fn=predict,
    inputs="text",
    outputs="text"
)

interface.launch()
```

---

### 8. Step 7: Deploy on Hugging Face Spaces

---

#### Steps

1. Go to Hugging Face Spaces
2. Create new Space
3. Select:
   - SDK: Gradio
4. Upload:
   - app.py
   - requirements.txt

---

#### Example requirements.txt

```
transformers
datasets
gradio
torch
```

---

### 9. Important Notes for Small Dataset (250 Samples)

---

#### Challenge

Small dataset can cause:

- Overfitting
- Poor generalization

---

#### Solutions

- Use pretrained models (transfer learning)
- Keep epochs low (2–5)
- Use validation split
- Try data augmentation (optional)

---

### 10. Final Mental Model

Dataset  
→ Tokenization  
→ Pretrained Model  
→ Fine-tuning  
→ Evaluation  
→ Upload  
→ Demo  
