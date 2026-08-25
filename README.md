# 🤖 AI Fundamentals — Days 1–4

> A simple, visual learning path from **AI history → Machine Learning → Deep Learning → Transformers → LLMs → Tokens → Embeddings → RAG → Agentic AI**.
>
> These notes are based on the four study documents and rewritten for easier understanding, revision, and interview preparation.

## 🧭 The 4-Day Journey

```text
DAY 1
AI Evolution
    ↓
AI → ML → Deep Learning → Transformers → LLMs
    ↓
Generative AI → Multimodal AI → Agentic AI

DAY 2
How an LLM answers
    ↓
Prompt → Context → Next-token generation → Response
    ↓
Training / Inference / Hallucination / Tools / RAG

DAY 3
How text enters an LLM
    ↓
Text → Tokenizer → Tokens → Token IDs
    ↓
BPE → Vocabulary → Context Window

DAY 4
How AI represents meaning
    ↓
Token ID → Embedding → Context + Position
    ↓
Semantic Similarity → Cosine Similarity → Applications
```

---

# 📘 DAY 1 — Evolution of AI

## 1. What is Artificial Intelligence?

**AI (Artificial Intelligence)** is the field of building systems that perform tasks that normally require human-like intelligence.

Examples:

- Understanding language
- Recognizing images
- Making predictions
- Solving problems
- Recommending content
- Generating text, images, audio or code
- Planning and decision-making

### Big picture

```text
AI
└── Machine Learning
    └── Deep Learning
        └── Transformers
            └── Many modern LLMs
```

## 2. Turing Test — 1950

Alan Turing proposed the **Imitation Game**, commonly called the Turing Test.

```text
             Human evaluator
                   │
          ┌────────┴────────┐
          ▼                 ▼
       Human             Machine
```

The evaluator communicates with both without knowing which is the machine. If the evaluator cannot reliably tell the difference, the machine is considered to have passed.

**Important:** Passing the test is evidence of human-like conversational behavior; it does not prove consciousness.

## 3. John McCarthy and the Birth of AI as a Field

John McCarthy is credited with coining the term **Artificial Intelligence** in the 1950s. The 1956 Dartmouth workshop is another major milestone in the formal development of AI research.

## 4. AI Winter

An **AI winter** is a period when AI funding, enthusiasm, expectations and progress decline.

```text
High expectations
      ↓
Technology cannot deliver
      ↓
Disappointment
      ↓
Less funding / interest
      ↓
AI winter
```

There were multiple AI winters rather than one single continuous period.

## 5. Rule-Based / Symbolic AI

The computer is given explicit human-written rules.

```text
IF condition
THEN action
```

Example:

```text
IF suspicious email pattern
THEN increase spam score
```

### Main limitation

Real-world problems create huge numbers of combinations. Writing every possible rule becomes difficult to maintain.

That problem helped motivate the move toward **Machine Learning**.

## 6. IBM Deep Blue — 1997

IBM's Deep Blue defeated chess champion Garry Kasparov.

**Why it mattered:** It showed how search, algorithms and computing power could produce extremely strong performance in a complex domain.

**Important:** Deep Blue was not a modern LLM.

## 7. Machine Learning

**Machine Learning** learns useful patterns from examples/data rather than relying only on manually written rules.

### Traditional approach

```text
Human writes rules + Data
          ↓
       Program
          ↓
        Output
```

### ML approach

```text
Data + Examples
      ↓
 Learning algorithm
      ↓
   Learned model
      ↓
    Prediction
```

Example:

```text
Cat images + Dog images
          ↓
       Training
          ↓
   Learned patterns
          ↓
New image → Cat / Dog
```

## 8. Deep Learning

**Deep Learning** is a subset of ML that uses multi-layer artificial neural networks.

```text
Machine Learning
      ↓
Neural Networks
      ↓
Many layers
      ↓
Deep Learning
```

Deep networks can automatically learn useful representations/features from data.

## 9. Computer Vision — ImageNet & AlexNet

