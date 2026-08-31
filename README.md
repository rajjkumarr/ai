# 🤖 AI Fundamentals — Days 1–5

> A simple, visual learning path from **AI history → Machine Learning → Deep Learning → Transformers → LLMs → Tokens → Embeddings → RAG → Agentic AI**.
>
> The notes are organized for **understanding first, revision second, interview preparation third**. Each day connects to the next.

## 🧭 The Learning Journey

```text
DAY 1 — WHERE AI CAME FROM
AI → ML → Deep Learning → NLP → Transformers → LLMs
                                   ↓
                         Generative / Multimodal / Agentic AI

DAY 2 — HOW AN LLM ANSWERS
Prompt → Context → Next-token generation → Response
                    ↓
          Training / Inference / Hallucination / Tools / RAG

DAY 3 — HOW TEXT ENTERS AN LLM
Text → Tokenizer → Tokens → Token IDs
                    ↓
           Vocabulary / BPE / Context Window

DAY 4 — HOW AI REPRESENTS MEANING
Token ID → Embedding → Context + Position
                    ↓
       Semantic Similarity / Cosine Similarity / Applications

DAY 5 — WHAT HAPPENS INSIDE A TRANSFORMER
Embeddings + Position
        ↓
Self-Attention
        ↓
Residual Connection
        ↓
FFN
        ↓
Repeat many Transformer blocks
        ↓
Logits → Softmax → Next Token
        ↓
Add token → Repeat → Complete response
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

If the evaluator cannot reliably distinguish the machine from the human through conversation, the machine is considered to have passed.

**Important:** Passing the test shows human-like conversational behavior; it does not prove consciousness.

## 3. John McCarthy and the Birth of AI as a Field

John McCarthy is credited with coining the term **Artificial Intelligence** in the 1950s. The 1956 Dartmouth workshop is another major milestone in formal AI research.

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

Humans explicitly write rules.

```text
IF condition
THEN action
```

Example:

```text
IF suspicious email pattern
THEN increase spam score
```

**Main limitation:** Real-world situations create huge numbers of combinations, so manually writing and maintaining every rule becomes difficult.

## 6. IBM Deep Blue — 1997

IBM's Deep Blue defeated chess champion Garry Kasparov.

**Why it mattered:** It demonstrated extremely strong performance in a complex domain using search, algorithms and computing power.

**Important:** Deep Blue was not a modern LLM.

## 7. Machine Learning

**Machine Learning** learns useful patterns from examples/data rather than relying only on manually written rules.

```text
Traditional:
Rules + Data → Program → Output

ML:
Data + Examples → Learning → Model → Prediction
```

## 8. Deep Learning

**Deep Learning** is a subset of ML that uses multi-layer neural networks.

```text
Machine Learning
      ↓
Neural Networks
      ↓
Many layers
      ↓
Deep Learning
```

Deep networks can learn useful representations/features from data.

## 9. Computer Vision — ImageNet & AlexNet

**ImageNet** became an important large-scale image dataset/benchmark.

**AlexNet (2012)** was a major deep-learning breakthrough in image recognition and helped accelerate modern deep learning.

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

Represents words numerically but largely ignores order and full context.

### N-grams

Capture short word sequences and some local context, but struggle with long-range relationships.

### RNN

Processes sequence information step by step and carries information forward. Long-term dependencies remain difficult.

### LSTM

Improves RNN memory with gating mechanisms, but is still sequential.

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

Transformers became the foundation for many modern language models.

## 12. Large Language Models (LLMs)

An **LLM** is a large neural-network language model trained on very large amounts of data so it can learn complex language patterns.

Common capabilities:

- Text generation
- Summarization
- Translation
- Question answering
- Coding
- Classification
- Text transformation

## 13. Generative AI

Generative AI creates new content.

```text
Traditional AI:
Input → Label / Prediction

Generative AI:
Input → New content
```

Possible outputs include text, code, images, audio and video.

## 14. ChatGPT Moment — 2022

ChatGPT's public release in November 2022 helped make conversational generative AI widely accessible and accelerated public/industry interest.

Important surrounding ideas include instruction following, RLHF, conversation/context and safety/alignment.

## 15. Multimodal AI

Multimodal AI works with more than one data type.

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

Other major directions:

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

> Search engine = **Retrieve** 🔍 | LLM = **Generate** 🤖

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

Search results are not automatically true. They can be outdated, misleading or imperfectly ranked.

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

The model is not randomly guessing words. It uses learned patterns and available context.

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

The model learns patterns involving grammar, programming, facts, language structure and relationships.

## 21. Knowledge Cutoff

A model has limits related to information available during training.

A deployed model does not normally rewrite its internal weights after every conversation.

```text
Training → Learned patterns → Deployed model

