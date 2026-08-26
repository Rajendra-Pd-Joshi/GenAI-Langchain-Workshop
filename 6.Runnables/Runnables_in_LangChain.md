# 🔗 Runnables in LangChain

> Understanding why Runnables exist, how they work, and how they enable
> composable LangChain workflows.

------------------------------------------------------------------------

## 📌 Overview

**Runnables** are one of the most important concepts in LangChain.

They provide a standardized way for different LangChain components to
communicate and work together.

This chapter covers:

-   Why Runnables were introduced
-   Problems with the early chain-based architecture
-   Lack of standardization between components
-   Code bloat and specialized chains
-   The common `Runnable` interface
-   `invoke()`, `batch()`, and `stream()`
-   Runnable composition
-   `RunnableSequence`
-   `RunnableParallel`
-   `RunnablePassthrough`
-   `RunnableLambda`
-   `RunnableBranch`
-   Conditional chaining
-   How Runnables relate to Chains and LCEL

------------------------------------------------------------------------

# 1. Why Do We Need Runnables?

To understand Runnables, we first need to understand the problems that
existed in the early LangChain architecture.

LangChain was created to make it easier to build applications powered by
Large Language Models.

As LLM applications became more complex, developers started building:

-   Chatbots
-   RAG applications
-   Question-answering systems
-   AI assistants
-   Tool-using applications
-   AI agents

A common workflow looked like:

``` text
Input
  ↓
Prompt
  ↓
LLM
  ↓
Output
```

LangChain initially provided many components and specialized chains to
make these workflows easier.

However, as the number of use cases increased, the architecture became
increasingly difficult to maintain and learn.

------------------------------------------------------------------------

# 2. Early LangChain Chains

Initially, LangChain created specialized chains for different use cases.

For example:

``` text
Prompt + LLM
    ↓
LLMChain
```

And:

``` text
Retriever + Prompt + LLM
          ↓
    Retrieval Chain
```

The approach worked well for individual use cases.

But every new use case could require another chain abstraction.

This gradually resulted in many different chains.

------------------------------------------------------------------------

# 3. Problem: Too Many Specialized Chains

As more use cases appeared:

``` text
More Use Cases
      ↓
More Chain Classes
      ↓
Larger Codebase
      ↓
More Maintenance
      ↓
More Complexity
```

Developers also had to learn which chain was appropriate for each use
case.

For example:

``` text
Use Case A → Chain A
Use Case B → Chain B
Use Case C → Chain C
Use Case D → Chain D
```

This increased the learning curve.

------------------------------------------------------------------------

# 4. Problem: Lack of Standardization

Another important problem was that different components used different
interfaces.

Conceptually:

``` text
Prompt Template
      ↓
   format()

LLM
      ↓
   predict()

Retriever
      ↓
get_relevant_documents()
```

For example:

``` python
prompt = prompt_template.format(topic="AI")
response = llm.predict(prompt)
```

The developer had to manually connect these components.

This required custom **glue code**.

------------------------------------------------------------------------

# 5. The Need for a Common Interface

The LangChain team needed a standardized interface.

Instead of having:

``` text
Prompt → format()
LLM → predict()
Retriever → get_relevant_documents()
```

the idea was to have components communicate through a common interface:

``` text
Prompt → invoke()
LLM → invoke()
Retriever → invoke()
```

This is the fundamental idea behind Runnables.

------------------------------------------------------------------------

# 6. What Is a Runnable?

A **Runnable** is a standardized unit of work in LangChain.

Conceptually:

``` text
Input
  ↓
┌─────────────────┐
│    Runnable     │
│                 │
│  Process Input  │
└─────────────────┘
  ↓
Output
```

A Runnable receives an input, performs some operation, and returns an
output.

Different components can implement the same Runnable interface.

------------------------------------------------------------------------

# 7. Runnable as an Abstract Interface

Conceptually, the architecture can be represented as:

``` python
from abc import ABC, abstractmethod

class Runnable(ABC):

    @abstractmethod
    def invoke(self, input):
        pass
```

A component can implement this interface:

``` python
class MyRunnable(Runnable):

    def invoke(self, input):
        return input.upper()
```

Now the component follows the common Runnable protocol.

The important idea is not the exact implementation above, but the
abstraction:

``` text
Common Interface
       ↓
     invoke()
       ↓
Different Components
```

------------------------------------------------------------------------

# 8. The Most Important Runnable Method: `invoke()`

The most important method to understand first is:

``` python
invoke()
```

Example:

``` python
result = runnable.invoke(input)
```

Conceptually:

``` text
Input
  ↓
invoke()
  ↓
Runnable
  ↓
Output
```

This common execution interface is what makes composition possible.