**ImageNet** became an important large-scale image dataset/benchmark.

**AlexNet (2012)** produced a major deep-learning breakthrough in image recognition and helped accelerate the deep-learning revolution.

## 10. NLP Evolution

```text
Bag of Words
     ↓
N-grams
     ↓
RNN
     ↓
LSTM
     ↓
Transformers
```

### Bag of Words

Converts words to numbers, but largely ignores word order and context.

### N-grams

Captures short word sequences, so it gets some local context, but struggles with long-range relationships.

### RNN

Processes a sequence step by step and carries previous information forward. Long-term dependencies are still difficult.

### LSTM

Improves RNNs with mechanisms for retaining important information longer, but remains sequential.

### Transformer

Uses **attention** to model relationships between tokens and supports efficient parallel processing during training.

## 11. Transformers — 2017

The 2017 **"Attention Is All You Need"** paper introduced the Transformer architecture.

### Self-Attention

The model can examine how relevant different tokens are to one another.

```text
Token A ─────┐
Token B ─────┼──→ Attention → Contextual relationships
Token C ─────┘
```

### Why Transformers changed AI

- Better long-range context handling
- Parallel processing during training
- Efficient scaling to large models
- Foundation for many modern language models

## 12. Large Language Models (LLMs)

An **LLM** is a large neural-network language model trained on very large amounts of data so it can learn complex language patterns.

Common capabilities:

- Text generation
- Summarization
- Translation
- Question answering
- Coding
- Classification
- Transformation of text

## 13. Generative AI

Generative AI creates new content.

```text
Traditional AI:
Input → Label / Prediction

Generative AI:
Input → New content
```

Possible outputs:

- Text
- Code
- Images
- Audio
- Video

## 14. ChatGPT Moment — 2022

ChatGPT's public release in November 2022 helped make conversational generative AI widely accessible and accelerated public/industry interest.

Important concepts around assistant systems include:

- Conversation
- Instruction following
- RLHF
- Context/memory features
- Safety/alignment

## 15. Multimodal AI

Multimodal AI works with more than one type of data.

```text
Text ─────┐
Image ────┤
Audio ────┼──→ Multimodal AI
Video ────┤
Documents ┘
```

## 16. Where AI Is Going

### Agentic AI

```text
Goal
 ↓
Plan
 ↓
Use tools
 ↓
Observe result
 ↓
Adjust
 ↓
Complete task
```

### Other major directions

- Multimodal AI
- Multi-agent orchestration
- Reasoning-focused models
- RAG
- Tool use
- Emerging agent/tool protocols
- Robotics
- AI adoption across industries

---

# 🧠 DAY 2 — How an LLM Answers

## 17. Search Engine vs LLM

### Search Engine

```text
Question
  ↓
Search index
  ↓
Find relevant documents
  ↓
Rank
  ↓
Results
```

### LLM

```text
Prompt
  ↓
Learned patterns + context
  ↓
Generate tokens
  ↓
Response
```

**Memory line:**

> Search engine = **Retrieve** 🔍  |  LLM = **Generate** 🤖

## 18. How Search Engines Find Information

```text
Website
 ↓
Crawler
 ↓
Index
 ↓
User query
 ↓
Find relevant pages
 ↓
Rank
 ↓
Results
```

Search results are not automatically true. They may be outdated, misleading or imperfectly ranked.

Good verification habits:

1. Trace back to the original source
2. Check who published it
3. Check the date
4. Compare multiple reliable sources

## 19. How LLMs Generate Responses

The core mechanism is **next-token generation**.

```text
Prompt
  ↓
Predict next token
  ↓
Add token to context
  ↓
Predict next token
  ↓
...
  ↓
Final response
```

This is not random guessing. The model uses patterns learned during training and the context available at inference time.

## 20. What Does an LLM Learn?

A trained neural network contains a huge number of learned numerical **parameters/weights**.

```text
Training data
    ↓
Learning
    ↓
Adjust parameters
    ↓
Trained model
```

The model learns patterns involving things such as:

- Grammar
- Programming
- Facts
- Language structure
- Relationships between concepts
- People, places and events

It is not simply a traditional database of facts.

## 21. Knowledge Cutoff

A model has limits related to the information available during training.

**Important:** A deployed model does not normally rewrite its internal weights after every conversation.

```text
Training
   ↓
Learned knowledge
   ↓
Deployed model

Current external information
   ↓
Need search / tool / retrieval
```

## 22. Base Model vs AI Assistant

```text
Base model
   + System instructions
   + Conversation context
   + Safety
   + Retrieval
   + Tools
   + Product logic
   ↓
AI Assistant
```

A chatbot product can therefore be much more than just the underlying model.

## 23. Training vs Inference

### Training

**Learning**

```text
Large datasets
 ↓
Adjust model parameters
 ↓
Learn patterns
```

### Inference

**Using what was learned**

```text
Prompt
 ↓
Trained model
 ↓
Generated answer
```

## 24. Hallucination

A **hallucination** is an output that sounds plausible but is unsupported, incorrect, misleading or fabricated.

> **Fluency ≠ Truth**

### Why can hallucinations happen?

- Insufficient information
- Ambiguous prompt
- Outdated knowledge
- False assumptions
- Unreliable learned patterns
- Generation is probabilistic
- The system is designed to generate answers, not act as a perfect truth checker

### Common types

- Invented facts
- Invented citations
- Incorrect combinations
- Outdated facts
- False precision
- Broken reasoning

## 25. Why Might an AI Say “I Don't Know”?

Possible influences include:

- Assistant training
- System instructions
- Weak learned patterns
- Safety rules
- Tool requirements
- Prompt wording

## 26. The Confidence Illusion

A model can sound certain even when the answer is wrong.

```text
Confident wording
      ≠
Factual certainty
```

For important information:

```text
Ask for evidence
 ↓
Check sources
 ↓
Verify
```

## 27. Tools Extend AI

Tools can provide capabilities beyond the model's internal learned patterns.

Examples:

- Web search
- Calculator
- Code execution
- Weather
- Location
- Calendar
- Email
- Databases
- Files/internal documents

```text
Question
 ↓
Model
 ↓
Tool
 ↓
Tool result
 ↓
Model
 ↓
Answer
```

## 28. RAG — Retrieval-Augmented Generation

RAG combines **retrieval + generation**.

```text
Question
 ↓
Retrieve relevant information
 ↓
Provide context
 ↓
LLM
 ↓
Answer
```

### Example

```text
Company documents
 ↓
Split into chunks
 ↓
Index/retrieve
 ↓
Relevant policy section
 ↓
LLM
 ↓
Employee answer
```

RAG can improve grounding, but it does **not** guarantee that every answer is correct.

## 29. Self-Awareness — Source Boundary

The Day 2 source begins this topic using **training, context, system and tools**, but the final part of that source is incomplete.

So there is **not enough source material to make a complete claim about self-awareness**.

---

# 🔤 DAY 3 — Tokens, Tokenization & Context

## 30. Why Does an LLM Need Tokens?

```text
Human text
   ↓
Tokenizer
   ↓
Tokens
   ↓
Token IDs
   ↓
Model
```

The model works with numerical representations of these token pieces.

## 31. What Is a Token?

A **token is a piece of text defined by a tokenizer**.

A token can be:

- A whole word
- Part of a word
- Punctuation
- Whitespace-related piece
- Symbol
- Special/control piece
- Code fragment

### Critical rule

> **Token ≠ Word**

## 32. What Is a Tokenizer?

A **tokenizer** is the program/algorithm/library that converts text into tokens.

```text
Sentence
 ↓
Tokenizer
 ↓
Token pieces
```

## 33. What Is a Vocabulary?

The **vocabulary** is the collection of token pieces that a tokenizer knows how to represent.

Simplified:

```text
"the"  → ID 10
"AI"   → ID 11
"love" → ID 12
```

## 34. What Is a Token ID?

A **token ID** is the numeric identifier associated with a token in that tokenizer's vocabulary.

