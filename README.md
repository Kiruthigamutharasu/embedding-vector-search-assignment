# Assignment 22: Embedding Models, Vector Stores & Similarity Search

## Overview

In this assignment, I built a **Personal Knowledge Search Engine** using embedding models and vector databases.

The goal was to convert documents into embeddings and perform **semantic similarity search** to retrieve the most relevant information.

This assignment demonstrates the **core retrieval foundation used in Retrieval Augmented Generation (RAG) systems**.

---

# Project Structure
embedding-vector-search/

│
├── notebook.ipynb # Main assignment notebook
├── README.md # Project documentation
├── requirements.txt # Python dependencies
├── .env # OpenAI API key
│
├── data/ # Sample documents
│ ├── ai.txt
│ ├── llm.txt
│ ├── ml.txt
│ ├── rag.txt
│ ├── vector_db.txt
│
├── faiss_index/ # Saved FAISS vector index
├── chroma_db/ # Chroma persistent vector database


---

# Embedding Models Used

### 1. OpenAI Embeddings
Model used:
text-embedding-3-small


Used for generating high-quality embeddings through the OpenAI API.

Observations:
- Embedding vector size: **1536**
- Fast API response
- Requires internet and API key

---

### 2. HuggingFace Embeddings

Model used:
sentence-transformers/all-MiniLM-L6-v2


Observations:
- Runs locally
- Embedding dimension: **384**
- Slightly slower on CPU compared to OpenAI

---

### 3. Ollama Embeddings

Model used:
nomic-embed-text


Observations:
- Fully local embedding model
- Useful for privacy-sensitive data
- Requires Ollama installed locally

---

# Vector Databases Used

### FAISS

FAISS was used for fast similarity search.

Features:
- In-memory vector index
- Extremely fast search performance
- Index saved locally for reuse

---

### ChromaDB

ChromaDB was used as a persistent vector store.

Features:
- Stores embeddings on disk
- Easy integration with LangChain
- Useful for production pipelines

---

# Similarity Search Implementation

Two approaches were implemented:

### 1. Manual Similarity Search
- Convert document chunks to embeddings
- Compute similarity scores
- Return top-k results

### 2. LangChain Vector Store Search

Using:
vectorstore.similarity_search(query)


This simplifies retrieval using vector database abstraction.


The pipeline supports **switchable embedding backends**:

- OpenAI
- HuggingFace
- Ollama

And **switchable vector stores**:

- FAISS
- ChromaDB

---

# Observations & Learning

### Importance of Embeddings in GenAI

Embeddings convert text into numerical vectors that capture semantic meaning.  
This allows machines to compare text based on meaning rather than exact words.

---

### Why Vector Databases Are Needed

Traditional databases cannot efficiently perform similarity search on high-dimensional vectors.

Vector databases like FAISS and ChromaDB enable fast semantic search across large document collections.

---

### How This Pipeline Enables RAG

The pipeline retrieves relevant documents before passing them to a language model.

This retrieval step is the **core idea behind Retrieval Augmented Generation (RAG)**.

---

# Challenges Faced

### 1. Dataset Too Small

Initially my dataset produced only **one chunk**, which caused similarity search to fail.

To fix this I expanded the dataset into multiple documents to generate enough chunks for meaningful retrieval.

---

### 2. OpenAI API Setup

I initially faced issues loading the OpenAI API key.  
This was resolved by creating a `.env` file and loading it using `python-dotenv`.

---

### 3. Understanding Vector Stores

It took some experimentation to understand the difference between **FAISS (in-memory)** and **ChromaDB (persistent storage)**.

Testing both helped me understand when each one should be used.

---

### 4. Embedding Model Comparison

Comparing OpenAI, HuggingFace, and Ollama embeddings required benchmarking speed and understanding embedding dimensions.

This helped me understand the **trade-off between cost, speed, and local deployment**.

---

# Installation

Create virtual environment
python3.11 -m venv venv
Activate environment

Windows

venv\Scripts\activate

pip install -r requirements.txt


---

# Setup OpenAI API Key

Create `.env` file


OPENAI_API_KEY=your_api_key_here


---

# Running the Notebook

Start Jupyter Notebook


jupyter notebook


Open:


notebook.ipynb


Run all cells sequentially.

---

# Technologies Used

- Python 3.11
- LangChain
- OpenAI Embeddings
- HuggingFace Sentence Transformers
- Ollama
- FAISS
- ChromaDB