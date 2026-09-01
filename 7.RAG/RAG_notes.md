# RAG (Retrieval-Augmented Generation)

## What is RAG?

---

## In-Context Learning

In-Context Learning is a core capability of Large Language Models (LLMs) like GPT-3/4, Claude, and Llama, where the model learns to solve a task purely by seeing examples in the prompt without updating its weights.

### Example: Sentiment Classification

```text
Below are examples of texts labeled with their sentiment.
Use these examples to determine the sentiment of the final text.

Text: I love this phone. It's so smooth. → Positive
Text: This app crashes a lot. → Negative
Text: The camera is amazing! → Positive
Text: I hate the battery life. → ?
```

The LLM uses the examples provided in the prompt to infer the expected output.

---

## Emergent Property

An **emergent property** is a behaviour or ability that suddenly appears in a system when it reaches a certain scale or complexity even though it was not explicitly programmed or expected from the individual components.

---

## Prompt-Based Examples

### Named Entity Recognition

```text
Label the named entities in the sentences (Person, Location, Organization):

Sentence: Elon Musk founded SpaceX.
Entities: [Elon Musk → Person], [SpaceX → Organization]

Sentence: The Eiffel Tower is in Paris.
Entities: [Eiffel Tower → Location], [Paris → Location]

Sentence: Sundar Pichai leads Google.
Entities: [...]
```

### Step-by-Step Reasoning Example

```text
Solve the math problems step by step:

Q: John has 5 apples. He buys 4 more. How many apples does he have now?
A: John had 3 apples. He bought 4 more. 3 + 4 = 7. → 7

Q: Sarah has 10 pens. She gives away 3. How many does she have left?
A: Sarah had 10 pens. She gave away 3. 10 - 3 = 7. → 7

Q: A pizza is cut into 8 slices. Alex eats 3 slices. How many are left?
A: ...
```

---

# RAG

RAG is a way to make a language model (like ChatGPT) smarter by giving it **extra information at the time you ask your question**.

Instead of relying only on the knowledge stored inside the LLM, RAG retrieves relevant external knowledge and provides it to the model as context.

### Basic Flow

```text
Query + Prompt
       |
       v
      LLM
       |
       v
   Response
```

With RAG:

```text
Query --------------------+
                          |
Context / External -------+--> Prompt --> LLM --> Response
Knowledge Base            |
```

### Why RAG?

RAG is useful when the model needs information that may not be reliably contained in its trained knowledge, such as:

1. **Private data**
2. **Recent developments / recent data**
3. **Reducing hallucinations**

The notes also emphasize that RAG provides the LLM with additional information rather than changing the model's weights.

---

# RAG Pipeline

The RAG workflow consists of four major stages:

1. **Indexing**
2. **Retrieval**
3. **Augmentation**
4. **Generation**

```text
                 RAG
                  |
      +-----------+-----------+
      |                       |
   Indexing               Query Time
                              |
                         Retrieval
                              |
                         Augmentation
                              |
                         Generation
```

---

# 1. Indexing

**Indexing** is the process of preparing your knowledge base so that it can be efficiently searched at query time.

This step consists of **4 sub-steps**:

1. Document Ingestion
2. Text Chunking
3. Embedding Generation
4. Storage in a Vector Store

---

## 1.1 Document Ingestion

**Document Ingestion** is the process of loading your source knowledge into memory.

### Examples

- PDF reports
- Word documents
- YouTube transcripts
- Blog pages
- GitHub repos
- Internal wikis
- SQL records
- Scraped webpages

### Tools

Examples of loaders include:

- `PyPDFLoader`
- `YoutubeLoader`
- `WebBaseLoader`
- `GitLoader`
- Other LangChain loaders

### Flow

```text
Source
  |
  v
Document Loader
  |
  v
Document
```

The notes also illustrate the idea that external knowledge is brought into the RAG pipeline so that it can become context for the LLM.

---

## 1.2 Text Chunking

**Text Chunking** means breaking large documents into small, semantically meaningful chunks.

### Why chunk?

LLMs have context limits (for example, approximately 4K–32K tokens depending on the model).

Smaller chunks are more focused, which can result in better semantic search.

### Tools

Examples mentioned:

- `RecursiveCharacterTextSplitter`
- `MarkdownHeaderTextSplitter`
- `SemanticChunker`

### Flow

```text
Large Document
      |
      v
  Text Splitter
      |
      +------> Chunk 1
      |
      +------> Chunk 2
      |
      +------> Chunk 3
      |
      +------> Chunk 4
```

A transcript or large source document can therefore be divided into multiple smaller pieces before embeddings are generated.

---

# 1.3 Embedding Generation

**Embedding Generation** means converting each chunk into a dense vector (embedding) that captures its meaning.

### Why embeddings?

