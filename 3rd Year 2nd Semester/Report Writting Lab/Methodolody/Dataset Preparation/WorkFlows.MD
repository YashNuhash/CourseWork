
---

# 🚀 Workflow to Fine-Tune & Publish BanglaBERT

### **Step 1: Prepare Dataset**

* Use **BanFakeNews-2.0** (CSV files with `text`, `label` columns).
* Preprocess (normalize, clean, tokenize).
* Split into `train`, `validation`, `test`.

---

### **Step 2: Train Model (Google Colab or Kaggle)**

* Use Hugging Face `transformers` and `datasets`.
* Fine-tune `sagorsarker/banglabert_base` (BanglaBERT).
* Save the trained weights.

Example (Colab code snippet):

```python
from transformers import AutoTokenizer, AutoModelForSequenceClassification, Trainer, TrainingArguments
from datasets import load_dataset

model_name = "sagorsarker/banglabert_base"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForSequenceClassification.from_pretrained(model_name, num_labels=2)

# Load BanFakeNews dataset
dataset = load_dataset("csv", data_files={
    "train": "train.csv",
    "validation": "val.csv",
    "test": "test.csv"
})

# Tokenization
def tokenize(batch):
    return tokenizer(batch["text"], padding="max_length", truncation=True)

dataset = dataset.map(tokenize, batched=True)

# Training setup
training_args = TrainingArguments(
    output_dir="./results",
    evaluation_strategy="epoch",
    save_strategy="epoch",
    learning_rate=2e-5,
    per_device_train_batch_size=16,
    per_device_eval_batch_size=16,
    num_train_epochs=3,
    weight_decay=0.01,
    logging_dir="./logs",
    push_to_hub=True   # 🔑 enables model upload to Hugging Face
)

trainer = Trainer(
    model=model,
    args=training_args,
    train_dataset=dataset["train"],
    eval_dataset=dataset["validation"],
    tokenizer=tokenizer
)

trainer.train()
```

---

### **Step 3: Push Model to Hugging Face Hub**

1. Create a free Hugging Face account → [huggingface.co](https://huggingface.co)
2. Log in from Colab:

```python
from huggingface_hub import notebook_login
notebook_login()
```

3. After training finishes:

```python
trainer.push_to_hub("BanglaBERT-FakeNews-Detection")
tokenizer.push_to_hub("BanglaBERT-FakeNews-Detection")
```

This uploads the model + tokenizer to your Hugging Face repo 🎉

---

### **Step 4: Publish Inference Demo**

* Create a **Hugging Face Space** with **Gradio** or **Streamlit** UI.
* Example Gradio code (`app.py`):

```python
import gradio as gr
from transformers import pipeline

pipe = pipeline("text-classification", model="your-username/BanglaBERT-FakeNews-Detection")

def predict(text):
    result = pipe(text)[0]
    label = "Fake News" if result['label'] == "LABEL_1" else "Real News"
    return f"Prediction: {label} (Confidence: {result['score']:.2f})"

iface = gr.Interface(fn=predict, inputs="text", outputs="text", title="Bangla Fake News Detector")
iface.launch()
```

* Deploy this inside Hugging Face **Spaces** → your model becomes **publicly usable as a web app**.

---

✅ At the end, you’ll have:

1. **Fine-tuned BanglaBERT model** on Hugging Face Hub.
2. **A public demo app** where anyone can paste Bangla news text and get Fake/Real prediction.
3. A **DOI link** (Hugging Face provides one) to cite in your paper.

---

