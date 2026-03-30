## Setting Up Important Libraries for Hugging Face Text Classification

---

### 1. Notebook Setup

File name:

```
huggingface_text_classification_tutorial.ipynb
```

---

### 2. Enable GPU in Google Colab

#### Step 2.1: Why GPU is Needed

Training transformer models on CPU is:

- Very slow
- Inefficient for even small datasets

GPU helps:

- Faster training
- Faster inference
- Better experimentation

---

#### Step 2.2: Enable GPU

In Google Colab:

- Go to **Runtime**
- Click **Change runtime type**
- Set:
  - Hardware accelerator → **L4 GPU** (or any available GPU)

---

#### Step 2.3: Verify GPU

```python
import torch

torch.cuda.is_available()
```

If it returns `True`, GPU is enabled.

---

### 3. Import Necessary Libraries

---

### 3.1 Core Libraries

These are essential Hugging Face libraries:

- `transformers` → for models  
- `datasets` → for dataset handling  
- `evaluate` → for metrics  
- `accelerate` → for optimized training  
- `gradio` → for building demos  

---

### 3.2 Install and Import Safely

```python
try:
    import datasets, evaluate, accelerate
    import gradio as gr
except ModuleNotFoundError:
    !pip install -U datasets evaluate accelerate gradio
    import datasets, evaluate, accelerate
    import gradio as gr
```

---

#### Important Note

Make sure spelling is correct:

- `accelerate` (not `accerlate`)

---

### 3.3 Additional Libraries

```python
import random
import numpy as np
import pandas as pd
```

---

#### Why These Are Needed

- `random` → reproducibility / sampling  
- `numpy` → numerical operations  
- `pandas` → data handling  

---

### 3.4 PyTorch and Transformers

```python
import torch
import transformers
```

---

#### Why These Are Needed

- `torch` → deep learning backend  
- `transformers` → pretrained models and pipelines  

---

### 4. Verify Installed Versions

```python
print(f"Using transformers version: {transformers.__version__}")
print(f"Using torch version: {torch.__version__}")
print(f"Using datasets version: {datasets.__version__}")
```

---

#### Why This Is Important

- Ensures compatibility
- Helps debugging issues
- Confirms successful installation

---

### 5. Final Clean Setup Code

```python
# Install if missing
try:
    import datasets, evaluate, accelerate
    import gradio as gr
except ModuleNotFoundError:
    !pip install -U datasets evaluate accelerate gradio
    import datasets, evaluate, accelerate
    import gradio as gr

# Core libraries
import random
import numpy as np
import pandas as pd

# Deep learning + transformers
import torch
import transformers

# Version check
print(f"Using transformers version: {transformers.__version__}")
print(f"Using torch version: {torch.__version__}")
print(f"Using datasets version: {datasets.__version__}")
```

---

### 6. Common Issues and Fixes

#### Issue 1: Module Not Found

Fix:
- Run the pip install block again

---

#### Issue 2: Wrong Library Version

Fix:
```python
!pip install -U transformers datasets
```

---

#### Issue 3: GPU Not Detected

Fix:
- Re-enable GPU in runtime
- Restart runtime

---

### Final Mental Model

Enable GPU  
→ Install Libraries  
→ Import Libraries  
→ Verify Versions  
→ Ready for Training  
