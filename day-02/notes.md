# 🤖 Day 02 — How an LLM Answers

> **Goal:** Understand what happens between a user's prompt and the final response, and learn the difference between a model, training, inference, tools, RAG, and hallucination.

---

## 🧭 Day 02 Learning Map

```text
User Prompt
    ↓
Context + Instructions
    ↓
LLM
    ↓
Predict next token
    ↓
Add token to context
    ↓
Repeat
    ↓
Response
```

Then extend the model with external capabilities:

```text
                    ┌── Web Search
                    ├── Calculator
Question → LLM → Tool → Tool Result → LLM → Answer
                    ├── Code
                    ├── Files
                    └── Databases
```

And for private/current knowledge:

```text
Question
   ↓
Retrieve relevant information
   ↓
Add retrieved context
   ↓
LLM
   ↓
Grounded answer
```

---

# 1. Search Engine vs LLM

These systems can both answer questions, but they work differently.

## 🔎 Search Engine

A simplified flow:

```text
User Query
    ↓
Search Index
    ↓
Find Candidate Pages
    ↓
Rank Results
    ↓
Show Results
```

The search engine primarily helps you **find existing information**.

## 🤖 LLM

A simplified flow:

```text
Prompt
  ↓
Model + Context
  ↓
Next-token generation
  ↓
Response
```

An LLM primarily **generates a sequence of tokens** based on learned patterns and the context supplied at inference time.

### Memory Rule

> **Search engine → retrieve existing information**
>
> **LLM → generate a response**

An AI application can combine both.

---

# 2. How Search Engines Find Information

A simplified search pipeline is:

```text
Web Pages
   ↓
Crawler
   ↓
Index
   ↓
User Query
   ↓
Retrieve Candidate Pages
   ↓
Rank
   ↓
Results
```

Search engines do not magically guarantee truth. A result can be:

- outdated
- misleading
- poorly ranked
- based on an unreliable source

### Verification habit

For important information:

```text
Find source
   ↓
Check publisher
   ↓
Check date
   ↓
Open original source
   ↓
Compare reliable sources
```

---

# 3. How an LLM Generates a Response

The central mechanism is **next-token prediction**.

Suppose the model sees:

```text
The capital of India is
```

The model predicts a likely next token such as:

```text
New
```

then continues from the updated sequence.

The simplified process is:

```text
Prompt
  ↓
Predict next token
  ↓
Append token
  ↓
Predict next token
  ↓
Append token
  ↓
Repeat
```

Eventually the model generates an end condition and the application presents the resulting text.

### Important

The model is not simply retrieving a paragraph from a database and pasting it into the response. It is generating tokens using learned parameters and the context available to it.

---

# 4. What Does an LLM Actually Learn?

During training, the model's parameters are adjusted so that it becomes better at predicting training examples.

A simplified view:

```text
Training Data
     ↓
Learning Process
     ↓
Parameter Updates
     ↓
Trained Model
```

The learned parameters capture patterns involving things such as:

- grammar
- syntax
- style
- facts and associations
- relationships between concepts
- programming patterns
- common language structures

The model is **not simply a traditional database of facts**.

---

# 5. What Are Model Parameters?

A model contains a very large number of learned numerical values called **parameters** or **weights**.

Simplified:

```text
Training Example
      ↓
Model predicts
      ↓
Compare with target
      ↓
Calculate error
      ↓
Update parameters
      ↓
Repeat
```

The parameters encode the learned behavior of the neural network.

### Important distinction

```text
Training
→ changes model parameters

Inference
→ uses the learned parameters to generate output
```

---

# 6. Training vs Inference

This distinction is one of the most important AI interview concepts.

## 🧠 Training

Training is the **learning phase**.

```text
Large Dataset
     ↓
Model
     ↓
Prediction
     ↓
Error / Loss
     ↓
Backpropagation + Optimization
     ↓
Updated Parameters
```

The goal is to improve the model's learned parameters.

## ⚡ Inference

Inference is the **usage phase**.

```text
User Prompt
     ↓
Trained Model
     ↓
Token Generation
     ↓
Response
```

The model normally does not permanently rewrite its parameters after each ordinary user conversation.

---

# 7. Knowledge Cutoff / Knowledge Boundary

A model's learned internal knowledge is tied to its training.

That means current information may not be available from the model's internal parameters alone.

```text
Training Data
      ↓
Learned Parameters
      ↓
Model Knowledge

Current External Information
      ↓
Needs retrieval / tools / fresh data
```

### Important

A model's internal knowledge and its ability to access external information are different things.

---

# 8. Base Model vs AI Assistant

An AI assistant is often much more than the underlying neural network.

A simplified product stack is:

```text
Base Model
   +
System Instructions
   +
Conversation Context
   +
Safety / Policy
   +
Retrieval
   +
Tools
   +
Application Logic
   ↓
AI Assistant
```