### Important distinction

```text
Token    = text piece
Token ID = numeric identifier
```

The ID itself does **not** mean the semantic meaning of the word.

## 35. Subword Tokenization

Whole-word vocabulary is impractical because language has an enormous number of possible words.

Subword tokenization solves this by reusing pieces.

```text
unbreakable
 ↓
un + break + able
```

The exact split depends on the tokenizer.

## 36. BPE — Byte Pair Encoding

BPE is a tokenization method that repeatedly merges frequently occurring neighboring pieces.

```text
Small pieces
    ↓
Frequent neighboring pair
    ↓
Merge
    ↓
Useful subword token
```

The source specifically mentions BPE as part of its tokenization notes.

## 37. Why Vocabulary Quality Matters

A useful vocabulary can represent common text efficiently.

```text
Good token piece
     ↓
Fewer tokens
     ↓
Better token efficiency
```

But:

> **Bigger vocabulary ≠ automatically better model**

## 38. Token Boundaries ≠ Meaning Boundaries

Tokenization is a representation choice.

If:

```text
unbelievable
 ↓
un + believ + able
```

that does not mean the tokenizer is saying there are three independent semantic concepts.

## 39. Different Languages → Different Token Counts

Token count depends on:

- language
- script
- vocabulary
- word structure
- tokenizer design

Therefore two equivalent sentences in different languages may use different numbers of tokens.

## 40. Tokenization Fertility

**Tokenization fertility** describes how many tokens are produced for a text unit.

```text
Text unit
 ↓
Tokenizer
 ↓
Token count
 ↓
Fertility
```

Higher fertility = more splitting.

Lower fertility = fewer tokens.

## 41. Special Tokens / Special Cases

Tokenization can treat these differently:

- Whitespace
- Capitalization
- Punctuation
- Symbols
- Emoji
- Code syntax

**Important:** one visible emoji does not necessarily equal one token.

## 42. Context Window

A **context window** is the maximum amount of tokenized information a model can work with as context for a request.

Think:

> **Context window = model's working desk**

It can contain things such as:

```text
System instructions
+
Conversation history
+
Current prompt
+
Retrieved documents
+
Tool results
```

## 43. What Happens When Context Fills?

Depending on the system, it may:

- Truncate old content
- Summarize old content
- Retrieve relevant history
- Use memory/RAG
- Manage input/output budgets

### Important

> **Larger context window ≠ perfect memory**

---

# 🧮 DAY 4 — Embeddings & Meaning

## 44. Token ID vs Meaning

Suppose:

```text
Dog → 8123
Cat → 123
```

The numbers alone do not tell us that dogs and cats are related.

```text
Token ID
  ↓
Identifier

Embedding
  ↓
Learned representation
```

## 45. Vectorization

**Vectorization** means converting information into numerical vectors so mathematical operations can be performed.

```text
Information
 ↓
Numbers
 ↓
Vector
```

Examples:

```text
[2, 5]

[3.8, 6, 7]

[0.12, -3.5, 4.20, -1.24, ...]
```

## 46. What Is an Embedding?

> **An embedding is a learned numerical vector representation of an item that captures useful relationships with other items.**

Example:

```text
Dog
 ↓
Embedding model
 ↓
[0.12, -0.43, 0.78, 0.21, ...]
```

### Important

An embedding isn't a dictionary where:

```text
Dimension 1 = animal
Dimension 2 = size
Dimension 3 = color
```

The useful information is generally distributed across many dimensions.

## 47. What Is a Dimension?

If the vector is:

```text
[0.7, -0.4, 0.8]
```

there are **3 dimensions**.

A dimension is simply one numerical position in the vector.

### More dimensions

```text
More dimensions
      ↓
Potentially richer patterns
      ↓
More storage + computation
```

More dimensions are not automatically better.

## 48. How Are Embeddings Learned?

Nobody manually assigns semantic meaning to each dimension.

Instead:

```text
Training data
     ↓
Patterns
     ↓
Learning
     ↓
Adjusted parameters/representations
     ↓
Useful embedding space
```