Current external information → Search / Tool / Retrieval
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

## 23. Training vs Inference

### Training

**Learning / adjusting parameters**

### Inference

**Using the trained model to generate output**

```text
Training:  Data → Learn → Model
Inference: Prompt → Model → Output
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
- Probabilistic generation
- The model is a generator, not a perfect truth checker

### Common types

- Invented facts
- Invented citations
- Incorrect combinations
- Outdated facts
- False precision
- Broken reasoning

## 25. Why Might an AI Say “I Don't Know”?

Possible influences include assistant training, system instructions, weak learned patterns, safety rules, tool requirements and prompt wording.

## 26. Confidence Illusion

```text
Confident wording
      ≠
Factual certainty
```

For important information, ask for evidence and verify it.

## 27. Tools Extend AI

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

RAG can improve grounding but does not guarantee perfect correctness.

## 29. Self-Awareness — Source Boundary

The Day 2 source starts this topic with **training, context, system and tools**, but the final part is incomplete. The source therefore does not support a complete conclusion about self-awareness.

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

The model works with numerical representations of token pieces.

## 31. What Is a Token?

A **token is a piece of text defined by a tokenizer**.

It can be a whole word, part of a word, punctuation, whitespace-related piece, symbol or code fragment.

> **Token ≠ Word**

## 32. Tokenizer, Vocabulary and Token ID

**Tokenizer** = converts text into tokens.

**Vocabulary** = collection of token pieces known to that tokenizer.

**Token ID** = numeric identifier for a token in that vocabulary.

```text
Sentence → Tokenizer → Token pieces → Numeric IDs
```

## 33. Token ID Is Not Meaning

```text
Dog → 8123
Cat → 123
```

The numbers above are IDs. They do not themselves tell the model how related dog and cat are.

## 34. Word vs Character vs Token

- Character = one character/symbol
- Word = human-readable word
- Token = tokenizer-defined piece

A word can become multiple tokens.

## 35. Subword Tokenization

Subword tokenization breaks words into reusable pieces so rare/new words can still be represented.

```text
Rare / new word
        ↓
Known subword pieces
        ↓
Tokens
        ↓
IDs
```

## 36. BPE — Byte Pair Encoding

BPE repeatedly merges frequently occurring neighboring pieces to create useful subword units.

```text
Small pieces
    ↓
Frequent pair
    ↓
Merge
    ↓
Useful subword
```

## 37. Vocabulary and Token Efficiency

A useful vocabulary can reduce token count for some text. But bigger vocabulary is not automatically better.

## 38. Token Boundaries ≠ Meaning Boundaries

A token split is mainly a representation choice; it is not a statement about human concepts.

## 39. Language and Token Count

Different languages and scripts can produce different token counts because tokenization depends on language structure, writing system and vocabulary.

## 40. Tokenization Fertility

**Tokenization fertility** describes how many tokens are produced for a text unit.

```text
Text unit → Tokenizer → Token count → Fertility
```

Higher fertility = more splitting.

## 41. Special Tokens / Special Cases

Whitespace, capitalization, punctuation, symbols, emoji and code can be tokenized differently.

## 42. Context Window

A **context window** is the maximum amount of tokenized information a model can work with for a particular request.

Think:

> **Context window = model's working desk**

Possible context:

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

Different systems can:

- Truncate old content
- Summarize older content
- Retrieve relevant history
- Use memory/RAG
- Manage input/output budgets

A larger context window does not automatically mean perfect memory.

## 44. Day 3 Misconceptions

- One token ≠ one word
- Different models can use different tokenizers
- Token ID ≠ semantic meaning
- One emoji ≠ necessarily one token
- Larger vocabulary ≠ automatically better
- Larger context ≠ perfect memory
- More tokens ≠ automatically better answer

---

# 🧠 DAY 4 — How AI Represents Meaning

## 45. Token IDs Do Not Carry Meaning

```text
Token
 ↓
