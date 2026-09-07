# 🚀 Generative AI & Agentic AI Workshop

<p align="center">
  <img src="assets/workshop-poster.png" alt="Generative AI & Agentic AI Workshop" width="850"/>
</p>

<h3 align="center">From Prompting to Autonomous AI Agents</h3>

<p align="center">
  A hands-on workshop on Generative AI, LangChain, LCEL, RAG, Tools, and AI Agents.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/LangChain-0.3+-green?logo=chainlink&logoColor=white" alt="LangChain"/>
  <img src="https://img.shields.io/badge/LangGraph-included-orange" alt="LangGraph"/>
  <img src="https://img.shields.io/badge/Streamlit-enabled-red?logo=streamlit&logoColor=white" alt="Streamlit"/>
  <img src="https://img.shields.io/badge/License-MIT-lightgrey" alt="License"/>
</p>

---

## 🎓 About the Workshop

This repository contains the **hands-on code, notebooks, and learning materials** used during the **Generative AI & Agentic AI Workshop** organised by the **Society of Engineering Students, Far Western University, School of Engineering, Mahendranagar, Kanchanpur**.

The workshop was designed to take learners from the fundamentals of working with Large Language Models all the way to building modern **LLM-powered applications and autonomous AI agents** — step by step, with code at every stage.

The learning path progresses through:

```
LLMs → ChatModels → Embeddings → Prompts → Structured Output
     → Output Parsers → Chains → LCEL / Runnables
     → Document Loaders → Text Splitters → Vector Stores → Retrievers
     → RAG (YouTube) → Tools → Tool Binding → AI Agents
```

---

## 🏫 Workshop Details

| Field           | Information                                   |
| --------------- | --------------------------------------------- |
| **Workshop**    | Generative AI & Agentic AI                    |
| **Theme**       | From Prompting to Autonomous AI Agents        |
| **Organiser**   | Society of Engineering Students               |
| **Institution** | Far Western University, School of Engineering |
| **Location**    | Mahendranagar, Kanchanpur                     |
| **Mentor**      | Rajendra Prasad Joshi                         |
| **Mode**        | Online via Google Meet                        |
| **Date**        | 2083/05/06 (BS)                               |
| **Time**        | 9:00 AM onwards                               |

---

## 📁 Repository Structure

```text
📦 GenAI-Langchain-Workshop/
│
├── 📂 1.LLMs/
├── 📂 2.ChatModels/
├── 📂 3.Embedding/
├── 📂 4.langchain-prompts/
├── 📂 5.langchain-structured-output/
├── 📂 6.langchain_output_parsers/
├── 📂 7.langchain-chains/
├── 📂 8.Runnables/
├── 📂 9.Document-loader/
├── 📂 10.text-splitters/
├── 📂 11.Vector-store/
├── 📂 12.Retrivers/
├── 📂 13.Youtube_rag/
├── 📂 14.tools_langchain/
├── 📂 15.tool_binding/
├── 📂 16.agents/
│
├── 📂 assets/
│   └── 🖼️ workshop-poster.png
│
├── 📜 requirements.txt
├── 📜 .gitignore
└── 📜 README.md
```

---

## 📚 Topics Covered

### 1. 🧠 Large Language Models (LLMs)
`📂 1.LLMs/`

Introduction to interacting with Large Language Models through LangChain.

- Understanding what LLMs are and how they work
- Basic LLM invocation with LangChain
- Sending prompts and reading responses
- Using API-based language models (OpenAI, etc.)
- Environment setup and API key configuration

---

### 2. 💬 Chat Models
`📂 2.ChatModels/`

Understanding modern conversational AI interfaces.

- Difference between LLMs and Chat Models
- System messages, Human messages, AI messages
- Message-based interaction patterns
- Building multi-turn conversational calls

---

### 3. 📊 Text Embeddings
`📂 3.Embedding/`

Representing text as numerical vectors for semantic understanding.

- What are embeddings and why they matter
- Generating text embeddings with LangChain
- Embedding models overview
- Semantic representation of text
- Preparing embeddings for vector databases and RAG pipelines

---

### 4. ✍️ Prompt Engineering & Prompt Templates
`📂 4.langchain-prompts/`

Creating reusable, dynamic prompts to control LLM behaviour.

- Prompt engineering fundamentals
- `PromptTemplate` and `ChatPromptTemplate`
- Dynamic prompt variables with placeholders
- System + human prompt patterns
- Building reusable, composable prompts

---

### 5. 🧩 Structured Output
`📂 5.langchain-structured-output/`

Making LLM responses predictable and machine-readable.

- Why structured output matters for real applications
- Pydantic models and TypedDict
- JSON Schema definitions
- `with_structured_output()` method
- Consuming structured AI responses in code

---

### 6. 🔄 Output Parsers
`📂 6.langchain_output_parsers/`

