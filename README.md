# 🚀 Generative AI & Agentic AI Workshop

<p align="center">
  <img src="assets/workshop-poster.png" alt="Generative AI & Agentic AI Workshop" width="850"/>
</p>

<h3 align="center">From Python & LangChain Fundamentals to RAG, Tools and AI Agents</h3>

<p align="center">
  A hands-on learning repository covering LangChain, prompts, structured outputs, output parsers, chains, LCEL/Runnables, RAG, tools, tool calling, and AI agents.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/LangChain-current-green?logo=chainlink&logoColor=white" alt="LangChain"/>
  <img src="https://img.shields.io/badge/LangGraph-included-orange" alt="LangGraph"/>
  <img src="https://img.shields.io/badge/Streamlit-enabled-red?logo=streamlit&logoColor=white" alt="Streamlit"/>
</p>

---

## 🎓 About the Workshop

This repository contains the notebooks, Python applications, notes, datasets, documents, and supporting material used for the **Generative AI & Agentic AI Workshop** organized by the **Society of Engineering Students, Far Western University, School of Engineering, Mahendranagar, Kanchanpur**.

The material follows a practical progression:

```text
Prerequisites
     ↓
LangChain Introduction
     ↓
LLM Responses + Embeddings
     ↓
Prompts + Messages
     ↓
Structured Outputs
     ↓
Output Parsers
     ↓
Chains
     ↓
Runnables / LCEL
     ↓
Document Loading + Text Splitting
     ↓
Vector Stores + Retrievers
     ↓
RAG
     ↓
Tools + Tool Calling
     ↓
AI Agents
```

The README structure below has been written from the **actual repository tree and the contents of the notebooks/files currently present in the repository**.

---

## 📁 Actual Repository Structure

```text
GenAI-Langchain-Workshop/
│
├── Prerequisites/
│   ├── 1.python_basics.ipynb
│   └── 2.enviroment_setup.ipynb
│
├── 1.introduction-to-langchain.ipynb
│
├── 1.Basics/
│   ├── 1.simple_response.ipynb
│   └── 2.embedding.ipynb
│
├── 2.prompts/
│   ├── 1_static_prompt.py
│   ├── 2_dynamic_prompt.py
│   ├── 3.chatbot.ipynb
│   ├── 4.messages.ipynb
│   ├── 5.chatprompt_template.ipynb
│   ├── 6.message_placeholder.ipynb
│   └── chathistory.txt
│
├── 3.structured-outputs/
│   ├── 1.typed_dict.ipynb
│   ├── 2.pydantic.ipynb
│   ├── 3.json_.ipynb
│   └── 4.when_to_use_what.ipynb
│
├── 4.Output-Parsers/
│   ├── 1.StrOutputParser.ipynb
│   ├── 2.JsonOutputParser.ipynb
│   ├── 3.Structured_Output_Parser.ipynb
│   └── 4.Pydantic_Output_Parser.ipynb
│
├── 5.Chains/
│   ├── 1.linear_chains.ipynb
│   ├── 2.parallel_chains.ipynb
│   └── 3.conditional_chains.ipynb
│
├── 6.Runnables/
│   ├── 1.how.ipynb
│   ├── 2.runnables.ipynb
│   └── Runnables_in_LangChain.md
│
├── 7.RAG/
│   ├── 1.document_loaders.ipynb
│   ├── 2.textSplitters.ipynb
│   ├── 3.vector_stores.ipynb
│   ├── 4.retrivers.ipynb
│   ├── youtube_chatbot.ipynb
│   ├── RAG_notes.md
│   ├── Rag need.pdf
│   ├── cricket.txt
│   ├── dl-curriculum.pdf
│   └── books/
│       └── Building Machine Learning Systems with Python - Second Edition.pdf
│
├── 8.Agents/
│   ├── 1.tools.ipynb
│   ├── 2.tool_calling.ipynb
│   ├── 3.langchain_agents.ipynb
│   └── 4.agents_langchain.ipynb
│
├── assets/
│   └── workshop-poster.png
│
├── genai_Notes.pdf
├── requirements.txt
├── .gitignore
└── README.md
```

---

# 📚 Detailed Repository Guide

