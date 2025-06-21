
## **2.4 Classical NLP Pipelines**

---

### 🛠️ What Is an NLP Pipeline?

A **Natural Language Processing (NLP) pipeline** is a **step-by-step process** that takes raw text and turns it into something a machine learning model can understand and use.

Think of it like a factory assembly line:

* Text comes in as raw material
* Each step processes or enriches it
* The final product is a clean, structured representation of the original text

These pipelines form the backbone of many real-world NLP tasks like **spam detection**, **sentiment analysis**, **chatbots**, and more.

---

### 🔁 Typical Stages in a Classical NLP Pipeline

Here’s what a basic classical pipeline might look like:

1. **Text Cleaning & Normalization**
2. **Tokenization**
3. **Stemming or Lemmatization**
4. **Stopword Removal**
5. **Part-of-Speech Tagging (optional)**
6. **Vectorization (BoW or TF-IDF)**
7. **Machine Learning Model**

Let’s walk through each step with intuitive explanations and examples.

---

### ✂️ 1. Text Cleaning & Normalization

Before you analyze anything, it helps to clean your data.

Typical cleaning includes:

* Lowercasing all text
  `"Hello" → "hello"`
* Removing punctuation
  `"You're great!" → "youre great"`
* Removing numbers or symbols (optional)

This step ensures consistency across the dataset.

---

### ✨ 2. Tokenization

Splitting text into individual words (or tokens).

```python
from nltk.tokenize import word_tokenize
word_tokenize("I love NLP!") 
# Output: ['I', 'love', 'NLP', '!']
```

These tokens become the units we work with in all future steps.

---

### 🌱 3. Stemming or Lemmatization

Reducing words to a root form:

* `running → run`
* `better → good`

You usually choose **one**, not both.

* Use **stemming** for speed and simplicity
* Use **lemmatization** for better accuracy

---

### 🚫 4. Stopword Removal

Some words are **too common** to be useful, like:

* “the”, “is”, “and”, “of”, “a”

Removing them reduces noise and dimensionality.

```python
from nltk.corpus import stopwords
stopwords.words('english')  # List of common stopwords
```

---

### 🏷️ 5. Part-of-Speech (POS) Tagging (Optional)

Adds grammatical meaning to words—especially useful if you plan to use lemmatization or extract only certain kinds of words (e.g., nouns, verbs).

```python
from nltk import pos_tag
pos_tag(['NLP', 'is', 'awesome'])
# Output: [('NLP', 'NNP'), ('is', 'VBZ'), ('awesome', 'JJ')]
```

---

### 🔢 6. Vectorization (BoW or TF-IDF)

Convert tokens into numerical vectors using methods like:

* **Bag-of-Words**: raw word counts
* **TF-IDF**: weighted importance of words

These vectors become the **features** for machine learning models.

---

### 📊 7. Train a Machine Learning Model

Now you can feed the vectors into algorithms like:

* **Logistic Regression**
* **Naive Bayes**
* **Support Vector Machines**

Your model learns patterns in word usage to make predictions, like:

* Is this email spam?
* Is this review positive or negative?

---

### 🧪 Mini Example: A Classical Pipeline in Code

```python
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.naive_bayes import MultinomialNB

# Step 1: Sample data
texts = [
    "I love this movie",
    "This film was awful",
    "Amazing story and great characters",
    "Terrible plot and boring scenes"
]
labels = [1, 0, 1, 0]  # 1 = Positive, 0 = Negative

# Step 2: Vectorize with TF-IDF
vectorizer = TfidfVectorizer(stop_words='english')
X = vectorizer.fit_transform(texts)

# Step 3: Train a model
model = MultinomialNB()
model.fit(X, labels)

# Step 4: Predict
test = vectorizer.transform(["great film"])
print(model.predict(test))  # Output: [1]
```

> 🧠 This is a basic **sentiment classifier** built entirely from a classical pipeline—no deep learning required!

---

### 🧰 Tools for Pipelines

If you're working with lots of data or want to automate these steps, libraries like **spaCy** and **NLTK** offer prebuilt pipelines.

You can also build custom pipelines using `scikit-learn`'s `Pipeline` class:

```python
from sklearn.pipeline import Pipeline

text_clf = Pipeline([
    ('tfidf', TfidfVectorizer(stop_words='english')),
    ('clf', MultinomialNB())
])
```

This makes the pipeline modular and reproducible.

---

### 🏁 Summary

A classical NLP pipeline:

* Starts with raw text
* Processes and transforms it
* Produces a vector-based representation
* Trains a traditional machine learning model

These pipelines were the **workhorses of NLP** for years—and still remain valuable today in many production systems.

In the next section, we’ll reflect on the **strengths and limitations** of these classical methods, especially compared to modern deep learning approaches.


