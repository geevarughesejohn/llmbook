

## 🔍 **Code Example: Using Pretrained Word Embeddings**

Now that you understand how different word embedding models work under the hood, let’s explore how to use **pretrained embeddings** in practice.

We’ll cover:

1. Loading pretrained embeddings using `gensim`
2. Looking up vectors for specific words
3. Measuring word similarity
4. Visualizing embeddings with `t-SNE`
5. (Optional) A tiny sentiment classifier using averaged word vectors

Let’s dive in.

---

### 🧰 Setup

Install the required packages (if you haven’t already):

```bash
pip install gensim nltk matplotlib scikit-learn
```

---

### 📥 1. Load a Pretrained Model

`gensim` provides easy access to many pretrained embeddings. Let’s start with **GloVe**.

```python
import gensim.downloader as api

# Load 100-dimensional GloVe vectors trained on Wikipedia and Gigaword
model = api.load("glove-wiki-gigaword-100")
```

You can also load:

* `"word2vec-google-news-300"` – pretrained Word2Vec model
* `"fasttext-wiki-news-subwords-300"` – FastText with subword info

---

### 🔤 2. Get the Vector for a Word

```python
# Get vector for the word 'apple'
vector = model['apple']
print(vector.shape)  # Should be (100,)
```

This gives you a dense 100-dimensional vector representing “apple.”

---

### 🤝 3. Measure Similarity Between Words

You can find out which words are most similar:

```python
# Top 5 words similar to 'king'
print(model.most_similar('king', topn=5))
```

And try analogies:

```python
# king - man + woman ≈ queen
result = model.most_similar(positive=['woman', 'king'], negative=['man'])
print(result[0])  # Should be close to 'queen'
```

You can also directly compute cosine similarity:

```python
similarity = model.similarity('dog', 'cat')
print(f"Similarity between dog and cat: {similarity:.2f}")
```

---

### 🎨 4. Visualize Word Embeddings with t-SNE

Let’s plot a small set of word vectors in 2D using **t-SNE** from `sklearn`.

```python
import matplotlib.pyplot as plt
from sklearn.manifold import TSNE

# Pick some words to visualize
words = ['king', 'queen', 'man', 'woman', 'dog', 'cat', 'apple', 'banana']
word_vectors = [model[word] for word in words]

# Reduce dimensions to 2D
tsne = TSNE(n_components=2, random_state=0, perplexity=5)
X_2d = tsne.fit_transform(word_vectors)

# Plot
plt.figure(figsize=(8, 6))
for i, word in enumerate(words):
    plt.scatter(X_2d[i, 0], X_2d[i, 1])
    plt.annotate(word, (X_2d[i, 0]+0.5, X_2d[i, 1]+0.5))
plt.title("2D Visualization of Word Embeddings")
plt.show()
```

This produces a nice plot showing **semantic clustering**—e.g., “man” and “woman” near each other, “dog” and “cat” close together.

---

### 🧪 (Optional) Tiny Sentiment Classifier with Averaged Embeddings

Let’s build a simple sentiment classifier using **averaged word vectors** for each sentence.

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score
import numpy as np
import nltk
nltk.download('punkt')
from nltk.tokenize import word_tokenize

# Simple dataset
texts = [
    "I love this movie", "This is terrible", "What a great experience", "I hate it",
    "Absolutely fantastic!", "Worst film ever", "Not bad at all", "Awful, just awful"
]
labels = [1, 0, 1, 0, 1, 0, 1, 0]  # 1 = positive, 0 = negative

# Convert each sentence to an average of its word vectors
def sentence_to_vec(sentence):
    tokens = word_tokenize(sentence.lower())
    vectors = [model[word] for word in tokens if word in model]
    return np.mean(vectors, axis=0) if vectors else np.zeros(model.vector_size)

X = np.array([sentence_to_vec(text) for text in texts])
y = np.array(labels)

# Train/test split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Train classifier
clf = LogisticRegression()
clf.fit(X_train, y_train)

# Evaluate
y_pred = clf.predict(X_test)
print(f"Accuracy: {accuracy_score(y_test, y_pred):.2f}")
```

➡️ You should get a reasonably good accuracy—even with this tiny dataset—just using **pretrained vectors + logistic regression**.

---

### ✅ Summary

In this code section, you learned how to:

* Load pretrained word embeddings (GloVe, Word2Vec, FastText)
* Explore similarity and analogy tasks
* Visualize word meanings with t-SNE
* Use embeddings for a basic NLP classification task

These tools are a powerful way to bring pretrained semantic knowledge into your own NLP workflows—even before jumping into deep neural networks.


