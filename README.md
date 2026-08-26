# 🚀 Generative AI & Agentic AI Workshop

<p align="center">
  <img src="assets/workshop-poster.png" alt="Generative AI & Agentic AI Workshop" width="850"/>
</p>

<h3 align="center">
  From Prompting to Autonomous AI Agents
</h3>

<p align="center">
  Hands-on workshop on Generative AI, LangChain, LCEL, RAG, Tools, and AI Agents.
</p>

---

## 🎓 About the Workshop

This repository contains the **hands-on code, examples, notebooks, and learning materials** used during the **Generative AI & Agentic AI Workshop** organized by the **Society of Engineering Students, Far Western University, School of Engineering, Mahendranagar, Kanchanpur**.

The workshop was designed to take learners from the fundamentals of working with Large Language Models to building modern **LLM-powered applications and autonomous AI agents**.

The learning path progresses from:

**LLMs → ChatModels → Prompts → Structured Output → Chains → LCEL/Runnables → RAG → Tools → Tool Binding → AI Agents**

---

## 🏫 Workshop Information

| Details         | Information                                   |
| --------------- | --------------------------------------------- |
| **Workshop**    | Generative AI & Agentic AI                    |
| **Theme**       | From Prompting to Autonomous AI Agents        |
| **Organizer**   | Society of Engineering Students               |
| **Institution** | Far Western University, School of Engineering |
| **Location**    | Mahendranagar, Kanchanpur                     |
| **Mentor**      | Rajendra Prasad Joshi                         |
| **Mode**        | Online via Google Meet                        |
| **Date**        | 2083/05/06                                    |
| **Time**        | 9:00 AM onwards                               |

---

# 📚 Topics Covered

The workshop covered the following major areas of Generative AI and LangChain.

## 1. Large Language Models (LLMs)

Introduction to interacting with Large Language Models through LangChain.

Topics include:

* Understanding LLMs
* Basic LLM invocation
* Sending prompts to language models
* Working with model responses
* Using API-based language models
* Environment and API key configuration

📁 Folder:

```text
1.LLMs/
```

---

## 2. Chat Models

Understanding modern conversational AI interfaces.

Topics include:

* Chat models
* System messages
* Human messages
* AI messages
* Message-based interaction
* Building conversational model calls

📁 Folder:

```text
2.ChatModels/
```

---

## 3. Text Embeddings

Understanding how text can be represented as numerical vectors.

Topics include:

* What are embeddings?
* Generating text embeddings
* Embedding models
* Semantic representation of text
* Preparing embeddings for vector databases and RAG

📁 Folder:

```text
3.Embedding/
```

---

## 4. Prompt Engineering & Prompt Templates

Learning how to create reusable and dynamic prompts.

Topics include:

* Prompt engineering fundamentals
* `PromptTemplate`
* `ChatPromptTemplate`
* Dynamic prompt variables
* System and human prompts
* Building reusable prompts

📁 Folder:

```text
4.langchain-prompts/
```

---

## 5. Structured Output

Making LLM responses predictable and machine-readable.

Topics include:

* Structured responses from LLMs
* Pydantic models
* TypedDict
* JSON Schema
* `with_structured_output()`
* Working with structured AI responses

📁 Folder:

```text
5.langchain-structured-output/
```

---

## 6. Output Parsers

Understanding how raw LLM responses can be transformed into useful formats.

Topics include:

* Output parsing
* Parsing model responses
* Structured response processing
* Integrating parsers into chains

📁 Folder:

```text
6.langchain_output_parsers/
```

---

# 🔗 7. Chains & LCEL

Introduction to composing multiple LangChain components together.

Topics include:

* Traditional LangChain chains
* LangChain Expression Language (LCEL)
* Pipe `|` operator
* Sequential execution
* Combining prompts and models
* Building reusable chains

📁 Folder:

```text
7.langchain-chains/
```

---

# ⚙️ 8. Runnables

A major part of the workshop focused on LangChain's Runnable architecture.

Topics include:

* `RunnableSequence`
* `RunnableParallel`
* `RunnablePassthrough`
* `RunnableLambda`
* `RunnableBranch`
* Runnable composition
* Conditional execution
* Chaining Runnables
* Data transformation using Runnables