------------------------------------------------------------------------

# 9. Other Important Runnable Methods

Important execution methods include:

``` text
invoke()
batch()
stream()
```

## `invoke()`

Used to process a single input:

``` python
result = runnable.invoke(input)
```

## `batch()`

Used to process multiple inputs:

``` python
results = runnable.batch([
    input1,
    input2,
    input3
])
```

Conceptually:

``` text
Input 1 ─┐
Input 2 ─┼──→ Runnable ──→ Outputs
Input 3 ─┘
```

## `stream()`

Used when output is produced incrementally:

``` python
for chunk in runnable.stream(input):
    print(chunk)
```

Conceptually:

``` text
Input
  ↓
Runnable
  ↓
Chunk 1
Chunk 2
Chunk 3
...
```

------------------------------------------------------------------------

# 10. Runnables as LEGO Blocks 🧱

A useful analogy is **LEGO blocks**.

Each Runnable is like a reusable LEGO block.

``` text
┌──────────────┐
│    Prompt    │
└──────────────┘

┌──────────────┐
│     LLM      │
└──────────────┘

┌──────────────┐
│    Parser    │
└──────────────┘
```

Because they follow a common interface, we can connect them:

``` text
Prompt
  ↓
LLM
  ↓
Parser
```

Just like LEGO:

``` text
🧱 + 🧱 + 🧱
```

Small components can be combined into larger workflows.

------------------------------------------------------------------------

# 11. Runnable Composition

Runnables can be composed together:

``` text
Runnable A
    ↓
Runnable B
    ↓
Runnable C
```

The resulting workflow can itself be treated as a Runnable.

For example:

``` text
A → B → C
```

can become:

``` text
┌─────────────────┐
│    A → B → C    │
└─────────────────┘
       Runnable
```

This allows us to build increasingly complex workflows.

------------------------------------------------------------------------

# 12. LCEL and the Pipe Operator

LangChain Expression Language (LCEL) provides a convenient way to
compose Runnables.

The pipe operator is:

``` python
|
```

For example:

``` python
chain = prompt | llm
```

This means:

``` text
Prompt
  ↓
 LLM
```

We can extend it:

``` python
chain = prompt | llm | parser
```

Flow:

``` text
Prompt
  ↓
LLM
  ↓
Parser
  ↓
Output
```

------------------------------------------------------------------------

# 13. RunnableSequence

`RunnableSequence` represents sequential execution.

``` text
A → B → C → D
```

The output of one Runnable becomes the input of the next.

Example:

``` python
from langchain_core.runnables import RunnableLambda

step1 = RunnableLambda(lambda x: x + 1)
step2 = RunnableLambda(lambda x: x * 2)

chain = step1 | step2

result = chain.invoke(5)

print(result)
```

Flow:

``` text
5
 ↓
+1
 ↓
6
 ↓
×2
 ↓
12
```

------------------------------------------------------------------------

# 14. RunnableParallel

Sometimes multiple operations need to be performed independently.

This is where `RunnableParallel` is useful.

``` text
                Input
                  |
          ┌───────┴───────┐
          ↓               ↓
      Runnable A      Runnable B
          ↓               ↓
       Output A        Output B
```

Conceptually:

``` python
from langchain_core.runnables import RunnableParallel

chain = RunnableParallel(
    first=first_chain,
    second=second_chain
)
```

The result contains multiple outputs:

``` python
{
    "first": "...",
    "second": "..."
}
```

------------------------------------------------------------------------

# 15. RunnablePassthrough

`RunnablePassthrough` passes the original input through without changing
it.

``` python
from langchain_core.runnables import RunnablePassthrough

chain = RunnablePassthrough()

result = chain.invoke("Hello")

print(result)
```

Output:

``` text
Hello
```

It is particularly useful when we want to preserve the original input
while also creating additional processed values.

Conceptually:

``` text
              Input
                |
        ┌───────┴────────┐
        ↓                ↓
   Process Input    Pass Original
        ↓                ↓
   Processed Data     Original
```

------------------------------------------------------------------------

# 16. RunnableLambda

`RunnableLambda` converts a normal Python function into a Runnable.

Example:

``` python
from langchain_core.runnables import RunnableLambda

def process_text(text):
    return text.upper()

runnable = RunnableLambda(process_text)

result = runnable.invoke("hello")

print(result)
```

Output:

``` text
HELLO
```

This is useful for adding custom Python logic to a LangChain workflow.

Example:

``` python
def clean_text(text):
    return text.strip()

chain = (
    RunnableLambda(clean_text)
    | prompt
    | llm
)
```

Flow:

``` text
Input
  ↓
Custom Python Function
  ↓
Prompt
  ↓
LLM
  ↓
Output
```

------------------------------------------------------------------------

# 17. RunnableBranch

Not every workflow should follow the same path.

Sometimes the next step depends on a condition.

For example:

``` text
                 Input
                   |
                   ↓
               Condition
               /       \
              ↓         ↓
         Runnable A  Runnable B
              \         /
               \       /
                Output
```

`RunnableBranch` can be used to build conditional workflows.

Example:

``` python
from langchain_core.runnables import RunnableBranch

branch = RunnableBranch(
    (
        lambda x: x["type"] == "technical",
        technical_chain
    ),
    general_chain
)
```

Flow:

``` text
Input
  ↓
Check Condition
  ↓
 ┌───────────────────┐
 │                   │
Technical          General
 │                   │
 ↓                   ↓
Technical Chain   General Chain
 │                   │
 └─────────┬─────────┘
           ↓
         Output
```

------------------------------------------------------------------------

# 18. Conditional Chaining

Conditional chaining is useful when different inputs need different
processing paths.

Example:

``` text
                 User Query
                     |
                     ↓
                 Classifier
                     |
          ┌──────────┴──────────┐
          ↓                     ↓
      Technical              General
          ↓                     ↓
   Technical Chain        General Chain
          \                     /
           \                   /
            └───────┬─────────┘
                    ↓
                 Response
```

This allows applications to dynamically choose which Runnable should
process an input.

------------------------------------------------------------------------

# 19. Building a Simple Runnable Pipeline

Consider:

``` text
User Input
    ↓
Clean Input
    ↓
Prompt
    ↓
LLM
    ↓
Parser
    ↓
Final Answer
```

Using Runnables:

``` python
from langchain_core.runnables import RunnableLambda

clean_input = RunnableLambda(
    lambda x: x.strip()
)

chain = (
    clean_input
    | prompt
    | llm
    | parser
)
```

Then:

``` python
result = chain.invoke("  Explain Runnables  ")
```

------------------------------------------------------------------------

# 20. Runnables and Chains

An important concept is:

> **Chains can be built by composing Runnables.**

For example:

``` text
Prompt
  ↓
LLM
  ↓
Parser
```

Each component can participate in the Runnable model.

The complete workflow can also behave like a Runnable.

Therefore:

``` text
Runnable
    ↓
Runnable
    ↓
Runnable
```

can become:

``` text
One Larger Runnable
```

This is one of the reasons Runnable composition is so powerful.

------------------------------------------------------------------------

# 21. Runnables and the Evolution of LangChain

The evolution can be summarized as:

``` text
LLM Applications
       ↓
Many Independent Components
       ↓
Different Interfaces
       ↓
Custom Glue Code
       ↓
Specialized Chains
       ↓
Too Many Chains
       ↓
Complexity
       ↓
Need for Standardization
       ↓
Runnables
       ↓
Common Interface
       ↓
Composition
       ↓
Flexible Workflows
```

------------------------------------------------------------------------

# 22. Before Runnables vs With Runnables

  Before Runnables          With Runnables
  ------------------------- ------------------------
  Different interfaces      Common interface
  `format()`                `invoke()`
  `predict()`               `invoke()`
  Custom glue code          Composition
  Many specialized chains   Reusable components
  Large codebase            Modular architecture
  Steep learning curve      Consistent abstraction
  Less flexible             Highly composable
  Fixed workflows           Dynamic workflows

------------------------------------------------------------------------

# 23. Runnable Types / Building Blocks

  Runnable                Purpose
  ----------------------- -------------------------------------------
  `RunnableSequence`      Sequential execution
  `RunnableParallel`      Parallel execution
  `RunnablePassthrough`   Pass input unchanged
  `RunnableLambda`        Convert a Python function into a Runnable
  `RunnableBranch`        Conditional routing

These abstractions allow us to construct different kinds of workflows.

------------------------------------------------------------------------

# 24. Execution Patterns

## Sequential

``` text
A
↓
B
↓
C
```

Using:

``` python
A | B | C
```

------------------------------------------------------------------------

## Parallel

``` text
      ┌→ A
Input ┤
      └→ B
```

Using:

``` python
RunnableParallel(
    a=A,
    b=B
)
```

------------------------------------------------------------------------

## Conditional

``` text
       Input
         ↓
    Condition
     /     \
    A       B
```

Using:

``` python
RunnableBranch(...)
```

------------------------------------------------------------------------

## Custom Python Logic

``` text
Input
  ↓
Python Function
  ↓
Output
```

Using:

``` python
RunnableLambda(function)
```

------------------------------------------------------------------------

## Passthrough

``` text
Input
  ↓
Same Input
```