Transforming raw LLM text responses into useful Python objects.

- Output parsing strategies
- Built-in LangChain parsers
- Structured response processing
- Integrating parsers into chains

---

### 7. 🔗 Chains & LCEL
`📂 7.langchain-chains/`

Composing multiple LangChain components together.

- Traditional LangChain chains (LLMChain, etc.)
- LangChain Expression Language (LCEL)
- The pipe `|` operator for composition
- Sequential execution of components
- Building reusable, readable chains

---

### 8. ⚙️ Runnables
`📂 8.Runnables/`

LangChain's core composable architecture for building flexible pipelines.

| Runnable              | Purpose                                  |
| --------------------- | ---------------------------------------- |
| `RunnableSequence`    | Execute components one after another     |
| `RunnableParallel`    | Execute multiple Runnables concurrently  |
| `RunnablePassthrough` | Pass input through unchanged             |
| `RunnableLambda`      | Wrap any Python function into a Runnable |
| `RunnableBranch`      | Conditional routing based on input       |

**`RunnableLambda` Example:**

```python
from langchain_core.runnables import RunnableLambda

chain = RunnableLambda(lambda x: x.upper())
print(chain.invoke("hello"))   # → HELLO
```

**`RunnableBranch` — Conditional Execution:**

```text
         Input
           │
       Condition
        /     \
     True     False
      │          │
  Runnable A  Runnable B
        \      /
         Output
```

---

### 9. 📄 Document Loaders
`📂 9.Document-loader/`

Loading external data into LangChain applications.

- PDF documents (`pypdf`)
- CSV files
- Web-based data
- Preparing external data for LLM pipelines

---

### 10. ✂️ Text Splitters
`📂 10.text-splitters/`

Chunking large documents before embedding and retrieval.

- Why chunking is necessary
- Chunk size and chunk overlap trade-offs
- `RecursiveCharacterTextSplitter`
- Preparing documents for vector stores

---

### 11. 🗄️ Vector Stores
`📂 11.Vector-store/`

Storing and searching embeddings at scale.

- What vector databases are and how they work
- Storing embeddings from documents
- Similarity search and semantic search
- Connecting embedding pipelines with vector stores

---

### 12. 🔍 Retrievers
`📂 12.Retrivers/`

The retrieval layer at the heart of RAG.

- Retriever interface in LangChain
- Similarity-based document retrieval
- Connecting retrievers with LLM chains
- Building end-to-end retrieval pipelines

---

### 13. 🎥 YouTube RAG
`📂 13.Youtube_rag/`

A complete Retrieval-Augmented Generation project using YouTube content.

```text
YouTube Video
      ↓
Transcript Extraction
      ↓
Document Processing
      ↓
Text Splitting
      ↓
Embeddings
      ↓
Vector Store
      ↓
Retriever
      ↓
LLM
      ↓
Question Answering over Video Content
```

This capstone RAG project demonstrates how to build a question-answering system grounded in a YouTube video's transcript — no hallucinations, only retrieved content.

---

### 14. 🛠️ Tools in LangChain
`📂 14.tools_langchain/`

Extending LLMs with the ability to call external functions.

- What tools are and why agents need them
- Creating custom Python tools
- Defining tool schemas and descriptions
- Using tools within LLM applications
- Tool-based reasoning patterns

---

### 15. 🔧 Tool Binding
`📂 15.tool_binding/`

Connecting tools directly to language models for automatic function calling.

- Binding tools to models with `.bind_tools()`
- OpenAI / LangChain function calling
- Tool schemas and model-driven tool selection
- Parsing tool call responses
- Connecting LLMs with real-world external functions

---

### 16. 🤖 AI Agents
`📂 16.agents/`

The workshop culminated with building **Agentic AI** systems.

- What are AI agents and how they differ from chains
- Tools + LLMs = Agents
- Agent reasoning loops (ReAct pattern)
- Tool execution and result feedback
- Autonomous task execution
- Building agent workflows with LangGraph
- Agent decision making and multi-step reasoning

---

## 🧠 Overall Learning Path

```text
                GENERATIVE AI
                     │
                     ▼
                   LLMs
                     │
                     ▼
                Chat Models
                     │
                     ▼
                Embeddings
                     │
                     ▼
                  Prompts
                     │
                     ▼
           Structured Output
                     │
                     ▼
             Output Parsers
                     │
                     ▼
                  Chains
                     │
                     ▼
              LCEL / Runnables
                     │
           ┌─────────┴──────────┐
           ▼                    ▼
      Sequential           Conditional
      Processing             Branching
           │                    │
           └─────────┬──────────┘
                     ▼
                    RAG
                     │
        ┌────────────┼────────────┐
        ▼            ▼            ▼
  Doc Loaders   Text Splitters  Embeddings
                                   │
                                   ▼
                             Vector Stores
                                   │
                                   ▼
                               Retrievers
                                   │
                                   ▼
                             YouTube RAG App
                                   │
                                   ▼
                                 Tools
                                   │
                                   ▼
                             Tool Binding
                                   │
                                   ▼
                               AI Agents
                                   │
                                   ▼
                          🤖 Agentic AI
```

