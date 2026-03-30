## Setting Up Environment for Hugging Face 

### 1. Create a Hugging Face Account

#### Step 1.1: Go to Website

Visit:
https://huggingface.co

---

#### Step 1.2: Sign Up

- Click on "Sign Up"
- Enter:
  - Email
  - Username
  - Password

---

#### Step 1.3: Why This Is Needed

You need an account to:

- Upload models
- Access private resources
- Use Hugging Face Hub features
- Deploy demos (Spaces)

---

### 2. Create a Hugging Face Access Token

#### Step 2.1: Go to Token Settings

https://huggingface.co/settings/tokens

---

#### Step 2.2: Create New Token

- Click "New Token"
- Give it a name (example: `colab-access`)
- Select permissions

---

#### Step 2.3: Permission Types

- Read → Download models/datasets from Hugging Face  
- Write → Upload models/datasets to Hugging Face  
- Fine-grained → Custom permissions (recommended for advanced control)

For this project:

Select:
- Read access  
- Write access  

---

#### Step 2.4: Generate Token

- Click "Create Token"
- Copy the token immediately

---

#### Important Security Note

Do NOT share your token.

Treat it like a password.

---

### 3. Set Up Google Colab Environment

---

#### Step 3.1: Open Colab

Go to:
https://colab.research.google.com

---

#### Step 3.2: Create New Notebook

- Click "New Notebook"
- Optionally rename it:
  `food-not-food.ipynb`

---

#### Step 3.3: Open Secrets Manager

- Click the key icon (left sidebar)
- This opens "Secrets"

---

#### Step 3.4: Add Your Token

- Add new secret:
  - Name: your chosen name (example: `HF_TOKEN`)
  - Value: paste your Hugging Face token

---

### 4. Access Token in Colab Code

---

#### Step 4.1: Retrieve Token Securely

```python
from google.colab import userdata

HF_TOKEN = userdata.get("HF_TOKEN")
HF_TOKEN
```

---

#### Step 4.2: Why This Approach Is Important

- Keeps token hidden
- Avoids hardcoding secrets in code
- Safer for sharing notebooks

---

### 5. Alternative Method: Login via Hugging Face CLI

---

#### Step 5.1: Install Required Library

```python
!pip install huggingface_hub
```

---

#### Step 5.2: Import Library

```python
import huggingface_hub
```

---

#### Step 5.3: Login Interactively

```python
huggingface_hub.login()
```

---

#### Step 5.4: What Happens Next

- You will be prompted to enter your token
- Paste your token
- If valid → login successful

---

### 6. When to Use Which Method

#### Use Secrets (Recommended)

- More secure
- Better for production and shared notebooks

---

#### Use Interactive Login

- Quick testing
- Simple experiments

---

### 7. Verifying Setup

You can test your setup by loading a model:

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("bert-base-uncased")
```

If no error occurs, setup is successful.

---

### 8. Common Mistakes

- Forgetting to copy token immediately
- Using wrong token name in `userdata.get()`
- Not enabling write access (cannot upload models)
- Exposing token publicly in code

---

### Final Mental Model

Create Account  
→ Generate Token (Read + Write)  
→ Store Token Securely (Colab Secrets)  
→ Access Token in Code  
→ Login to Hugging Face  