Token ID
```

The ID identifies a token but is not a semantic representation.

## 46. Vectorization

**Vectorization** is converting information into numerical form so mathematical operations can be performed.

```text
Information → Numbers → Vector → Math
```

Example:

```text
[2, 5]
[3.8, 6, 7]
[0.12, -3.5, 4.20, -1.24, -6.81]
```

## 47. Embeddings

An **embedding** is a learned numerical vector representation of an item that captures useful relationships with other items.

```text
Token / item
     ↓
Learned embedding
     ↓
Vector
     ↓
Relationships
```

## 48. Dimensions

A **dimension** is one numerical position in a vector.

```text
[0.7, -0.4, 0.8]
   ↑     ↑     ↑
 d1    d2    d3
```

Dimensions are learned. Do not assume dimension 1 = “animal” or dimension 2 = “food”. Useful information is distributed across the representation.

## 49. Why Many Dimensions?

More dimensions can provide more capacity to represent complex patterns, but also require more storage and computation.

## 50. Semantic Similarity

**Semantic similarity** measures how close two pieces of text are in meaning.

```text
“How do I centre a div?”
        ≈
“How can I align an HTML element in the middle of its parent?”
```

Embedding-based search can compare broader meaning, not only exact words.

## 51. Cosine Similarity

**Cosine similarity** compares vectors mainly by their direction/angle.

```text
Same direction     → high / close to +1
90° apart          → around 0
Opposite direction → low / close to -1
```

Formula:

```text
cos(A,B) = (A · B) / (||A|| × ||B||)
```

It can remain high when vectors have different lengths but similar directions.

## 52. Similarity Does NOT Mean Truth

```text
Similarity ≠ Truth
```

Two false statements can be semantically similar. Two texts can be close in topic while disagreeing.

Embeddings do not independently verify truth, intent, quality or safety.

## 53. Token Embedding vs Text Embedding

```text
Token embedding → one token
Text embedding  → larger text such as a sentence/document
```

## 54. Position and Order

Token embeddings tell the model **what token** is present. Positional information helps tell the model **where the token appears**.

```text
Token embedding
       +
Position
       ↓
Identity + order
```

## 55. Static vs Contextual Meaning

A static representation can stay fixed for a token. A contextual representation can change based on surrounding text.

Example:

```text
“I deposited money in the bank.”
                    ↓
              financial bank

“We sat on the bank of the river.”
                    ↓
              river bank
```

## 56. How Contextualization Works

```text
Initial token representation
          ↓
Process surrounding context
          ↓
Updated/contextual representation
```

## 57. Bias in Embeddings

Embeddings learn patterns from data. Human-created data can contain stereotypes, historical inequality and other unwanted associations.

```text
Human-created data
       ↓
Learned patterns
       ↓
Embeddings
       ↓
Possible unwanted associations
```

## 58. Embedding Applications

### Semantic Search

```text
Query → Query embedding → Compare document embeddings → Relevant results
```

### Recommendation Systems

Represent users/items/content as vectors and find related items.

### Clustering

```text
Many items → Embeddings → Similarity → Clusters
```

### RAG

```text
Documents → Chunks → Embeddings → Retrieve relevant chunks → LLM
```

### Duplicate Detection

Find texts with similar meaning even when wording differs.

### Classification

Use embeddings as useful representations for downstream classifiers.

### Multimodal Embeddings

Represent information from multiple modalities such as text, images and video.

---

# 🚀 DAY 5 — TRANSFORMER ARCHITECTURE

## 59. First Understand the Goal

Suppose the user gives the model:

> **"The capital of India is"**

The Transformer must help the model produce the next token, such as:

> **"Delhi"**

Then it generates the next token after that, and continues until the response is complete.

### The complete high-level flow

```text
Sentence
   ↓
Tokenizer
   ↓
Tokens
   ↓
Token IDs
   ↓
Embeddings
   ↓
Position information
   ↓
Transformer blocks
   ↓
Final representation
   ↓
Linear layer
   ↓
Logits
   ↓
Softmax
   ↓
Next-token probabilities
   ↓
Choose next token
   ↓
Add token to context
   ↓
Repeat
```

---

## 60. Step 1 — Sentence → Tokens

Input:

> **"The capital of India is"**

Simplified tokens:

```text
The | capital | of | India | is
```

A real tokenizer may split text differently.

## 61. Step 2 — Tokens → Token IDs

Example only:

```text
The      → 52
capital  → 1832
of       → 25
India    → 781
is       → 41
```

So:

```text
[52, 1832, 25, 781, 41]
```

Remember: IDs identify tokens; they do not contain semantic meaning.

## 62. Step 3 — Token IDs → Embeddings

The token IDs are used to look up learned vectors.

```text
India
  ↓