---

## 🛠️ Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/Rajendra-Pd-Joshi/GenAI-Langchain-Workshop.git
cd GenAI-Langchain-Workshop
```

### 2. Create a Virtual Environment

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**Linux / macOS:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

The `requirements.txt` includes:

```text
langchain
langchain-openai
langchain-community
langgraph
python-dotenv
streamlit
pypdf
```

### 4. Configure Environment Variables

Create a `.env` file in the root directory:

```env
OPENAI_API_KEY=your_openai_api_key_here
```

> ⚠️ Never commit your `.env` file or expose API keys publicly. The `.gitignore` is already configured to exclude it.

---

## 📖 Recommended Learning Order

Follow the numbered folders in sequence for the best learning experience:

```
1.  LLMs                     → Understand base language models
2.  ChatModels               → Switch to conversational interfaces
3.  Embedding                → Represent text as vectors
4.  Prompts                  → Control LLM behaviour with templates
5.  Structured Output        → Get predictable, typed responses
6.  Output Parsers           → Transform raw output into Python objects
7.  Chains                   → Compose components with LCEL
8.  Runnables                → Master the full Runnable toolkit
9.  Document Loaders         → Bring in external data (PDF, CSV, web)
10. Text Splitters            → Chunk documents for retrieval
11. Vector Stores             → Store and search embeddings
12. Retrievers                → Retrieve relevant context
13. YouTube RAG               → Build a complete RAG app
14. Tools                     → Define tools for LLMs to call
15. Tool Binding              → Attach tools to models
16. AI Agents                 → Build autonomous reasoning systems
```

---

## 🎯 Workshop Goal

The primary goal was to guide learners through the **complete modern AI stack** — from a single prompt to a fully autonomous agent:

```
Simple Prompting
      ↓
LLM Applications
      ↓
Chained Components (LCEL)
      ↓
Retrieval-Augmented Generation (RAG)
      ↓
Tool-Using Applications
      ↓
Autonomous AI Agents
      ↓
🚀 Agentic AI Systems
```

---

## 🧰 Technologies & Concepts

| Category             | Tools / Concepts                                  |
| -------------------- | ------------------------------------------------- |
| **Language**         | Python 3.10+                                      |
| **LLM Framework**    | LangChain, LangGraph                              |
| **LLM Providers**    | OpenAI (GPT models)                               |
| **Embeddings**       | OpenAI Embeddings, LangChain Embedding interfaces |
| **Vector Stores**    | FAISS / Chroma (via `langchain-community`)        |
| **Document Loading** | `pypdf`, LangChain Document Loaders               |
| **RAG**              | Retrieval-Augmented Generation pipeline           |
| **Agent Framework**  | LangChain Agents, LangGraph                       |
| **UI**               | Streamlit                                         |
| **Env Management**   | `python-dotenv`                                   |

---

## 🔗 References

- [LangChain Documentation](https://python.langchain.com/)
- [LangChain Python API Reference](https://reference.langchain.com/python/)
- [LangGraph Documentation](https://langchain-ai.github.io/langgraph/)
- [LangChain LCEL Guide](https://python.langchain.com/docs/concepts/lcel/)
- [RunnableLambda Reference](https://reference.langchain.com/python/langchain-core/runnables/base/RunnableLambda)
- [RunnableBranch Reference](https://reference.langchain.com/python/langchain-core/runnables/branch/RunnableBranch)
- [OpenAI API Docs](https://platform.openai.com/docs/)

---

## 👨‍🏫 Mentor

**Rajendra Prasad Joshi**
Junior AI/ML Engineer | Agentic AI Intern at Alba Connect Co., Ltd. (Tokyo)
B.Tech Computer Science, VIT Vellore | CGPA 9.08/10
COMPEX Scholar — Indian Embassy, Kathmandu

*Generative AI & Agentic AI Workshop*
Society of Engineering Students
Far Western University, School of Engineering — Mahendranagar, Kanchanpur

---

## 🙏 Acknowledgement

This repository contains educational materials and hands-on implementations prepared for the **Generative AI & Agentic AI Workshop**. It is intended as a practical learning resource for students and developers exploring the foundations of **Generative AI, LangChain, RAG, Tool Calling, and Agentic AI**.

---

## ⭐ Support the Repository

If this workshop material helped you learn something new, consider giving it a ⭐ on GitHub — it helps others discover the resource too.

**Happy Learning & Building! 🚀🤖**