## 0. `Prerequisites/` — Python & Environment Setup

This folder prepares learners for the rest of the workshop.

### `1.python_basics.ipynb`

A Python fundamentals notebook covering the programming concepts needed for the later LangChain exercises.

Topics include:

- First Python program
- `print()`
- Comments
- Variables
- Dynamic typing
- Variable naming rules
- Data types
- Strings
- f-strings
- Input and output
- Type conversion

### `2.enviroment_setup.ipynb`

Walks through setting up the development environment for the workshop.

It covers:

- Creating a Python virtual environment
- Activating environments on Windows PowerShell
- Windows Command Prompt
- macOS/Linux activation
- Upgrading `pip`
- Installing LangChain packages
- Installing vector-database dependencies
- Creating a `.env` file
- Configuring an OpenRouter API key
- Adding `.env` to `.gitignore`
- Loading environment variables
- Initializing `ChatOpenAI` with an OpenRouter base URL

> The repository uses environment variables for API credentials. API keys should never be committed to GitHub.

---

# 1. `1.introduction-to-langchain.ipynb` — Introduction to LangChain

This notebook provides the conceptual foundation for the entire workshop.

It explains LangChain as a framework for building applications around LLMs and introduces its major building blocks:

- Models
- Prompt templates
- Output parsers
- Chains
- Agents
- Vector stores
- Memory / conversation history
- Tools
- APIs
- Retrievers
- Workflows

It also explains how these components can be connected to turn a basic model call into a complete LLM application.

---

# 2. `1.Basics/` — LLM Responses & Embeddings

## `1.simple_response.ipynb`

Introduces direct interaction with an OpenAI chat model through LangChain.

The notebook demonstrates:

- Loading environment variables
- Creating `ChatOpenAI`
- Invoking a model with a text prompt
- Selecting a model such as `gpt-4o-mini`
- Experimenting with the `temperature` parameter
- Observing how temperature changes response variation

Example progression:

```text
Prompt
  ↓
ChatOpenAI
  ↓
Model Response
```

The notebook also experiments with different temperatures while generating text.

## `2.embedding.ipynb`

Introduces **text embeddings**.

It demonstrates:

- Creating `OpenAIEmbeddings`
- Embedding a single query with `embed_query()`
- Embedding multiple documents with `embed_documents()`
- Comparing query and document embeddings
- Using embeddings for semantic similarity

The examples use questions about Nepal and cricket-related documents to illustrate how text is converted into numerical vectors.

Conceptually:

```text
Text
 ↓
Embedding Model
 ↓
Vector Representation
 ↓
Similarity Comparison
```

This becomes the foundation for the vector-store and RAG sections later in the repository.

---

# 3. `2.prompts/` — Prompts, Chatbots & Message Handling

This folder moves from raw model calls toward reusable prompt-driven applications.

## `1_static_prompt.py`

A small Streamlit research tool.

It provides:

- A text input
- A `Summarize` button
- A `ChatOpenAI` model
- Direct invocation of the user's prompt
- Display of the generated response

It demonstrates the simplest form of turning an LLM call into a small UI application.

## `2_dynamic_prompt.py`

A Streamlit application demonstrating **dynamic prompt construction**.

The user selects:

- Research paper
- Explanation style
- Explanation length

A `PromptTemplate` combines those values into a model-ready prompt.

Flow:

```text
User Selections
      ↓
PromptTemplate
      ↓
Formatted Prompt
      ↓
ChatOpenAI
      ↓
Explanation
```

## `3.chatbot.ipynb`

Introduces a simple terminal chatbot and then begins adding conversation history.

The notebook demonstrates:

- A continuous input loop
- Exit handling
- Calling the chat model repeatedly
- Maintaining a `chat_history` collection

This introduces the need for explicit conversation state.

## `4.messages.ipynb`

Introduces LangChain's message objects:

- `SystemMessage`
- `HumanMessage`
- `AIMessage`

The notebook builds a message list and sends the conversation to the model.

Conceptually:

```text
System Instructions
       +
Human Message
       +
AI Response
       ↓
Conversation State
```

## `5.chatprompt_template.ipynb`

Introduces `ChatPromptTemplate`.

The template contains:

- A system message with a dynamic `domain`
- A human message with a dynamic `topic`

The example shows how one reusable chat template can produce prompts for different domains and topics.

## `6.message_placeholder.ipynb`

Introduces `MessagesPlaceholder` for injecting existing conversation history into a chat prompt.

The notebook loads sample history from `chathistory.txt` and inserts it into a customer-support prompt.

Flow:

```text
Saved Chat History
       ↓
MessagesPlaceholder
       ↓
ChatPromptTemplate
       ↓
Current User Query
       ↓
Model
```

## `chathistory.txt`

Contains a small example conversation consisting of a human refund request and an AI response.

It serves as sample history for the `MessagesPlaceholder` example.

---

# 4. `3.structured-outputs/` — Reliable Structured Model Responses

This section explores how LLM responses can be constrained into predictable structures.

## `1.typed_dict.ipynb`

Introduces Python's `TypedDict` and LangChain's structured-output support.

The notebook covers:

- Defining schemas with `TypedDict`
- Required fields
- `Annotated` descriptions
- Optional fields
- Literal values
- Using `with_structured_output()`
- Sentiment-analysis examples

The notebook also discusses an important limitation: `TypedDict` describes the expected structure but does not provide the same runtime validation capabilities as Pydantic.

## `2.pydantic.ipynb`

Introduces Pydantic models for structured and validated data.

It demonstrates:

- `BaseModel`
- Default values
- Optional fields
- Type conversion/coercion
- `EmailStr`
- Field descriptions
- Validation
- Structured LLM output

The notebook uses sentiment-analysis examples and explains why Pydantic is useful when validation is important.

## `3.json_.ipynb`

Introduces **JSON Schema** as a language-independent way to describe structured output.

It demonstrates JSON schema concepts such as:

- Object schemas
- Properties
- String fields
- Integer fields
- Structured model responses

This provides a bridge from Python-specific structures to a universal JSON representation.

## `4.when_to_use_what.ipynb`

Compares the three approaches:

| Approach | Main Use |
| --- | --- |
| `TypedDict` | Lightweight Python type/schema description |
| `Pydantic` | Python-side validation and structured data |
| `JSON Schema` | Language-independent schema representation |

The notebook provides a practical decision guide for choosing between them.

---

# 5. `4.Output-Parsers/` — Converting Model Output

This section focuses on output parsers and how they transform model responses into usable application data.

## `1.StrOutputParser.ipynb`

Introduces `StrOutputParser`.

The notebook builds a multi-step chain:

```text
Prompt
 ↓
LLM
 ↓
String Parser
 ↓
Second Prompt
 ↓
LLM
 ↓
String Parser
```

The example first generates research about a topic and then asks the model to summarize that research.

## `2.JsonOutputParser.ipynb`

Introduces `JsonOutputParser`.

It demonstrates:

- Requesting JSON-formatted output
- Generating format instructions
- Passing those instructions into a prompt
- Parsing the result into Python data

The notebook also notes the limitation that JSON formatting alone does not enforce a strict schema.

## `3.Structured_Output_Parser.ipynb`

Introduces:

- `StructuredOutputParser`
- `ResponseSchema`
- Multiple named response fields
- Format instructions
- Parsing structured model output

The example requests multiple facts about a batsman and converts the response into a structured result.

## `4.Pydantic_Output_Parser.ipynb`

Introduces `PydanticOutputParser`.

It demonstrates:

- Defining a Pydantic model
- Creating format instructions
- Manually invoking the model/parser
- Integrating the parser into a chain
- Validating structured output

The example defines fields such as a person's name, age, and country and uses validation constraints.

---

# 6. `5.Chains/` — Composing LangChain Components

This folder introduces increasingly flexible chains.

## `1.linear_chains.ipynb`

Introduces a **sequential/linear chain**.

The example:

1. Generates a detailed cricket-career report.
2. Passes that report to another prompt.
3. Generates interesting facts from the report.

Flow:

```text
Prompt 1 → LLM → Parser
                    ↓
                Prompt 2
                    ↓
                  LLM
                    ↓
                 Parser
```

## `2.parallel_chains.ipynb`

Introduces **parallel execution** with `RunnableParallel`.

