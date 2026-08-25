# 🤖 AI Learning Roadmap

> Day-by-day AI learning path. Each day follows: **Deep Learning → Practice → Interview Q&A → Quick Revision → GitHub notes**.

## 🧭 Journey

```text
DAY 01  AI Foundations & Evolution
   ↓
DAY 02  How LLMs Work
   ↓
DAY 03  Tokenization & Context
   ↓
DAY 04  Embeddings & Semantic Meaning
   ↓
DAY 05  Neural Networks & Training
   ↓
DAY 06  Transformers
   ↓
DAY 07  Attention & Self-Attention
   ↓
DAY 08  LLM Architecture & Inference
   ↓
DAY 09  Prompt Engineering
   ↓
DAY 10  RAG Fundamentals
   ↓
DAY 11  Embeddings + Vector Databases
   ↓
DAY 12  RAG Retrieval & Quality
   ↓
DAY 13  Function Calling & Tools
   ↓
DAY 14  AI Agents
   ↓
DAY 15  Agentic Workflows & Memory
   ↓
DAY 16  Evaluation, Hallucination & Guardrails
   ↓
DAY 17  AI Application Architecture
   ↓
DAY 18  RAG Project
   ↓
DAY 19  Agent Project
   ↓
DAY 20  Interview + System Design
```

---

## 📅 Progress Tracker

| Day | Topic | Status |
|---|---|---|
| 01 | AI Foundations & Evolution | ✅ Completed |
| 02 | How LLMs Work | ✅ Completed |
| 03 | Tokenization & Context | ✅ Completed |
| 04 | Embeddings & Semantic Meaning | ✅ Completed |
| 05 | Neural Networks & Training | ⬜ |
| 06 | Transformers | ⬜ |
| 07 | Attention & Self-Attention | ⬜ |
| 08 | LLM Architecture & Inference | ⬜ |
| 09 | Prompt Engineering | ⬜ |
| 10 | RAG Fundamentals | ⬜ |
| 11 | Embeddings + Vector Databases | ⬜ |
| 12 | RAG Retrieval & Quality | ⬜ |
| 13 | Function Calling & Tools | ⬜ |
| 14 | AI Agents | ⬜ |
| 15 | Agentic Workflows & Memory | ⬜ |
| 16 | Evaluation & Guardrails | ⬜ |
| 17 | AI Application Architecture | ⬜ |
| 18 | RAG Project | ⬜ |
| 19 | Agent Project | ⬜ |
| 20 | Interview + System Design | ⬜ |

---

# 📚 Day-by-Day Topics

## DAY 01 — AI Foundations & Evolution

**Status: ✅ Completed**

- AI definition
- Turing Test
- John McCarthy
- AI winters
- Symbolic / rule-based AI
- IBM Deep Blue
- Machine Learning
- Deep Learning
- ImageNet / AlexNet
- NLP evolution: BoW → N-grams → RNN → LSTM → Transformer
- Transformers
- LLMs
- Generative AI
- Multimodal AI
- Agentic AI

**Mental model:**

```text
AI → ML → Deep Learning → Transformers → LLMs → Generative / Agentic AI
```

## DAY 02 — How LLMs Work

**Status: ✅ Completed**

- Search engine vs LLM
- Next-token generation
- Model parameters / weights
- Training vs inference
- Knowledge cutoff
- Base model vs AI assistant
- Hallucinations
- Confidence illusion
- Tools
- RAG

**Mental model:**

```text
Prompt → Context → Next token → Add token → Next token → Response
```

## DAY 03 — Tokenization & Context

**Status: ✅ Completed**

- Token
- Tokenizer
- Vocabulary
- Token ID
- Word vs token
- Subword tokenization
- BPE
- Token boundaries
- Tokenization fertility
- Language/token differences
- Special tokens
- Context window

**Mental model:**

```text
Text → Tokenizer → Tokens → Token IDs → Model
```

## DAY 04 — Embeddings & Semantic Meaning

**Status: ✅ Completed**

- Embedding definition
- Token ID vs embedding
- Vector representation
- Dimensions
- Semantic meaning
- Contextual representation
- Positional information
- Cosine similarity
- Semantic search
- Embeddings in RAG

**Mental model:**

```text
Text → Token IDs → Embedding model → Vectors → Similarity / Retrieval
```

## DAY 05 — Neural Networks & Training

**Status: ⬜**

- Neurons
- Weights and biases
- Layers
- Forward propagation
- Activation functions
- Loss
- Gradient descent
- Backpropagation
- Learning rate
- Epochs and batches
- Overfitting / underfitting
- Train / validation / test data

```text
Input → Network → Prediction → Loss → Backpropagation → Update weights → Repeat
```

## DAY 06 — Transformers

**Status: ⬜**

- Transformer architecture
- Encoder vs decoder
- Transformer block
- Self-attention
- Multi-head attention
- Feed-forward network
- Residual connections
- Layer normalization
- Positional information
- Encoder-only / decoder-only / encoder-decoder models