### RunnableLambda

`RunnableLambda` allows a normal Python function to be converted into a LangChain Runnable so that it can be composed with other Runnable components.

Example:

```python
from langchain_core.runnables import RunnableLambda

chain = RunnableLambda(lambda x: x.upper())

result = chain.invoke("hello")

print(result)
```

Output:

```text
HELLO
```

### RunnableBranch

`RunnableBranch` allows conditional execution where different Runnables can be selected depending on the input.

Conceptually:

```text
                Input
                  |
             Condition
              /     \
           True     False
            |         |
        Runnable A  Runnable B
            \         /
             \       /
              Output
```

This makes it possible to create **conditional chains** and route inputs to different processing paths.

📁 Folder:

```text
8.Runnables/
```

---

# 📄 9. Document Loaders

Introduction to loading external data into LangChain.

Topics include:

* Loading documents
* PDF documents
* CSV files
* Web-based data
* Preparing external data for LLM applications

📁 Folder:

```text
9.Document-loader/
```

---

# ✂️ 10. Text Splitters

Understanding why large documents need to be divided into smaller chunks before being processed by embedding and retrieval systems.

Topics include:

* Document chunking
* Chunk size
* Chunk overlap
* `RecursiveCharacterTextSplitter`
* Preparing documents for vector stores

📁 Folder:

```text
10.text-splitters/
```

---

# 🗄️ 11. Vector Stores

Understanding how embeddings can be stored and searched.

Topics include:

* Vector databases
* Storing embeddings
* Similarity search
* Semantic search
* Connecting embeddings with vector stores

📁 Folder:

```text
11.Vector-store/
```

---

# 🔍 12. Retrievers

Understanding the retrieval component of Retrieval-Augmented Generation.

Topics include:

* Retrievers
* Similarity-based retrieval
* Retrieving relevant documents
* Connecting retrievers with LLM chains
* Building retrieval pipelines

📁 Folder:

```text
12.Retrivers/
```

---

# 🎥 13. YouTube RAG

A practical Retrieval-Augmented Generation project based on YouTube content.

The project demonstrates how to:

```text
YouTube Video
      ↓
Transcript
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
Question Answering
```

The goal is to build a system that can answer questions based on the content of a YouTube video's transcript.

📁 Folder:

```text
13.Youtube_rag/
```

---

# 🛠️ 14. Tools in LangChain

Introduction to tools and how LLM applications can interact with external functionality.

Topics include:

* What are tools?
* Creating custom Python tools
* Defining tool functions
* Using tools with LLM applications
* Tool-based reasoning

📁 Folder:

```text
14.tools_langchain/
```

---

# 🔧 15. Tool Binding

Understanding how tools can be connected directly to language models.

Topics include:

* Binding tools to models
* Function calling
* Tool schemas
* Model-driven tool selection
* Connecting LLMs with external functions

📁 Folder:

```text
15.tool_binding/
```

---

# 🤖 16. AI Agents

The workshop concluded with the concepts behind **Agentic AI**.

Topics include:

* What are AI agents?
* Tools + LLMs
* Agent reasoning
* Tool execution
* Autonomous task execution
* Building AI agent workflows
* Agent decision making
* Connecting agents with external tools

📁 Folder:

```text
16.agents/
```

---

# 🧠 Overall Learning Path

The complete workshop progression can be visualized as:

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
              ┌───────┴────────┐
              ▼                ▼
       Sequential          Conditional
        Processing           Branching
              │                │
              └───────┬────────┘
                      ▼
                     RAG
                      │
          ┌───────────┼───────────┐
          ▼           ▼           ▼
       Loaders    Splitters   Embeddings
                                  │
                                  ▼
                            Vector Stores
                                  │
                                  ▼
                              Retrievers
                                  │
                                  ▼
                               RAG Apps
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

# 📁 Repository Structure