The notebook processes the same input through multiple branches, including:

- Summary generation
- Quiz-question generation

The outputs are then combined into a final response.

```text
                    ┌──→ Summary ──┐
Input ──────────────┤              ├──→ Final Output
                    └──→ Quiz ─────┘
```

## `3.conditional_chains.ipynb`

Introduces conditional chain execution.

The example:

1. Uses a Pydantic schema to classify review sentiment.
2. Routes the review according to the sentiment.
3. Uses a different prompt for the resulting path.

Conceptually:

```text
Review
  ↓
Sentiment Classifier
  ↓
 ┌───────────────┐
 │               │
Positive       Negative
 │               │
 ↓               ↓
Reply A        Reply B
```

This establishes the idea of dynamic routing.

---

# 7. `6.Runnables/` — LangChain's Composable Architecture

## `1.how.ipynb`

This notebook explains **why Runnables were introduced**.

It first recreates a simplified pre-Runnable architecture using custom classes such as:

- A mock prompt template
- A mock LLM
- A mock chain

It then explains the problems of specialized chain abstractions and the need for a standardized interface.

The central idea is:

```text
Different Components
        ↓
Common Interface
        ↓
invoke()
        ↓
Composable Workflows
```

The notebook uses the LEGO-block analogy to explain how components can be connected into larger workflows.

## `2.runnables.ipynb`

Provides hands-on examples of the major Runnable abstractions:

- `RunnableSequence`
- `RunnableParallel`
- `RunnablePassthrough`
- `RunnableLambda`
- `RunnableBranch`
- LCEL pipe operator `|`

It also demonstrates converting normal Python functions into Runnables and creating conditional branches.

## `Runnables_in_LangChain.md`

A detailed written reference for the Runnable architecture.

It covers:

- Why Runnables exist
- Problems with early specialized chains
- Standardization
- `invoke()`
- `batch()`
- `stream()`
- Runnable composition
- `RunnableSequence`
- `RunnableParallel`
- `RunnablePassthrough`
- `RunnableLambda`
- `RunnableBranch`
- Conditional workflows
- LCEL
- Runnables and Chains
- Runnables in RAG and Agentic AI workflows

---

# 8. `7.RAG/` — Retrieval-Augmented Generation

This is the largest application-oriented section of the repository.

It builds RAG knowledge step by step:

```text
Documents
   ↓
Document Loaders
   ↓
Text Splitting
   ↓
Embeddings
   ↓
Vector Store
   ↓
Retriever
   ↓
Relevant Context
   ↓
LLM
   ↓
Answer
```

## `1.document_loaders.ipynb`

Introduces LangChain document loaders.

It covers:

- `TextLoader`
- `PyPDFLoader`
- `DirectoryLoader`
- Glob patterns
- `load()`
- `lazy_load()`
- `WebBaseLoader`
- Document content
- Document metadata

The examples use repository documents such as `cricket.txt` and `dl-curriculum.pdf`.

## `2.textSplitters.ipynb`

Explores how large documents are divided into manageable chunks.

It covers:

- Character-based splitting
- Chunk size
- Chunk overlap
- Recursive character splitting
- Structure-aware splitting
- Semantic chunking concepts

The notebook emphasizes that splitting strategy directly affects downstream retrieval quality.

## `3.vector_stores.ipynb`

Introduces vector storage with **Chroma**.

The notebook demonstrates:

- Creating LangChain `Document` objects
- OpenAI embeddings
- Creating a persistent Chroma vector store
- Adding documents
- Reading stored documents
- Similarity search
- Similarity search with scores
- Metadata filtering
- Updating stored documents

The examples use IPL/cricket-related documents and metadata such as team names.

## `4.retrivers.ipynb`

Introduces LangChain retrievers.

It explains that a retriever receives a query and returns relevant documents.

The notebook demonstrates:

- Wikipedia Retriever
- Vector Store Retriever
- Similarity search
- MMR / Maximal Marginal Relevance
- Converting vector stores into retrievers
- Retriever invocation

The vector-store retriever pipeline is:

```text
Documents
 ↓
Embeddings
 ↓
Vector Store
 ↓
Retriever
 ↓
Relevant Documents
```

## `youtube_chatbot.ipynb`