So when you interact with a modern AI product, you are usually interacting with a **system built around a model**, not just an isolated model.

---

# 9. Why Can LLMs Hallucinate?

## Definition

A **hallucination** is an output that appears plausible but is unsupported, incorrect, misleading, or fabricated.

The key rule is:

> **Fluency does not guarantee truth.**

An answer can sound very confident and still be wrong.

---

# 10. Why Hallucinations Can Happen

Several factors can contribute:

### 1. Missing information

The model may not have enough information in its training or current context.

### 2. Ambiguous prompts

If the question has multiple interpretations, the model may choose the wrong one.

### 3. Outdated knowledge

The model may not know a recent event unless fresh information is provided.

### 4. Pattern completion

The model is optimized to generate likely continuations, not to guarantee that every generated statement is factual.

### 5. False assumptions

If the prompt contains a false premise, the model may build an answer on top of it.

### 6. Unsupported details

The model can produce names, citations, numbers, or references that sound reasonable but are not real or accurate.

---

# 11. Common Types of Hallucination

| Type | Example |
|---|---|
| Invented fact | Making up an event or person |
| Fake citation | Producing a citation that does not exist |
| False precision | Giving a very specific number without evidence |
| Outdated information | Presenting old information as current |
| Wrong combination | Combining two true facts into a false claim |
| Unsupported explanation | Giving a confident explanation without evidence |

---

# 12. The Confidence Illusion

A model can sound certain even when it is incorrect.

```text
Confident wording
      ≠
Factual certainty
```

For high-stakes or changing information, use verification:

```text
AI answer
   ↓
Ask for evidence
   ↓
Check source
   ↓
Verify date
   ↓
Compare reliable sources
```

---

# 13. Why Might an AI Say "I Don't Know"?

An AI assistant may decline to answer or state uncertainty for several reasons:

- insufficient information
- system instructions
- safety constraints
- weak confidence or weak learned patterns
- unavailable tools
- ambiguous user request
- product-level behavior designed to reduce unsupported answers

The phrase itself does not prove that the model has human-like self-awareness. It can be the result of learned behavior and system instructions.

---

# 14. Tools Extend an AI System

A model can be connected to external tools.

Examples include:

- web search
- calculator
- code execution
- weather
- location
- calendar
- email
- file retrieval
- databases

A simplified tool-use loop is:

```text
User Question
     ↓
    LLM
     ↓
Decide a tool is useful
     ↓
   Tool Call
     ↓
  Tool Result
     ↓
    LLM
     ↓
Final Answer
```

### Example

```text
User: What is 17% of 840?

LLM
 ↓
Calculator tool
 ↓
Result
 ↓
LLM explains answer
```

The model itself does not magically become a calculator because it can talk about arithmetic. A connected tool can provide exact computation.

---

# 15. What Is RAG?

**RAG = Retrieval-Augmented Generation**.

It combines:

```text
Retrieval
   +
Generation
```

A simplified pipeline:

```text
User Question
      ↓
Retrieve Relevant Information
      ↓
Add Retrieved Context
      ↓
LLM
      ↓
Generated Answer
```

---

# 16. Why Do We Need RAG?

A model's internal training knowledge may be:

- incomplete
- outdated
- not specific to your organization
- missing private company information

RAG allows an application to retrieve relevant external material at query time.

### Example: Company HR Assistant

```text
Company Policies
      ↓
Document Processing
      ↓
Search / Retrieval Index
      ↓
Employee Question
      ↓
Relevant Policy Sections
      ↓
LLM
      ↓
Answer grounded in company policy
```

---

# 17. RAG vs Fine-Tuning

These are often confused.

## RAG

Use when the model needs **external or changing information**.

```text
Question
 ↓
Retrieve data
 ↓
Put data in context
 ↓
Generate answer
```

## Fine-Tuning

Use when you want to change or specialize aspects of **model behavior** by further training on examples.

```text
Examples
 ↓
Further training
 ↓
Updated model behavior
```

### Memory Rule

> **RAG changes the information available at inference time.**
>
> **Fine-tuning changes learned model behavior/parameters.**

They can also be used together.

---

# 18. RAG Does Not Guarantee Truth

RAG can improve grounding, but it is not automatically correct.

Possible failure points:

```text
Bad document
   ↓
Bad chunking
   ↓
Bad retrieval
   ↓
Wrong context
   ↓
LLM
   ↓
Wrong answer
```

So a good RAG system must also think about:

- document quality
- chunking
- retrieval quality
- ranking
- metadata filters
- citations / source attribution
- evaluation

---

# 19. Context Is More Than the User's Message

A modern model can receive a larger context containing multiple sources.

A simplified view is:

