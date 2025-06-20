
# **Chapter 3: Word Embeddings and Dense Representations**

---

## **🎯 Learning Objectives**

By the end of this chapter, the reader will be able to:

* Understand what **word embeddings** are and why they matter.
* See how embeddings solve the limitations of sparse representations like TF-IDF.
* Explore how models like **Word2Vec**, **GloVe**, and **FastText** learn embeddings.
* Visualize word relationships in vector space.
* Use pre-trained embeddings in code and analyze their structure.
* Recognize the limitations of static embeddings, and understand why **contextual representations** (like BERT or GPT) are needed.

---

## **📚 Chapter Sections**

---

### **3.1 Introduction: From Counting to Understanding**

* Reflect on the limitations of Bag-of-Words and TF-IDF: sparsity, lack of meaning.
* Introduce the need for dense, semantic representations.
* Build the intuitive idea that **words appearing in similar contexts tend to have similar meanings**.
* Set the stage for the chapter.

---

### **3.2 What Are Word Embeddings?**

* Introduce **word embeddings** formally and intuitively.
* Explain that a word is represented as a **dense vector** of real numbers (e.g., 100–300 dimensions).
* Discuss properties like **semantic similarity**, **vector closeness**, and **continuous representation**.
* Use simple analogies (e.g., “words on a map”) to make it visual and relatable.

---

### **3.3 How Embeddings Capture Meaning**

* Explain how embeddings are learned from large corpora through co-occurrence and context.
* Discuss the **distributional hypothesis** (“You shall know a word by the company it keeps”).
* Show how embedding spaces reflect relationships:

  * Clustering: animals, countries, emotions
  * Analogies: `king – man + woman ≈ queen`
* Use visualizations (t-SNE or PCA) and diagrams to show word groupings.

---

### **3.4 Word2Vec: Learning Embeddings from Context**

* Introduce **Word2Vec**, its origin (Google, 2013), and significance.
* Explain the **two training strategies**:

  * **CBOW**: predict a word from its context
  * **Skip-gram**: predict the context from a word
* Dive into the **architecture and training logic** (without heavy math).
* Explain the role of context window, negative sampling, and why Word2Vec is unsupervised.

---

### **3.5 GloVe: Global Vectors from Co-occurrence**

* Explain the motivation behind GloVe (Stanford, 2014).
* Compare to Word2Vec:

  * Word2Vec: predictive, local
  * GloVe: count-based, global
* Describe how GloVe uses a **co-occurrence matrix** and learns embeddings by factorizing it.
* Show how it balances frequency with meaning.

---

### **3.6 FastText: Going Beyond Words**

* Present the key innovation: **subword embeddings** using character n-grams.
* Explain how this helps:

  * Represent rare or misspelled words
  * Capture morphological structure (e.g., “run”, “running”, “runner”)
* Discuss FastText’s use in multilingual and noisy datasets.

---

### **3.7 Working with Pretrained Embeddings (Code + Case Study)**

* Introduce real-world usage of embeddings.
* Use `gensim` or HuggingFace to:

  * Load pre-trained Word2Vec, GloVe, or FastText models
  * Retrieve vectors
  * Compute similarity
  * Visualize clusters with PCA or t-SNE
* Build a simple classifier (e.g., sentiment analysis) using averaged word vectors.

---

### **3.8 Limitations of Word Embeddings**

* Discuss problems that embeddings don’t solve:

  * **Context insensitivity**: same vector for “bank” in different meanings
  * **Static nature**: embeddings don’t change based on sentence
  * **Out-of-vocabulary (OOV)**: unknown words = no vector
* Use real examples to show failure cases.

---

### **3.9 From Static to Contextual: The Next Step**

* Set up the transition to contextual embeddings (Chapter 4).
* Briefly introduce the idea behind **ELMo**, **BERT**, and **GPT**:

  * Vectors now depend on sentence context
  * Meaning is dynamic, not fixed
* End with a teaser: **“How does a model know what 'Java' means in different sentences? That’s the magic of contextual embeddings.”**