Builds a complete **YouTube transcript RAG application**.

The notebook covers the complete RAG lifecycle:

### 1. Transcript ingestion

It demonstrates two approaches:

- `YouTubeTranscriptApi`
- LangChain's `YoutubeLoader`

### 2. Text splitting

Uses `RecursiveCharacterTextSplitter`.

### 3. Embeddings

Uses OpenAI embeddings.

### 4. Vector storage

Uses FAISS.

### 5. Retrieval

Creates a similarity-based retriever.

### 6. Augmentation

Combines the user question with retrieved transcript context.

### 7. Generation

Uses `ChatOpenAI` to generate the answer.

The complete flow is:

```text
YouTube URL
    ↓
Transcript
    ↓
Chunks
    ↓
Embeddings
    ↓
FAISS
    ↓
Retriever
    ↓
Relevant Transcript Chunks
    ↓
Prompt + Context
    ↓
ChatOpenAI
    ↓
Answer
```

## `RAG_notes.md`

Contains extensive written notes explaining the RAG architecture.

The notes cover concepts including:

- Why RAG is needed
- External knowledge bases
- Document ingestion
- Chunking
- Embeddings
- Vector stores
- Semantic search
- Retrieval
- Augmentation
- Generation
- End-to-end RAG architecture

## Supporting RAG data

### `cricket.txt`

A text knowledge source used for document-loading and retrieval experiments.

### `dl-curriculum.pdf`

A PDF used in document-loader and text-splitting examples.

### `Rag need.pdf`

Supporting material related to the RAG section.

### `books/Building Machine Learning Systems with Python - Second Edition.pdf`

A larger book PDF used as an example knowledge source.

---

# 9. `8.Agents/` — Tools, Tool Calling & AI Agents

This section moves from deterministic chains and RAG into **agentic systems**.

## `1.tools.ipynb`

Introduces the concept of tools and how tools extend LLM capabilities.

It demonstrates several built-in and custom tools:

- DuckDuckGo search
- Wikipedia
- Python REPL
- Shell tools
- Custom tools with `@tool`
- `StructuredTool`
- `BaseTool`
- Tool schemas
- Toolkits

The notebook progresses from:

```text
Python Function
      ↓
@tool
      ↓
Structured Tool
      ↓
LLM-usable Tool
```

## `2.tool_calling.ipynb`

Focuses specifically on **LLM tool calling**.

The notebook demonstrates:

1. Creating a tool.
2. Creating a chat model.
3. Binding the tool with `.bind_tools()`.
4. Sending a user message.
5. Inspecting `tool_calls`.
6. Passing tool results back into the conversation.

It also introduces a currency-conversion example and discusses injected tool arguments.

Core architecture:

```text
User
 ↓
LLM
 ↓
Tool Call?
 ├── No → Final Response
 └── Yes
       ↓
     Tool
       ↓
   Tool Result
       ↓
      LLM
       ↓
 Final Response
```

## `3.langchain_agents.ipynb`

Introduces LangChain's higher-level agent API.

The notebook defines a custom tipping-calculation tool and creates an agent using:

```python
create_agent(...)
```

The agent receives a natural-language request and decides how to use the available tool.

This demonstrates the transition from manually orchestrated tool calling to an agent abstraction.

## `4.agents_langchain.ipynb`

This file currently contains only a minimal notebook structure and does not contain a substantive implementation.

It is retained in the repository as part of the Agents section.

---

# 📦 Supporting Repository Files

## `requirements.txt`

The repository's Python dependencies are:

```text
langchain
langchain-openai
langchain-community
langgraph
python-dotenv
streamlit
pypdf
```

These dependencies support the workshop's model calls, LangChain components, community integrations, environment management, Streamlit applications, and PDF loading.

## `genai_Notes.pdf`

A large supporting PDF containing additional workshop/reference material.

## `assets/workshop-poster.png`

The workshop poster used in the README.

## `.gitignore`

Repository-level Git ignore configuration.

## `README.md`

This document provides the actual repository structure, learning progression, and explanation of the workshop material.

---

# 🧠 Complete Learning Path