[0.7, 0.9, 0.2, -0.1, ...]
```

Now the model has numerical representations of the tokens.

## 63. Step 4 — Add Position Information

The model also needs order.

```text
The      → position 1
capital  → position 2
of       → position 3
India    → position 4
is       → position 5
```

Conceptually:

```text
Token representation + position information
                   ↓
                input representation
```

The exact positional mechanism varies by architecture.

---

# 64. Step 5 — Enter the Transformer

Now the token representations enter a stack of Transformer blocks.

A simplified block is:

```text
Input
 ↓
Layer Normalization
 ↓
Self-Attention
 ↓
Residual Connection
 ↓
Layer Normalization
 ↓
FFN / MLP
 ↓
Residual Connection
 ↓
Output
```

The exact architecture can vary, but this is the key mental model.

---

# 65. Step 6 — Self-Attention

The main question is:

> **Which other tokens are useful for understanding this token?**

For:

> **The capital of India is**

information from `capital` and `India` can be useful when predicting what comes next.

Conceptually:

```text
The      ↔
capital  ↔
of       ↔
India    ↔
is       ↔
```

The tokens can exchange information through attention.

### Easy definition

> **Self-attention lets tokens look at other tokens in the same sequence and combine useful information.**

---

# 66. Query, Key and Value — Simple Intuition

Attention creates three learned representations:

### Query (Q)

> **What information am I looking for?**

### Key (K)

> **What kind of information do I contain?**

### Value (V)

> **What information should I provide if I am relevant?**

Think of a library:

```text
Your question = Query
Book topic     = Key
Book content   = Value
```

This is an intuition, not a literal conversation between words.

---

# 67. How Q, K and V Are Created

Starting with input representations `X`:

```text
Q = XWQ
K = XWK
V = XWV
```

Where `WQ`, `WK` and `WV` are learned weight matrices.

The important idea:

> The model learns how to transform representations into queries, keys and values.

---

# 68. Attention Scores

The model compares Queries with Keys.

Conceptually:

```text
Query
  ↓
Compare with Keys
  ↓
Attention scores
```

The scores answer:

> **How strongly should this token use information from another token?**

---

# 69. Attention Softmax

The attention scores are scaled and passed through softmax.

```text
QKᵀ
 ↓
Scale by √dₖ
 ↓
Softmax
 ↓
Attention weights
```

The weights can look conceptually like:

```text
Token A → 10%
Token B → 20%
Token C → 70%
```

These numbers tell us how strongly information from each Value should contribute.

### Why divide by √dₖ?

Scaling keeps the attention scores at a useful numerical range and helps training remain stable.

---

# 70. Apply the Weights to Values

The attention weights are applied to the Value vectors.

```text
Attention weights
       ↓
Weighted combination of Values
       ↓
Attention output
```

This is where information from relevant tokens is brought together.

---

# 71. Multi-Head Attention

Instead of one attention operation, Transformers use multiple attention heads.

```text
                Input
                  ↓
       ┌──────────┼──────────┐
       ↓          ↓          ↓
     Head 1     Head 2     Head 3   ...
       ↓          ↓          ↓
   Attention  Attention  Attention
       └──────────┼──────────┘
                  ↓
             Concatenate
                  ↓
          Linear projection
                  ↓
              Output
```

### Why multiple heads?

Different heads can learn different useful patterns/relationships.

Do not assume one fixed human-readable job for every head.

---

# 72. Step 7 — Residual Connection

After attention, the Transformer combines the original representation with the newly processed information.

```text
Original information
        +
New attention information
        ↓
Updated representation
```

Conceptually:

```text
Input ─────────────────────┐
  ↓                        ↓
Attention ───────────────→ ADD
```

Residual/skip connections help information and gradients move through deep networks effectively.

---

# 73. Step 8 — FFN (Feed-Forward Network)

FFN means **Feed-Forward Network** and is also commonly called an **MLP**.

Its job is:

> **Take the representation produced by attention and transform it further.**

### Easy rule

> **Attention = exchange information**
>
> **FFN = process / transform information**

A simplified FFN is:

```text
Input
 ↓
Linear layer
 ↓
Nonlinear activation / gating
 ↓
Linear layer
 ↓