Related concepts can become neighbors because the training data repeatedly places them in related contexts.

## 49. Semantic Similarity

**Semantic similarity** measures how close two pieces of text are in meaning.

Example:

```text
“How do I centre a div?”

“How can I align an HTML element in the middle of its parent?”
```

Different wording.

Similar meaning.

Embedding-based retrieval can capture this broader relationship.

## 50. Embedding Space

Imagine each vector as a point in a huge mathematical space.

```text
        Dog ●
           \
            ● Cat

                    ● Car
```

Related concepts can form neighborhoods.

Real embedding spaces may have hundreds or thousands of dimensions.

## 51. Cosine Similarity

**Cosine similarity** compares vectors mainly by their direction/angle.

```text
A →
B →

Same direction → high similarity
```

Approximate interpretation:

| Direction | Similarity |
|---|---:|
| Same direction | close to +1 |
| About 90° | around 0 |
| Opposite direction | close to -1 |

Formula:

```text
cos(A,B) = (A · B) / (||A|| × ||B||)
```

Where:

- `A · B` = dot product
- `||A||` = magnitude of A
- `||B||` = magnitude of B

### Key point

Two vectors can have different lengths and still have high cosine similarity if their directions are similar.

## 52. Similarity ≠ Truth

This is extremely important.

```text
High semantic similarity
        ≠
Truth
```

Example:

> "JavaScript is the best language."

and

> "JavaScript is the worst language."

They can be semantically similar because both discuss JavaScript and opinions about it.

Similarity doesn't verify:

- truth
- quality
- intent
- safety

## 53. Visualizing Embeddings

We cannot directly visualize hundreds/thousands of dimensions.

So we can reduce dimensions:

```text
High-dimensional vectors
        ↓
Dimensionality reduction
        ↓
2D / 3D
        ↓
Visual clusters
```

The visualization is only an approximation and can lose information.

Your Day 4 source mentions **TensorFlow Projector** for exploring these relationships.

## 54. Token Embedding

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Token embeddings
```

Example conceptually:

```text
I          → [0.12, -0.32, 0.08, ...]
love       → [0.41, 0.73, -0.12, ...]
JavaScript → [...]
```

These values are model-specific and illustrative.

## 55. Token Embedding vs Text Embedding

| | Token embedding | Text embedding |
|---|---|---|
| Represents | One token | Larger text unit |
| Example | `JavaScript` | `I love JavaScript` |
| Granularity | Small | Larger |
| Typical use | Model representation | Search/retrieval/similarity |

## 56. Why Position Matters

Consider:

> Dog bites man.

and:

> Man bites dog.

Same words.

Different order.

Different meaning.

Therefore the model needs information about **where the token appears**.

```text
Token representation
      +
Position
      ↓
Order-aware representation
```

## 57. Static vs Contextual Representation

### Static representation

One fixed representation for the word regardless of sentence.

Problem:

> "I deposited money in the bank."

vs

> "We sat on the bank of the river."

The word `bank` has different meanings.

### Contextual representation

The representation can change depending on surrounding words.

```text
bank + money + deposit
        ↓
Finance context

bank + river + water
        ↓
River context
```

## 58. How Modern LLMs Handle Context

Conceptually:

```text
Initial token representation
        ↓
Process surrounding context
        ↓
Context-sensitive representation
```

This is an important connection between **Day 1 Transformers** and **Day 4 embeddings**.

Transformers don't just look at isolated token identities. They build context-sensitive representations by processing relationships between tokens.

## 59. Bias in Embeddings

Human-created training data can contain bias.

Therefore:

```text
Biased data
   ↓
Learned patterns
   ↓
Potentially biased representations
```

Embeddings do not automatically know which associations humans consider undesirable.

## 60. Where Embeddings Are Used

### Semantic Search

```text
Query
 ↓
Query embedding
 ↓
Compare document embeddings
 ↓
Most similar results
```

### Recommendation Systems

```text
User/item/content
 ↓