```text
                         GENERATIVE AI
                              │
                              ▼
                         Prerequisites
                              │
                              ▼
                       Introduction to
                          LangChain
                              │
                              ▼
                    ┌─────────────────────┐
                    │       Basics        │
                    │ LLM Responses       │
                    │ Embeddings          │
                    └──────────┬──────────┘
                               ▼
                            Prompts
                               │
                    ┌──────────┴──────────┐
                    ▼                     ▼
                 Messages          Chat Templates
                    │                     │
                    └──────────┬──────────┘
                               ▼
                      Structured Outputs
                               │
              ┌────────────────┼────────────────┐
              ▼                ▼                ▼
          TypedDict         Pydantic       JSON Schema
              └────────────────┼────────────────┘
                               ▼
                        Output Parsers
                               │
                               ▼
                            Chains
                               │
                 ┌─────────────┼─────────────┐
                 ▼             ▼             ▼
              Linear        Parallel     Conditional
                 └─────────────┼─────────────┘
                               ▼
                         Runnables / LCEL
                               │
                               ▼
                              RAG
                               │
            ┌──────────────────┼──────────────────┐
            ▼                  ▼                  ▼
     Document Loaders    Text Splitters     Vector Stores
                                                    │
                                                    ▼
                                                Retrievers
                                                    │
                                                    ▼
                                               YouTube RAG
                                                    │
                                                    ▼
                                                  Tools
                                                    │
                                                    ▼
                                              Tool Calling
                                                    │
                                                    ▼
                                                 Agents
                                                    │
                                                    ▼
                                             🤖 Agentic AI
```

---

# 🛠️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/Rajendra-Pd-Joshi/GenAI-Langchain-Workshop.git
cd GenAI-Langchain-Workshop
```

### 2. Create a virtual environment

**Windows**

```bash
python -m venv venv
venv\Scripts\activate
```

**Linux / macOS**

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure environment variables

Create a local `.env` file for the API configuration required by the notebooks.

For OpenAI-based examples:

```env
OPENAI_API_KEY=your_api_key_here
```

The environment-setup notebook also demonstrates configuring **OpenRouter** with `ChatOpenAI`.

> **Security:** Never commit API keys, `.env` files, or other secrets to GitHub.

---

# 📖 Recommended Learning Order

For a learner starting from the beginning:

```text
1.  Prerequisites
2.  Introduction to LangChain
3.  Basics
4.  Prompts
5.  Structured Outputs
6.  Output Parsers
7.  Chains
8.  Runnables
9.  RAG
10. Agents
```

The sequence moves from **Python/environment fundamentals → model interaction → prompt engineering → structured data → composition → retrieval → tool use → agents**.

---

# 🎯 Workshop Goal

The repository demonstrates the progression from a simple LLM call to increasingly capable AI applications:

```text
Simple Model Call
       ↓
Prompt Engineering
       ↓
Structured Responses
       ↓
Composable Chains
       ↓
Runnables / LCEL
       ↓
Retrieval-Augmented Generation
       ↓
Tool-Using Applications
       ↓
Tool Calling
       ↓
AI Agents
       ↓
🚀 Agentic AI
```

---

# 🧰 Main Technologies

| Category | Technology |
| --- | --- |
| **Language** | Python |
| **LLM Framework** | LangChain |
| **Agent Framework** | LangGraph / LangChain Agents |
| **Model Integration** | ChatOpenAI / OpenAI |
| **Embeddings** | OpenAI Embeddings |
| **Vector Store** | Chroma, FAISS |
| **RAG** | LangChain retrieval components |
| **Document Processing** | PyPDF / LangChain loaders |
| **UI** | Streamlit |
| **Environment** | python-dotenv |
| **Validation** | Pydantic |
| **Structured Data** | TypedDict / JSON Schema |

---

# 👨‍🏫 Mentor

**Rajendra Prasad Joshi**  
Agentic AI Engineer

**Generative AI & Agentic AI Workshop**  
Society of Engineering Students  
Far Western University, School of Engineering — Mahendranagar, Kanchanpur

---

## ⭐ Support the Repository

If these workshop materials help you learn Generative AI, LangChain, RAG, tools, or AI agents, consider giving the repository a ⭐.

**Happy Learning & Building! 🚀🤖**