- Similar ideas land close together in vector space.
- They allow fast, fuzzy semantic search.

### Tools

Examples mentioned:

- `OpenAIEmbeddings`
- `SentenceTransformerEmbeddings`
- `InstructorEmbeddings`

### Flow

```text
Source
  |
  v
Document Loader
  |
  v
Document
  |
  v
Text Splitter
  |
  +------> Chunk 1
  +------> Chunk 2
  +------> Chunk 3
  +------> Chunk 4
               |
               v
        Embedding Model
               |
       +-------+-------+-------+
       |       |       |       |
      V1      V2      V3      V4
```

Each chunk is converted into a vector representation.

For example:

```text
Chunk 1 --> [vector]
Chunk 2 --> [vector]
Chunk 3 --> [vector]
Chunk 4 --> [vector]
```

---

# 1.4 Storage in a Vector Store

The generated vectors are stored along with the **original chunk text + metadata** in a vector database.

### Vector DB options

#### Local

- FAISS
- Chroma

#### Cloud

- Pinecone
- Weaviate
- Milvus
- Qdrant

### Flow

```text
Chunk 1 ----> Embedding ----\
Chunk 2 ----> Embedding -----\
Chunk 3 ----> Embedding ------> Vector Store
Chunk 4 ----> Embedding -----/
```

The vector store becomes the searchable representation of the external knowledge base.

---

# 2. Retrieval

**Retrieval** is the real-time process of finding the most relevant pieces of information from a pre-built index (created during indexing) based on the user's question.

In simple terms, retrieval asks:

> "From all the knowledge I have, which 3–5 chunks are most helpful to answer this query?"

### Retrieval Flow

```text
User Query
    |
    v
 Retriever
    |
    v
Semantic Search
    |
    v
Vector Store
    |
    v
Most Relevant Chunks
(Context)
```

The notes show that the query is used to perform a semantic search against the vector store and return the most relevant chunks.

### Conceptual Steps

```text
Step 1 --> Query
Step 2 --> Semantic search
Step 3 --> Ranking
Step 4 --> Select relevant chunks
```

The retrieved chunks become the **context** that will be passed to the LLM.

---

# 3. Augmentation

**Augmentation** refers to the step where the retrieved documents (chunks of relevant context) are combined with the user's query to form a new, enriched prompt for the LLM.

### Flow

```text
Most Relevant Chunks (Context)
              +
            Query
              |
              v
            Prompt
```

The prompt now contains both:

- The user's question
- Relevant information retrieved from the external knowledge base

### Example Prompt

```text
"""You are a helpful assistant.
Answer the question ONLY from the provided context.
If the context is insufficient, just say you don't know.

{context}

Question: {question}"""
```

This instruction helps constrain the answer to the retrieved context.

---

# 4. Generation

**Generation** is the final step where a Large Language Model (LLM) uses the user's query and the retrieved & augmented context to generate a response.

### Complete RAG Flow

```text
                         INDEXING
                            |
                            v
Source --> Document Loader --> Text Splitter
                                  |
                                  v
                           Chunks of Text
                                  |
                                  v
                           Embedding Model
                                  |
                                  v
                             Vector Store
                                  |
                            Semantic Search
                                  |
                                  v
QUERY ----------------------> Retriever
                                  |
                                  v
                        Most Relevant Chunks
                              (Context)
                                  |
                                  +--------+
                                           |
QUERY -------------------------------------+
                                           |
                                           v
                                         Prompt
                                           |
                                           v
                                          LLM
                                           |
                                           v
                                        Response
```

---

# Complete RAG Architecture

```text
                     EXTERNAL KNOWLEDGE BASE
                              |
                              v
                       Document Loader
                              |
                              v
                         Text Splitter
                              |
                  +-----------+-----------+
                  |           |           |
                Chunk 1     Chunk 2     Chunk 3 ...
                  |           |           |
                  +-----------+-----------+
                              |
                              v
                       Embedding Model
                              |
                              v
                         Vector Store
                              |
                       Semantic Search
                              ^
                              |
Query -----------------> Retriever
                              |
                              v
                    Most Relevant Chunks
                         (Context)
                              |
                              +------+
                                     |
Query -------------------------------+
                                     |
                                     v
                                   Prompt
                                     |
                                     v
                                    LLM
                                     |
                                     v
                                  Response
```

---

# RAG vs. In-Context Learning

## In-Context Learning

In-context learning gives examples or information directly inside the prompt.

```text
Examples / Information
          +
        Query
          |
          v
        Prompt
          |
          v
         LLM
          |
          v
       Response
```

The model learns how to perform the task from the examples in the prompt **without updating its weights**.

## RAG

RAG dynamically retrieves relevant information from an external knowledge base.