Output
```

The first linear layer often expands the representation, the nonlinear step gives the network more expressive power, and the second linear layer projects it back toward the model dimension.

The FFN generally processes each token position independently using the same learned network. Attention is what mixes information between token positions.

---

# 74. Why Do We Need Nonlinearity?

If we only used linear transformations, the network would have much less ability to model complex relationships.

Language contains complicated relationships involving:

- grammar
- syntax
- references
- semantics
- context
- patterns

The nonlinear part helps the network learn richer transformations.

Modern architectures may use functions/gating such as GELU or SwiGLU; the exact choice depends on the model.

---

# 75. One Complete Transformer Block

```text
                 Input
                   ↓
              LayerNorm
                   ↓
         Multi-Head Attention
                   ↓
            Residual Add
                   ↓
              LayerNorm
                   ↓
                FFN
                   ↓
            Residual Add
                   ↓
                 Output
```

### Remember the jobs

```text
Attention → exchange information
FFN       → transform information
Residual  → preserve + combine information
LayerNorm → stabilize processing
```

---

# 76. Step 9 — Repeat the Transformer Block

One block isn't enough.

```text
Input
 ↓
Transformer Block 1
 ↓
Transformer Block 2
 ↓
Transformer Block 3
 ↓
...
 ↓
Transformer Block N
```

Each block receives the previous representation and transforms it further.

A useful mental model is:

```text
Layer 1 → basic relationships
Layer 2 → richer relationships
Layer 3 → more contextual structure
...
Later layers → increasingly rich representations
```

The real behavior is distributed and more complicated than assigning one human concept to each layer.

---

# 77. Step 10 — Final Representation

After many Transformer blocks, we have rich contextual representations of the sequence.

```text
Tokens
  ↓
Many Transformer blocks
  ↓
Final contextual representations
```

Now the model asks:

> **What token should come next?**

---

# 78. Step 11 — Linear Layer

The final representation is mapped to the vocabulary.

Suppose the vocabulary has 100,000 possible tokens.

The linear layer produces a score for each one.

These raw scores are called **logits**.

Example:

```text
Delhi      → 8.5
Mumbai     → 4.2
London     → 2.1
Paris      → 1.5
banana     → -1.2
...
```

The numbers are illustrative.

### Important

> **Logit = raw score before probability conversion.**

---

# 79. Step 12 — Softmax

Now we need probabilities.

```text
Logits
  ↓
Softmax
  ↓
Probabilities
```

Example:

```text
Delhi      → 90%
Mumbai     → 5%
London     → 2%
Paris      → 1%
...
```

Softmax converts the raw scores into a probability distribution whose values add up to 1.

### Softmax formula

```text
Pᵢ = eᶻⁱ / Σⱼ eᶻʲ
```

You don't need to memorize the formula yet. Remember:

> **Softmax = score → probability**

---

# 80. There Are Two Different Softmax Roles

This is important.

### Softmax inside attention

```text
Attention scores
      ↓
Softmax
      ↓
Attention weights
```

It answers:

> **How much should this token use information from other tokens?**

### Softmax at the output

```text
Logits
  ↓
Softmax
  ↓
Next-token probabilities
```

It answers:

> **How likely is each possible next token?**

Same mathematical function, different purpose.

---

# 81. Step 13 — Choose the Next Token

Suppose:

```text
Delhi   → 90%
Mumbai  → 5%
London  → 2%
```

The decoding strategy selects a token.

It might choose the highest-probability token, or a sampling strategy can introduce controlled variation.

Suppose the selected token is:

> **Delhi**

Now:

```text
The capital of India is Delhi
```

But the model doesn't stop.

---

# 82. Step 14 — Add the Token and Repeat

The new token becomes part of the context.

```text
The capital of India is
               ↓
The capital of India is Delhi
               ↓
Predict next token
               ↓
Add it
               ↓
Predict next token
               ↓
...
```

This is called **autoregressive generation**.

### Simple definition

> The model uses what has already been generated to help predict what comes next.

---

# 83. Causal Attention — Why Future Tokens Are Hidden

GPT-style decoder-only Transformers use causal attention.

When predicting a token, the model cannot look at future tokens that would give away the answer.

For example:

```text
Position 1 → sees 1
Position 2 → sees 1, 2
Position 3 → sees 1, 2, 3
Position 4 → sees 1, 2, 3, 4
```

Conceptually:

```text
          1   2   3   4
