# llama-index-project

This repository documents key **LlamaIndex indices** and **retrievers** used for building retrieval-augmented generation (RAG) systems.

## LlamaIndex Indices

### 1. `KeywordTableIndex`
- Builds an index around extracted keywords from documents.
- Useful for exact or keyword-driven matching.
- Lightweight and helpful when semantic embeddings are not required.

### 2. `DocumentSummaryIndex`
- Stores higher-level summaries of each document.
- Best for quickly narrowing down relevant documents before deep retrieval.
- Pairs naturally with summary-based retrievers.

### 3. `VectorStoreIndex`
- Converts chunks into vector embeddings and stores them in a vector store.
- Enables semantic search based on meaning instead of exact word overlap.
- Most common index for modern RAG pipelines.

## Retriever Types

### 1. `VectorStoreIndex` Retrievers
- Retrieve nearest chunks/documents from vector similarity search.
- Good for semantic relevance and paraphrased queries.

### 2. BM25 Retrievers
- Sparse retrieval based on term frequency and inverse document frequency.
- Strong baseline for lexical matching and keyword-heavy questions.

### 3. `DocumentSummaryRetriever` Family

#### a) `DocumentSummaryLLMRetriever`
- Uses LLM reasoning over summaries to select relevant documents.
- Useful when relevance depends on high-level document meaning.

#### b) `DocumentSummaryEmbeddingRetriever`
- Uses embeddings of document summaries for semantic retrieval at summary level.
- Faster than full-document semantic retrieval in many setups.

## `QueryFusionRetriever`

`QueryFusionRetriever` combines results from multiple retrievers and fuses them into one ranked list for better recall and robustness.

### Fusion Strategies

#### 1) Reciprocal Rank Fusion (RRF)
- Combines rank positions from multiple retrievers.
- Rewards items that appear consistently across retrieval methods.

#### 2) Relative Score Fusion
- Normalizes and combines similarity/relevance scores across retrievers.
- Helps merge outputs when retrievers produce different score ranges.

#### 3) Distribution Score Fusion
- Fuses results based on the score distribution of each retriever.
- Useful when calibrating across heterogeneous retrieval systems.