## DAY 07 — Attention & Self-Attention

**Status: ⬜**

- Query, Key, Value
- Attention scores
- Scaling
- Softmax
- Weighted values
- Multi-head attention
- Causal / masked attention
- Relationship between tokens

```text
Q + K → Scores → Softmax → Weights → Weighted V → Context
```

## DAY 08 — LLM Architecture & Inference

**Status: ⬜**

- Decoder-only LLMs
- Transformer blocks
- Logits
- Softmax probabilities
- Autoregressive generation
- Greedy decoding
- Temperature
- Top-k
- Top-p
- KV cache
- Input vs output tokens

## DAY 09 — Prompt Engineering

**Status: ⬜**

- Clear instructions
- Context
- Constraints
- Output formats
- Zero-shot
- Few-shot
- Structured prompts
- Prompt templates
- Prompt injection basics
- Reliable prompting patterns

## DAY 10 — RAG Fundamentals

**Status: ⬜**

- Why RAG
- Retrieval vs generation
- Document ingestion
- Chunking
- Embedding documents
- Vector search
- Retrieval
- Context injection
- Grounded generation

```text
Documents → Chunk → Embed → Store
Question → Embed → Retrieve → Context + Prompt → LLM → Answer
```

## DAY 11 — Vector Databases

**Status: ⬜**

- Vector database
- Vector index
- Similarity search
- Cosine similarity
- Euclidean distance
- Approximate nearest neighbors
- Metadata filtering
- Query vs document embeddings

## DAY 12 — RAG Retrieval & Quality

**Status: ⬜**

- Chunk size
- Chunk overlap
- Metadata
- Top-k
- Similarity thresholds
- Hybrid search
- Reranking
- Query transformation
- Retrieval evaluation
- Grounding
- RAG failure modes

## DAY 13 — Function Calling & Tools

**Status: ⬜**

- Why models need tools
- Tool schemas
- Function calling
- Structured arguments
- Tool execution loop
- Tool results
- Multiple tools
- Tool selection
- Error handling
- External APIs

```text
User → LLM → Tool call → Application executes → Tool result → LLM → Answer
```

## DAY 14 — AI Agents

**Status: ⬜**

- Agent definition
- Agent vs chatbot
- Goals
- Planning
- Tool use
- Observation
- Action
- Feedback loops
- Single-agent systems
- Multi-agent systems

```text
Goal → Plan → Act → Observe → Adjust → Act → Complete
```

## DAY 15 — Agentic Workflows & Memory

**Status: ⬜**

- Short-term memory
- Long-term memory
- Conversation state
- Working memory
- Planning strategies
- ReAct-style workflows
- Tool orchestration
- Human-in-the-loop
- Failure recovery
- Multi-agent coordination

## DAY 16 — Evaluation, Hallucination & Guardrails

**Status: ⬜**

- Accuracy
- Relevance
- Groundedness
- Faithfulness
- Retrieval evaluation
- Hallucination detection
- Prompt injection
- Data leakage
- Output validation
- Guardrails

## DAY 17 — AI Application Architecture

**Status: ⬜**

- Frontend → backend → model
- LLM APIs
- Streaming
- RAG architecture
- Tool calling architecture
- Authentication
- Rate limiting
- Caching
- Observability
- Cost
- Latency
- Production design

```text
User → Frontend → Backend / AI Orchestrator
                         ├─ LLM
                         ├─ RAG / Vector DB
                         ├─ Tools / APIs
                         ├─ Memory
                         └─ Guardrails
```

## DAY 18 — RAG Project

**Status: ⬜**

Build a complete document Q&A system:

- Upload documents
- Extract text
- Chunk
- Embed
- Store vectors
- Retrieve
- Generate answer
- Show sources
- Handle errors
- Evaluate retrieval and answers

## DAY 19 — Agent Project

**Status: ⬜**

Build an agentic application:

- User goal
- Planning/workflow
- Multiple tools
- Tool execution
- Memory/state
- Error recovery
- Structured output
- Evaluation/logging

## DAY 20 — Interview + System Design

**Status: ⬜**

Revise:

- AI fundamentals
- ML vs DL
- Transformers
- Attention
- Tokens
- Embeddings
- LLM inference
- Prompt engineering
- RAG
- Vector databases
- Tool calling
- Agents
- Evaluation
- AI system design

Practice every topic using:

```text
What is it?
   ↓
Why do we need it?
   ↓
How does it work?
   ↓
Example
   ↓
Trade-offs
   ↓
Real-world architecture
```

---

# 🔁 Daily Study Format

Every day we will maintain the same structure:

```text
01. Deep explanation
02. Simple mental model
03. Visual representation
04. Practical examples
05. Common mistakes / traps
06. Interview questions
07. Your answers + corrections
08. Quick revision notes
09. GitHub update
```

> **The README is the high-level tracker. Detailed notes will be added day-by-day so progress stays easy to follow and revise.**