```text
📦 langchain-models
│
├── 📂 1.LLMs
├── 📂 2.ChatModels
├── 📂 3.Embedding
├── 📂 4.langchain-prompts
├── 📂 5.langchain-structured-output
├── 📂 6.langchain_output_parsers
├── 📂 7.langchain-chains
├── 📂 8.Runnables
├── 📂 9.Document-loader
├── 📂 10.text-splitters
├── 📂 11.Vector-store
├── 📂 12.Retrivers
├── 📂 13.Youtube_rag
├── 📂 14.tools_langchain
├── 📂 15.tool_binding
├── 📂 16.agents
│
├── 📂 assets
│   └── 🖼️ workshop-poster.png
│
├── 📜 requirements.txt
├── 📜 .gitignore
└── 📜 README.md
```

---

# 🛠️ Installation & Setup

## 1. Clone the repository

```bash
git clone https://github.com/Rajendra-Pd-Joshi/langchain-models.git
```

```bash
cd langchain-models
```

---

## 2. Create a Virtual Environment

### Windows

```bash
python -m venv venv
```

```bash
venv\Scripts\activate
```

### Linux / macOS

```bash
python3 -m venv venv
```

```bash
source venv/bin/activate
```

---

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

# 🔐 Environment Variables

Create a `.env` file in the root directory.

Example:

```env
OPENAI_API_KEY=your_api_key_here
```

Depending on the notebook or example, additional model-provider API keys may be required.

> ⚠️ Never commit your `.env` file or expose API keys publicly.

---

# 📖 Recommended Learning Order

For beginners, follow the repository in this order:

```text
1. LLMs
   ↓
2. ChatModels
   ↓
3. Embedding
   ↓
4. Prompts
   ↓
5. Structured Output
   ↓
6. Output Parsers
   ↓
7. Chains
   ↓
8. Runnables
   ↓
9. Document Loaders
   ↓
10. Text Splitters
   ↓
11. Vector Stores
   ↓
12. Retrievers
   ↓
13. YouTube RAG
   ↓
14. Tools
   ↓
15. Tool Binding
   ↓
16. AI Agents
```

---

# 🎯 Workshop Goal

The primary goal of this workshop was to help learners understand the evolution of modern AI applications:

```text
Prompting
    ↓
LLM Applications
    ↓
Chains
    ↓
RAG
    ↓
Tool-Using Applications
    ↓
AI Agents
    ↓
Agentic AI
```

By the end of the workshop, learners were introduced to the building blocks required to move from simple **LLM interactions** toward **tool-using and autonomous AI systems**.

---

# 👨‍🏫 Mentor

### Rajendra Prasad Joshi

**Generative AI & Agentic AI Workshop**

Society of Engineering Students
Far Western University, School of Engineering
Mahendranagar, Kanchanpur

---

# 📚 Technologies & Concepts

The workshop introduced and used technologies and concepts including:

* 🐍 Python
* 🦜🔗 LangChain
* 🤖 Large Language Models
* 💬 Chat Models
* ✨ Prompt Engineering
* 📊 Text Embeddings
* 🧩 Structured Outputs
* 🔗 LCEL
* ⚙️ Runnables
* 🌿 Conditional Branching
* 📄 Document Loaders
* ✂️ Text Splitting
* 🗄️ Vector Stores
* 🔍 Retrievers
* 📚 RAG
* 🛠️ Tools
* 🔧 Tool Calling / Binding
* 🤖 AI Agents
* 🚀 Agentic AI

---

# 🔗 References

* [LangChain Documentation](https://python.langchain.com/)
* [LangChain Python Reference](https://reference.langchain.com/python/)
* [LangChain Runnables](https://reference.langchain.com/python/langchain-core/runnables/)
* [RunnableLambda](https://reference.langchain.com/python/langchain-core/runnables/base/RunnableLambda)
* [RunnableBranch](https://reference.langchain.com/python/langchain-core/runnables/branch/RunnableBranch)

---

# 🙏 Acknowledgement

This repository contains educational material and hands-on implementations prepared for the **Generative AI & Agentic AI Workshop**.

The repository is intended as a practical learning resource for students and developers who want to explore the foundations of **Generative AI, LangChain, RAG, Tool Calling, and Agentic AI**.

---

## ⭐ Support the Repository

If this repository helped you learn something about Generative AI or LangChain, consider giving it a ⭐ on GitHub.

**Happy Learning & Building! 🚀🤖**