1         ✓   ✗   ✗   ✗
2         ✓   ✓   ✗   ✗
3         ✓   ✓   ✓   ✗
4         ✓   ✓   ✓   ✓
```

The future is masked.

This allows the model to learn next-token prediction without cheating.

---

# 84. Training vs Generation in a Transformer

### During training

The model can calculate predictions for many positions in parallel while applying the causal mask.

Conceptually:

```text
Input tokens
 ↓
Transformer
 ↓
Predict many next-token targets
 ↓
Compare with true next tokens
 ↓
Loss
 ↓
Backpropagation
 ↓
Update weights
```

### During generation

The model usually generates one new token at a time.

```text
Prompt
 ↓
Token 1
 ↓
Token 2
 ↓
Token 3
 ↓
...
```

This difference is important:

> **Training can be highly parallelized; autoregressive generation is sequential across newly generated tokens.**

---

# 85. The Most Important Transformer Mental Model

Don't try to memorize every equation first.

Remember these three jobs:

```text
1. ATTENTION
   → Exchange information between tokens

2. FFN
   → Transform each token's current representation

3. OUTPUT LAYER
   → Turn the final representation into next-token probabilities
```

And the full flow:

```text
Represent
   ↓
Exchange
   ↓
Transform
   ↓
Repeat
   ↓
Predict
   ↓
Repeat generation
```

---

# 🎯 86. Sentence → Next Token: The Entire Process in One Example

Input:

> **"The capital of India is"**

### 1. Tokenize

```text
The | capital | of | India | is
```

### 2. Token IDs

```text
52 | 1832 | 25 | 781 | 41
```

### 3. Embeddings

```text
52   → vector
1832 → vector
25   → vector
781  → vector
41   → vector
```

### 4. Position

```text
Token representation + position
```

### 5. Attention

Tokens exchange useful contextual information.

### 6. FFN

Each token's representation is transformed.

### 7. Repeat

The process continues through many Transformer blocks.

### 8. Final representation

```text
Rich contextual representation
```

### 9. Linear layer

```text
Vocabulary tokens → logits
```

### 10. Softmax

```text
Logits → probabilities
```

### 11. Select

```text
Delhi → selected next token
```

### 12. Repeat

```text
The capital of India is Delhi ...
```

Then the model predicts the next token again.

---

# 🧠 87. FFN vs Attention vs Softmax

| Component | What it does |
|---|---|
| **Attention** | Lets tokens exchange information |
| **FFN** | Transforms each token's current representation |
| **Residual** | Preserves and combines information |
| **LayerNorm** | Helps stabilize processing |
| **Logits** | Raw scores for possible next tokens |
| **Softmax** | Converts scores into probabilities |
| **Decoding** | Selects/samples the next token |

---

# ⭐ 88. FINAL EASY SUMMARY

## The 11-step memory trick

```text
1. TOKENIZE
   Break sentence into tokens

2. ID
   Give every token an ID

3. EMBED
   Turn IDs into learned vectors

4. POSITION
   Tell the model the order

5. ATTENTION
   Let tokens exchange information

6. FFN
   Transform the information

7. REPEAT
   Run through many Transformer blocks

8. LOGITS
   Give every possible next token a score

9. SOFTMAX
   Turn scores into probabilities

10. PREDICT
    Choose the next token

11. REPEAT
    Add the token and predict again
```

### ⭐ Four words to remember

> **ATTENTION = EXCHANGE**
>
> **FFN = TRANSFORM**
>
> **SOFTMAX = SCORE → PROBABILITY**
>
> **GENERATION = REPEAT**

### ⭐ One-line interview answer

> **A Transformer takes token embeddings plus positional information, repeatedly uses self-attention to exchange contextual information and an FFN to transform representations, then maps the final representation to vocabulary logits, converts them to probabilities with softmax, selects the next token, adds it to the context, and repeats the process to generate the response.**

---

# 📌 89. What You Should Understand Before Moving On

You should now be comfortable explaining these connections:

```text
Token ID
   ↓
Embedding
   ↓
Position
   ↓
Attention
   ↓
Contextual representation
   ↓
FFN
   ↓
Many Transformer blocks
   ↓
Final representation
   ↓
Logits
   ↓
Softmax
   ↓
Next token
```

And most importantly:

> **Attention does not generate the final answer.**
>
> **FFN does not choose the next word.**
>
> **Softmax does not understand the sentence.**
>
> They each do a different job inside the larger Transformer pipeline.