Using:

``` python
RunnablePassthrough()
```

------------------------------------------------------------------------

# 25. Complete Runnable Architecture

A LangChain application can combine several Runnable abstractions:

``` text
                         Runnable
                             |
          ┌──────────────────┼──────────────────┐
          ↓                  ↓                  ↓
   RunnableLambda      RunnableBranch     RunnableParallel
          |                  |                  |
          ↓                  ↓                  ↓
    Custom Logic       Conditional         Parallel
                       Routing             Execution
          |
          └──────────────────┬──────────────────┘
                             ↓
                    RunnableSequence
                             ↓
                      Complex Workflow
```

------------------------------------------------------------------------

# 26. Example: RAG Workflow

Runnables can be used as building blocks for more advanced applications
such as RAG.

``` text
Question
   ↓
Retriever
   ↓
Documents
   ↓
Prompt
   ↓
LLM
   ↓
Answer
```

A RAG application can therefore be understood as a composition of
multiple processing components.

------------------------------------------------------------------------

# 27. Example: Agentic AI Workflow

The same idea extends to AI agents.

Conceptually:

``` text
User
 ↓
Agent
 ↓
Reasoning
 ↓
Tool Selection
 ↓
Tool
 ↓
Observation
 ↓
Reasoning
 ↓
Final Answer
```

Complex agentic workflows can be constructed from smaller reusable
components.

------------------------------------------------------------------------

# 28. The LEGO Principle

The core idea behind Runnables can be remembered using LEGO:

``` text
🧱 Runnable A
       +
🧱 Runnable B
       +
🧱 Runnable C
       =
🧱 Larger Workflow
```

Then:

``` text
🧱 Larger Workflow
       +
🧱 Runnable D
       =
🧱 Even Larger Workflow
```

A composition of components can itself become a building block.

This enables flexible and reusable AI workflows.

------------------------------------------------------------------------

# 29. Why Runnables Exist --- Short Answer

If you need to explain Runnables in an interview or classroom:

> **Runnables were introduced to provide a common interface for
> LangChain components so that they could be easily composed, reused,
> and connected without requiring a separate specialized chain for every
> use case.**

In short:

``` text
Many Specialized Chains
          ↓
       Complexity
          ↓
   Need for Standardization
          ↓
       Runnables
          ↓
      Composition
          ↓
 Flexible AI Workflows
```

------------------------------------------------------------------------

# 30. Key Takeaways

### 1. Runnables provide standardization

Different components can follow a common interface.

``` python
invoke()
```

### 2. Runnables reduce glue code

Instead of manually connecting components with different APIs,
components can communicate through a common abstraction.

### 3. Runnables are composable

``` python
prompt | llm | parser
```

### 4. Runnables are modular

Each component can perform a specific task.

### 5. Runnables can form larger Runnables

``` text
A → B → C
```

can become a larger composable workflow.

### 6. Runnables support multiple execution patterns

``` text
invoke()
batch()
stream()
```

### 7. Runnables support complex workflows

Using:

``` text
RunnableSequence
RunnableParallel
RunnablePassthrough
RunnableLambda
RunnableBranch
```

we can create:

-   Sequential workflows
-   Parallel workflows
-   Conditional workflows
-   Custom processing
-   Dynamic routing

------------------------------------------------------------------------

# 31. Quick Revision

``` text
What is a Runnable?
→ A standardized unit of work in LangChain.

Why do Runnables exist?
→ To standardize components and make them composable.

Most important method?
→ invoke()

Multiple inputs?
→ batch()

Streaming?
→ stream()

Sequential workflow?
→ RunnableSequence

Parallel workflow?
→ RunnableParallel

Pass input unchanged?
→ RunnablePassthrough

Custom Python function?
→ RunnableLambda

Conditional workflow?
→ RunnableBranch

How are Runnables commonly composed?
→ Using the | pipe operator.

What is the main analogy?
→ LEGO blocks.

Why are Runnables important?
→ They provide a foundation for flexible LangChain workflows.
```

------------------------------------------------------------------------

# 🎓 Workshop Topic

**Generative AI & Agentic AI Workshop**

### Topic Covered

**Runnables in LangChain --- From Components to Composable AI
Workflows**

------------------------------------------------------------------------

## 🔗 Related Topics

Continue learning:

1.  LangChain Models
2.  Chat Models
3.  Prompt Templates
4.  Structured Output
5.  Output Parsers
6.  Chains
7.  LCEL
8.  Runnables
9.  Document Loaders
10. Text Splitters
11. Embeddings
12. Vector Stores
13. Retrievers
14. RAG
15. Tools
16. Tool Binding
17. AI Agents
18. Agentic AI