```text
System Instructions
        +
Conversation History
        +
Current User Prompt
        +
Retrieved Documents
        +
Tool Results
        ↓
Model Context
        ↓
Generation
```

This is why the same model can behave differently depending on the context supplied to it.

---

# 20. Model vs Tool vs Retrieval

This distinction is important.

| Component | Main job |
|---|---|
| Model | Understand/generate based on learned patterns |
| Tool | Perform an external operation |
| Retrieval | Find relevant external information |
| RAG system | Combine retrieval with generation |
| Assistant | Orchestrate model, context, tools, safety, and product logic |

---

# 🧠 Day 02 Mental Model

Keep this picture in mind:

```text
                 ┌───────────────┐
                 │ User Prompt   │
                 └───────┬───────┘
                         ↓
                 ┌───────────────┐
                 │    Context    │
                 │ instructions  │
                 │ history       │
                 │ retrieved data│
                 │ tool results  │
                 └───────┬───────┘
                         ↓
                  ┌─────────────┐
                  │     LLM     │
                  └──────┬──────┘
                         ↓
                Predict next token
                         ↓
                  Add to context
                         ↓
                      Repeat
                         ↓
                  Final response
```

External capabilities fit around the model:

```text
                         ┌───────────┐
                         │ Web       │
                         ├───────────┤
                         │ Calculator│
                         ├───────────┤
                         │ Code      │
                         ├───────────┤
                         │ Database  │
                         └─────┬─────┘
                               ↓
Question → LLM → Tool/Retrieval → Result → LLM → Answer
```

---

# ⚡ Quick Revision

### LLM
A neural network language model that generates text token by token using learned parameters and context.

### Training
The learning phase where model parameters are optimized using training data.

### Inference
Using the trained model to generate an output for an input.

### Hallucination
A plausible-looking but unsupported or incorrect output.

### Tool
An external capability the AI system can invoke to perform an operation or obtain information.

### RAG
Retrieval-Augmented Generation: retrieve relevant external information and provide it to the model during generation.

### Base Model
The underlying trained model.

### AI Assistant
The larger system built around the model, including instructions, context, tools, retrieval, safety, and application logic.

---

# 🎯 Interview Questions

## Beginner

### 1. What is an LLM?

An LLM is a large neural language model trained on large amounts of data to learn language patterns and generate text.

### 2. What is the difference between training and inference?

Training updates the model's parameters. Inference uses those learned parameters to produce outputs for new inputs.

### 3. What is next-token prediction?

It is the process of predicting the next token based on the preceding tokens and available context, repeated until the response is generated.

---

## Intermediate

### 4. Why can an LLM hallucinate?

Because fluent generation does not guarantee factual verification. Missing information, ambiguous prompts, outdated knowledge, false assumptions, and unsupported pattern completion can all contribute.

### 5. What is RAG?

RAG retrieves relevant external information at query time and supplies it to the LLM so the answer can be generated using that context.

### 6. Why use tools with an LLM?

Tools allow the system to perform operations that are better handled externally, such as exact calculations, web retrieval, code execution, or database access.

---

## Advanced

### 7. Is RAG the same as fine-tuning?

No. RAG changes the information supplied at inference time. Fine-tuning updates the model through additional training to change or specialize learned behavior.

### 8. Is the model itself the same thing as an AI assistant?

No. An AI assistant can include the model plus system instructions, context management, tools, retrieval, safety mechanisms, and application logic.

### 9. Why does a tool sometimes improve reliability?

A specialized tool can perform an operation directly—for example exact arithmetic or fetching current documents—instead of relying only on the model's learned patterns.

### 10. Can RAG completely eliminate hallucinations?

No. Retrieval quality and source quality can still be poor, and the model can still interpret or generate incorrectly. RAG improves grounding but does not guarantee correctness.

---

# 📝 Practice Questions

Try answering these without looking at the notes:

1. Explain the difference between a search engine and an LLM.
2. Explain next-token prediction to a beginner.
3. What is the difference between model parameters and context?
4. Why is training different from inference?
5. Why can an LLM be confident and still be wrong?
6. Explain tool use with a simple example.
7. Explain RAG in one sentence.
8. Compare RAG and fine-tuning.
9. Why does an AI assistant need more than just a model?
10. Draw the complete request → retrieval/tool → model → response flow.

---

# ✅ Day 02 Completion Checklist

- [ ] Search engine vs LLM
- [ ] Next-token generation
- [ ] Model parameters
- [ ] Training vs inference
- [ ] Knowledge boundary
- [ ] Base model vs assistant
- [ ] Hallucination
- [ ] Confidence illusion
- [ ] Tool use
- [ ] RAG
- [ ] RAG vs fine-tuning
- [ ] Context composition
- [ ] Interview questions
- [ ] Practice questions