Vectors
 ↓
Find related vectors
 ↓
Recommendations
```

### Clustering

```text
Many items
 ↓
Embeddings
 ↓
Similarity
 ↓
Clusters
```

### RAG

```text
Documents
 ↓
Chunks
 ↓
Embeddings
 ↓
Vector index

User question
 ↓
Query embedding
 ↓
Similarity search
 ↓
Relevant chunks
 ↓
LLM
 ↓
Answer
```

### Duplicate Detection

Find texts with similar meaning even when wording differs.

### Classification

Use embeddings as useful representations for downstream classifiers.

### Multimodal Embeddings

Represent information from different modalities such as:

- text
- image
- video

---

# 🔗 THE MOST IMPORTANT CONNECTION ACROSS ALL 4 DAYS

This is the part you should truly understand rather than memorize.

```text
                         AI
                          ↓
                         ML
                          ↓
                   Deep Learning
                          ↓
                    Transformers
                          ↓
                         LLM
                          ↓
              ┌───────────┴───────────┐
              │                       │
          Your input              Model knowledge
              │                       │
              ▼                       │
            Text                      │
              ↓                       │
         Tokenizer                    │
              ↓                       │
           Tokens                     │
              ↓                       │
         Token IDs                    │
              ↓                       │
        Embeddings                    │
              ↓                       │
     Position + Context               │
              ↓                       │
     Contextual representation        │
              └──────────┬────────────┘
                         ↓
                     Transformer
                         ↓
                Next-token prediction
                         ↓
                     Response
```

And if the model needs outside information:

```text
User question
      ↓
Need current / private / external information
      ↓
Search / Database / Files / RAG / Tool
      ↓
Relevant information
      ↓
LLM context
      ↓
Generated answer
```

---

# ⭐ 60-SECOND INTERVIEW EXPLANATION

> **"An LLM is a large neural-network language model, commonly based on the Transformer architecture. When we give it text, a tokenizer breaks the text into tokens and maps them to token IDs. Token IDs are only identifiers, so the model uses learned numerical representations called embeddings. The model also needs positional and contextual information because the same token can mean different things in different sentences. During inference, the Transformer processes this context and generates the response through next-token prediction. If the application needs current or external information, tools or RAG can retrieve that information and add it to the model's context before generation."**

---

# 🎯 FINAL REVISION MAP

```text
AI
│
├── ML
│   └── Deep Learning
│       └── Transformers
│           └── LLM
│
├── Input side
│   ├── Tokenizer
│   ├── Tokens
│   ├── Token IDs
│   └── Embeddings
│
├── Understanding side
│   ├── Position
│   ├── Context
│   ├── Attention
│   └── Contextual representations
│
├── Generation side
│   └── Next-token prediction
│
└── External knowledge / capability
    ├── Search
    ├── Tools
    ├── Files
    ├── Databases
    └── RAG
```

## 🧠 If you remember only 15 things

1. **AI** is the broad field.
2. **ML** learns patterns from data.
3. **Deep Learning** uses multi-layer neural networks.
4. **Transformers** use attention to model relationships between tokens.
5. **LLMs** are large language models built from learned patterns.
6. **Training** = learning.
7. **Inference** = using what was learned.
8. **Token** = piece of text.
9. **Token ID** = numeric identifier for a token.
10. **Embedding** = learned numerical vector representation.
11. **Context** changes how tokens can be represented/interpreted.
12. **Cosine similarity** compares vector direction.
13. **Similarity does not prove truth.**
14. **RAG** = retrieve external information + generate an answer.
15. **Agentic AI** = AI that can plan, use tools, act and iterate toward a goal.

---

## 📚 Source coverage

These notes consolidate the four uploaded study documents: AI evolution, LLM generation/inference/hallucination/tools/RAG, tokenization/context windows, and embeddings/semantic similarity/applications. The source PDFs include handwritten diagrams and examples; those concepts have been converted into clean text-based visuals here. The Day 2 self-awareness section is incomplete in the source, so no unsupported conclusion is added.
