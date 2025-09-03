
# Student Course Q\&A Chatbot (RAG)

A Retrieval-Augmented Generation (RAG) chatbot designed for university students. For now, it’s loaded with a document describing each course, and it answers questions by retrieving the most relevant course snippets and grounding the response on them.

## What it does

- Splits the course document into chunks, creates embeddings, and caches both chunks and embeddings for faster runs.
- Uses vector search to retrieve the top‑k relevant chunks and feeds them as context to a chat model to generate grounded answers for student queries.


## Current data

- Knowledge base: a single document with course descriptions (e.g., objectives, content) intended to help students explore and compare courses.


## Chunking strategies

- Fixed-size: character-length windows (fast, may break sentences).
- Recursive: hierarchical splitting by separators to respect a target size.
- Page-based: per page for PDFs; HTML/TXT fallbacks supported.
- Sentence-based: groups n consecutive sentences (default in the main script).
- Semantic: merges sentences using embedding similarity and a threshold.
- Agentic: an LLM segments text into task-oriented chunks (student Q\&A).
- Overlapping variants: preserve context across adjacent chunks.


## Retrieval

- Embeddings are indexed with FAISS (IndexFlatL2) for exact L2 nearest-neighbor search; answers use the top‑k retrieved chunks as context (k=4 by default).


## How to use

- Set the API key via environment variable and point the script to the course document file path; run once to build caches, then query with student questions (e.g., “What are the learning objectives for Economics-Management?”).
