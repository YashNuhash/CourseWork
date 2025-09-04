
# 📌 How to Proceed with Step 1 using BanFakeNews-2.0

### **1.1 Dataset Acquisition**

* Download directly from the [ACL Anthology link](https://aclanthology.org/2025.indonlp-1.12/) or GitHub (dataset + baseline code).
* Files you’ll have:

  * `train_cleaned.csv`
  * `val_cleaned.csv`
  * `test_cleaned.csv` (internal)
  * `external_test.csv` (optional, for ablation study)

---

### **1.2 Preprocessing Plan**

Even though the dataset is “cleaned,” you should **standardize further** to make sure it works for your NLP pipeline:

1. **Text Normalization**

   * Normalize Unicode (e.g., remove ZWNJ characters, harmonize Bangla ligatures).
   * Convert multiple spaces → single space.

2. **Lowercasing** (optional for Bangla; but keep case if English words are mixed).

3. **Stopword Removal**

   * Use a Bangla stopword list (BNLP / IndicNLP).
   * Example: remove `যে, এবং, কিন্তু, তাহলে`.

4. **Tokenization**

   * Use **IndicNLP tokenizer** or HuggingFace `bert-base-bengali` tokenizer.

5. **Extra Cleaning**

   * Remove URLs, hashtags, mentions if present.
   * Convert Bangla numerals (০১২৩৪৫৬৭৮৯) to normalized digits if needed.

---

### **1.3 Example Preprocessing Script (Python)**

Here’s a simple script tailored for BanFakeNews-2.0:

```python
import pandas as pd
import re
from bnlp.corpus import stopwords
from bnlp.tokenizer import Tokenizer
from indicnlp.normalize.indic_normalize import IndicNormalizerFactory

# Load dataset
df = pd.read_csv("train_cleaned.csv")

# Bangla normalizer
factory = IndicNormalizerFactory()
normalizer = factory.get_normalizer("bn")

# Bangla tokenizer
tok = Tokenizer()

# Load Bangla stopwords
stop_words = set(stopwords)

def clean_text(text):
    # Normalize Unicode
    text = normalizer.normalize(text)
    
    # Remove URLs, numbers, and symbols
    text = re.sub(r"http\S+|www\S+", "", text)
    text = re.sub(r"[0-9০-৯]+", "", text)
    text = re.sub(r"[^\u0980-\u09FF\s]", "", text)  # keep only Bangla
    
    # Tokenize
    tokens = tok.word_tokenize(text)
    
    # Remove stopwords
    tokens = [t for t in tokens if t not in stop_words]
    
    return " ".join(tokens)

# Apply cleaning
df["cleaned_text"] = df["text"].astype(str).apply(clean_text)

# Save cleaned dataset
df.to_csv("train_processed.csv", index=False)
print(df.head())
```

---

### **1.4 Train-Validation-Test Splits**

* Already provided (70:15:15).
* Just confirm:

  ```python
  print(len(pd.read_csv("train_cleaned.csv")))
  print(len(pd.read_csv("val_cleaned.csv")))
  print(len(pd.read_csv("test_cleaned.csv")))
  ```
* Keep their split for comparability with published results.

---

### **1.5 Output of Step 1**

At the end of Step 1 you’ll have:

* `train_processed.csv`
* `val_processed.csv`
* `test_processed.csv`
* (optionally `external_test_processed.csv`)

Each row:

```csv
text,label,cleaned_text
"বাংলাদেশে আজ একটি বড় ঘটনা ঘটেছে।",1,"বাংলাদেশে আজ বড় ঘটনা ঘটেছে"
```


---