```text
             External Knowledge
                    |
                    v
              Vector Store
                    |
Query --> Retriever
                    |
                    v
            Relevant Context
                    |
Query + Context --> Prompt
                    |
                    v
                   LLM
                    |
                    v
                Response
```

---

# Key Ideas from the Notes

## 1. LLM Knowledge vs. External Knowledge

An LLM has knowledge encoded in its parameters/weights.

RAG adds an **external knowledge base** that can be searched at query time.

```text
LLM
 |
 +--> Internal / learned knowledge
 |
 +--> RAG --> External knowledge base
```

## 2. RAG Adds Context

The basic idea is:

```text
Query + Retrieved Context
          |
          v
        Prompt
          |
          v
         LLM
          |
          v
       Response
```

The retrieved information gives the model additional context for answering the question.

## 3. Private Data

RAG can be used to provide an LLM with access to private or organization-specific information without putting all of that information into the model's weights.

Examples include:

- Internal documents
- Private reports
- Internal wikis
- Company data
- Other organization-specific knowledge

## 4. Recent Data

RAG can retrieve newer information from an external knowledge base, helping the application work with recent developments or data.

## 5. Hallucinations

The notes identify reducing **hallucinations** as one of the motivations for using RAG.

A prompt can explicitly constrain the model:

```text
You are a helpful assistant.
Answer the question ONLY from the provided context.
If the context is insufficient, just say you don't know.

{context}

Question: {question}
```

---

# RAG in One Line

> **RAG = Retrieve relevant external information + Augment the prompt with that information + Generate an answer using an LLM.**

---

# Summary of the 4 Stages

| Stage | What happens |
|---|---|
| **Indexing** | Prepare the knowledge base for efficient search |
| **Retrieval** | Find the most relevant chunks for the user's query |
| **Augmentation** | Combine retrieved context with the user's query |
| **Generation** | LLM uses the query and augmented context to generate the response |

### Indexing

```text
Documents
   ↓
Ingestion
   ↓
Chunking
   ↓
Embeddings
   ↓
Vector Store
```

### Query Time

```text
Query
  ↓
Retrieval
  ↓
Relevant Chunks
  ↓
Augmentation
  ↓
Prompt
  ↓
LLM
  ↓
Response
```

---

# Notes / Visual Annotations Captured from the PDF

The handwritten annotations reinforce the following ideas:

- RAG supplies **external knowledge/context** to an LLM.
- The knowledge can be thought of as a separate knowledge base rather than knowledge permanently encoded in the model.
- The retrieved chunks are used to create an enriched prompt.
- Semantic search is used during retrieval.
- The vector store contains the embeddings associated with document chunks.
- The final LLM response is generated from the query together with the retrieved context.
- RAG is particularly useful for **private data**, **recent developments/data**, and **hallucination reduction**.
- The notes also contrast prompt-based learning with approaches such as fine-tuning and supervised learning.

---

# End-to-End Example

Suppose an organization has a large collection of internal documents.

### Step 1 — Ingest

```text
Internal PDFs
     ↓
Document Loader
```

### Step 2 — Chunk

```text
Documents
     ↓
Text Splitter
     ↓
Small semantic chunks
```

### Step 3 — Embed

```text
Chunks
  ↓
Embedding Model
  ↓
Vectors
```

### Step 4 — Store

```text
Vectors + Original Text + Metadata
              ↓
         Vector Store
```

### Step 5 — Query

```text
User:
"What is our company's leave policy?"
```

### Step 6 — Retrieve

```text
Query
  ↓
Semantic Search
  ↓
Vector Store
  ↓
Most Relevant Chunks
```

### Step 7 — Augment

```text
Relevant Chunks
      +
User Question
      ↓
Enriched Prompt
```

### Step 8 — Generate

```text
Enriched Prompt
      ↓
     LLM
      ↓
Answer based on retrieved context
```

---

# Final Mental Model

Think of RAG as giving an LLM an **external memory/search system**:

```text
                         +----------------------+
                         | External Knowledge   |
                         |      Base            |
                         +----------+-----------+
                                    |
                                    v
                             +-------------+
                             | Vector      |
                             | Store       |
                             +------+------+
                                    ^
                                    |
                              Semantic Search
                                    |
User Query ----------------> Retriever
                                    |
                                    v
                           Relevant Context
                                    |
                                    +------+
                                           |
User Query --------------------------------+
                                           |
                                           v
                                      +---------+
                                      | Prompt  |
                                      +----+----+
                                           |
                                           v
                                      +---------+
                                      |   LLM   |
                                      +----+----+
                                           |
                                           v
                                      +---------+
                                      |Response |
                                      +---------+
```

**Core idea:**

> The LLM does not need to contain every piece of information in its weights. RAG lets it retrieve relevant information from an external knowledge base at query time, put that information into the prompt as context, and then generate a response using that context.
