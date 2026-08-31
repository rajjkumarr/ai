# 🤖 Day 05 — Transformer Architecture

> **Goal:** Understand what happens inside a Transformer after text is converted into token embeddings — all the way to predicting the next token.

## 🧭 The Day 05 Journey

```text
Sentence
   ↓
Tokenizer
   ↓
Tokens
   ↓
Token IDs
   ↓
Embedding Vectors
   ↓
Position Information
   ↓
┌─────────────────────────────┐
│      Transformer Block      │
│                             │
│  Self-Attention             │
│       ↓                     │
│  Residual Connection        │
│       ↓                     │
│  Feed-Forward Network (FFN) │
│       ↓                     │
│  Residual Connection        │
└─────────────────────────────┘
   ↓
Repeat many blocks
   ↓
Final Representation
   ↓
Linear Layer
   ↓
Logits
   ↓
Softmax
   ↓
Next-Token Probabilities
   ↓
Choose Next Token
   ↓
Add Token to Context
   ↓
Repeat
```

---

# 1. Start With a Sentence

Suppose you ask the model:

> **“The capital of India is”**

The model does not directly run the raw sentence through the neural network.

It first converts the text into a form the network can process.

---

# 2. Sentence → Tokens

A **tokenizer** breaks the sentence into token pieces.

For learning, imagine:

```text
The | capital | of | India | is
```

A real tokenizer may split the text differently. A token can be a whole word, part of a word, punctuation, whitespace-related piece, or another text fragment.

> **Remember:** Token ≠ Word

---

# 3. Tokens → Token IDs

Each token is mapped to a number from the tokenizer's vocabulary.

Example only:

```text
The       → 52
capital   → 1832
of        → 25
India     → 781
is        → 41
```

So the model receives something like:

```text
[52, 1832, 25, 781, 41]
```

### ⚠️ Important

A token ID is only an **identifier**.

```text
India → 781
```

does not mean:

```text
781 = “India's meaning”
```

---

# 4. Token IDs → Embeddings

The model uses the token IDs to look up learned **embedding vectors**.

For example:

```text
India
   ↓
[0.7, 0.9, 0.2, -0.1, …]
```

The vector above is only an illustration.

### What is an embedding?

An **embedding** is a learned numerical representation of a token or other item.

Instead of only knowing:

```text
India → ID 781
```

the model now has a numerical representation that can participate in mathematical operations and later contextual processing.

---

# 5. Add Position Information

A Transformer also needs to know **where each token appears**.

Why?

Because order can change meaning.

```text
Dog bites man
```

is different from:

```text
Man bites dog
```

So conceptually:

```text
Token information
       +
Position information
       ↓
Input representation
```

Modern architectures use different mechanisms for positional information. The important idea is:

> **The model needs token information + position/order information.**

---

# 6. Now the Transformer Starts

The token representations enter the Transformer.

A simplified Transformer block looks like this:

```text
Input
  ↓
Self-Attention
  ↓
Residual Connection
  ↓
Feed-Forward Network (FFN)
  ↓
Residual Connection
  ↓
Output
```

This block is repeated many times in a large language model.

---

# 7. Self-Attention — The Core Idea

The most important question is:

> **How are the tokens related to one another?**

Consider:

> **“The capital of India is”**

When processing the end of the sentence, information from words such as **capital** and **India** is very useful.

Self-attention allows token positions to exchange information.

```text
The      ↔
capital  ↔
of       ↔
India    ↔
is       ↔
```

The model calculates how strongly different positions should interact.

### Easy mental model

> **Attention = information exchange between tokens.**

---

# 8. Query, Key and Value — Simple Intuition

Attention uses three learned projections:

```text
Q = Query
K = Key
V = Value
```

Think of them like a search system:

| Part | Easy way to think about it |
|---|---|
| **Query** | What information am I looking for? |
| **Key** | What kind of information do I contain? |
| **Value** | What information should I provide if I am relevant? |

This is only an intuition. Q, K and V are mathematical projections, not literal questions and answers between words.

---

# 9. How Q, K and V Are Created

Suppose the input representations are represented by `X`.

The Transformer creates:

```text
Q = XWQ
K = XWK
V = XWV
```

Where:

- `X` = current token representations
- `WQ` = learned Query weights
- `WK` = learned Key weights
- `WV` = learned Value weights

These weight matrices are learned during training.

---

# 10. Attention Scores

The model compares Queries with Keys.

The basic operation is:

```text
Q × Kᵀ
```

This produces scores that tell the model how strongly positions relate to one another.

Conceptually:

```text
Query of one token
        ↓
Compare with Keys of other tokens
        ↓
Attention scores
```

Higher score → stronger relationship for that attention calculation.

---

# 11. Why Divide by √dₖ?

The scaled dot-product attention equation is:

```text
Attention(Q,K,V)
= softmax((QKᵀ / √dₖ)V)
```

More clearly:

```text
softmax( QKᵀ / √dₖ ) × V
```

The division by `√dₖ` keeps the raw attention scores at a more manageable scale, which helps make training stable.

You do not need to memorize the mathematics yet. Remember:

> **Scaling keeps attention scores well-behaved.**

---

# 12. Softmax Inside Attention

After the attention scores are calculated, Softmax converts them into normalized attention weights.

Example only:

```text
capital → 0.60
India   → 0.30
of      → 0.07
The     → 0.03
```

The weights add up to approximately 1.

These weights tell the model how much information to take from the corresponding Value vectors.

```text
Attention scores
       ↓
    Softmax
       ↓
Attention weights
       ↓
Weighted Values
       ↓
Attention output
```

### Important

This Softmax has nothing to do with choosing the final next token yet.

It is answering:

> **“How much should this position attend to other positions?”**

---

# 13. Apply the Values

The attention weights are applied to the Value vectors.

If the model gives:

```text
Token A → 10%
Token B → 20%
Token C → 70%
```

then the attention output is a weighted combination of their Value vectors.

Conceptually:

```text
Relevant information
        ↓
Weighted combination
        ↓
New context-aware representation
```

---

# 14. What Has Attention Achieved?

Before attention:

```text
“it”
```

has an initial representation.

After attention:

```text
“it”
+
relevant information from surrounding tokens
```

So its representation becomes **context-aware**.

> **Attention lets tokens exchange useful information.**

---

# 15. Multi-Head Attention

Instead of performing only one attention calculation, Transformers use multiple attention heads.

```text
              Input
                │
      ┌─────────┼─────────┐
      ↓         ↓         ↓
   Head 1     Head 2    Head 3   … Head N
      ↓         ↓         ↓         ↓
  Attention  Attention  Attention  Attention
      └─────────┼─────────┘
                ↓
         Combine outputs
                ↓
        Linear projection
                ↓
             Output
```

### Why multiple heads?

Different heads can learn different useful patterns in the data.

For example, the model may learn attention patterns related to:

- syntax
- references
- nearby relationships
- long-range relationships
- semantic associations

Do not assume one fixed head always means one specific human-readable concept. The patterns are learned.

---

# 16. Residual Connection

After attention, the Transformer does not throw away the original representation.

Conceptually:

```text
Original information
        +
New information from attention
        ↓
Updated representation
```

This is called a **residual connection** or **skip connection**.

Why is it useful?

It helps preserve information and makes deep networks easier to train.

---

# 17. FFN — Feed-Forward Network

Now we reach the second major component of a Transformer block.

### Simple definition

> **FFN takes the information produced by attention and transforms it further.**

The easiest memory rule is:

```text
Attention = exchange information
FFN       = transform information
```

---

# 18. What Does an FFN Look Like?

A simplified FFN is:

```text
Input
 ↓
Linear Layer
 ↓
Nonlinear Activation / Gating
 ↓
Linear Layer
 ↓
Output
```

The first linear layer often expands the representation.

The nonlinear step gives the network more expressive power.

The second linear layer projects it back toward the model dimension.

Conceptually:

```text
Small representation
        ↓
      Expand
        ↓
Nonlinear processing
        ↓
      Compress
        ↓
Updated representation
```

---

# 19. Why Does the FFN Need Nonlinearity?

Language relationships are extremely complex.

A purely linear transformation would be too limited.

A nonlinear activation allows the network to learn much richer patterns.

Common activation/gating choices in modern Transformer architectures include things such as:

- GELU
- SwiGLU

The exact choice depends on the architecture.

---

# 20. Does FFN Look at Other Tokens?

Usually, the FFN processes each token position independently using the same learned network.

So conceptually:

```text
Token A → FFN → Token A'
Token B → FFN → Token B'
Token C → FFN → Token C'
```

### Compare

**Attention:**

```text
Token A ↔ Token B ↔ Token C
```

Tokens exchange information.

**FFN:**

```text
Token A → transform
Token B → transform
Token C → transform
```

Each position is transformed using the FFN.

> **Attention mixes information between positions. FFN transforms the representation at each position.**

---

# 21. Layer Normalization

Transformers also use **Layer Normalization**.

Its broad purpose is to keep internal activations well-behaved and help training remain stable.

A simplified block often looks like:

```text
LayerNorm
   ↓
Attention
   ↓
Residual
   ↓
LayerNorm
   ↓
FFN
   ↓
Residual
```

Different architectures vary in exactly where normalization is placed.

---

# 22. One Complete Transformer Block

```text
                 INPUT
                   ↓
              LayerNorm
                   ↓
         Multi-Head Attention
                   ↓
            Residual Add
                   ↓
              LayerNorm
                   ↓
               FFN / MLP
                   ↓
            Residual Add
                   ↓
                 OUTPUT
```

This is a simplified mental model, but it captures the main flow.

---

# 23. Why Repeat the Block?

One block is usually not enough.

Large language models stack many Transformer blocks:

```text
Input
  ↓
Block 1
  ↓
Block 2
  ↓
Block 3
  ↓
...
  ↓
Block N
```

Each block transforms the representations further.

After many layers, the model has rich contextual representations.

### Mental model

```text
Layer 1 → basic relationships
Layer 2 → richer relationships
Layer 3 → more contextual processing
...
Layer N → rich final representation
```

Do not interpret this as a fixed rule that one layer equals one specific concept. Information is distributed across the network.

---

# 24. Now We Predict the Next Token

After the Transformer stack, the model has a final representation for the current sequence.

The next question is:

> **What token should come next?**

For a language model, the final representation is projected into scores for the vocabulary.

---

# 25. Linear Layer → Logits

Suppose the vocabulary contains many possible tokens.

The final linear layer produces one raw score for each possible next token.

These raw scores are called **logits**.

Example only:

```text
Delhi      → 8.5
Mumbai     → 4.2
London     → 2.1
Paris      → 1.5
banana     → -1.2
...
```

### Remember

> **Logit = raw score before probability conversion.**

Logits are not probabilities.

---

# 26. Softmax — Logits → Probabilities

Now the second important use of Softmax appears.

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

These probabilities add up to approximately 100%.

### Softmax definition

> **Softmax converts raw scores into a probability distribution.**

---

# 27. How Softmax Works — Simple Example

Suppose the logits are:

```text
[3, 1, 0]
```

### Step 1 — Exponentiate

Softmax uses the exponential function:

```text
e³ ≈ 20.09
e¹ ≈ 2.72
e⁰ = 1
```

So:

```text
[3, 1, 0]
   ↓
[20.09, 2.72, 1]
```

### Step 2 — Add them

```text
20.09 + 2.72 + 1 = 23.81
```

### Step 3 — Divide each by the total

```text
20.09 / 23.81 ≈ 0.844
2.72  / 23.81 ≈ 0.114
1     / 23.81 ≈ 0.042
```

So:

```text
[0.844, 0.114, 0.042]
```

or:

```text
84.4%
11.4%
4.2%
```

That's Softmax.

---

# 28. Two Softmax Operations You Must Not Confuse

This is very important.

## Softmax #1 — Inside Attention

```text
QKᵀ scores
    ↓
Softmax
    ↓
Attention weights
```

Question being answered:

> **“How much should this token attend to other tokens?”**

## Softmax #2 — Final Output

```text
Final representation
    ↓
Linear layer
    ↓
Logits
    ↓
Softmax
    ↓
Next-token probabilities
```

Question being answered:

> **“How likely is each possible next token?”**

Same mathematical function, different purpose.

---

# 29. Choose the Next Token

Suppose:

```text
Delhi      → 90%
Mumbai     → 5%
London     → 2%
...
```

A decoding strategy chooses the next token.

A simple strategy can choose the highest-probability token.

Another strategy can sample from the probability distribution.

This is why generated text can sometimes vary.

---

# 30. Add the Token and Repeat

Suppose the model chooses:

> **Delhi**

Now the sequence becomes:

```text
The capital of India is Delhi
```

The model doesn't stop automatically.

It predicts the next token again.

```text
The capital of India is Delhi
                ↓
          Predict next token
                ↓
               “.”
```

Then the sequence becomes:

```text
The capital of India is Delhi.
```

The process continues until the response is finished.

---

# 31. Autoregressive Generation

This repeated process is called **autoregressive generation**.

It means:

> **What the model already generated becomes part of the context used to generate what comes next.**

Visualize it as:

```text
Prompt
 ↓
Token 1
 ↓
Prompt + Token 1
 ↓
Token 2
 ↓
Prompt + Token 1 + Token 2
 ↓
Token 3
 ↓
...
```

---

# 32. Does the Model Predict the Whole Sentence at Once?

No — not in an autoregressive decoder-only LLM.

A useful mental model is:

```text
Predict token 1
Predict token 2
Predict token 3
Predict token 4
...
```

Those tokens eventually form:

```text
words → phrases → sentences → complete response
```

So the model fundamentally predicts the **next token**, not an entire paragraph at once.

---

# 33. Causal Attention

GPT-style decoder-only language models use **causal attention**.

The current position can use information from earlier positions, but not future positions.

For example:

```text
Position 1 → sees 1
Position 2 → sees 1,2
Position 3 → sees 1,2,3
Position 4 → sees 1,2,3,4
```

Conceptually:

```text
             1   2   3   4
Position 1   ✓   ✗   ✗   ✗
Position 2   ✓   ✓   ✗   ✗
Position 3   ✓   ✓   ✓   ✗
Position 4   ✓   ✓   ✓   ✓
```

This prevents the model from seeing the future answer while learning to predict the next token.

---

# 34. Why Transformers Can Train Efficiently

RNNs process sequences step by step:

```text
Token 1
  ↓
Token 2
  ↓
Token 3
  ↓
Token 4
```

Transformers can process many token positions in parallel during training while using the causal mask to preserve the next-token prediction objective.

Conceptually:

```text
Token 1 ─┐
Token 2 ─┤
Token 3 ─┼→ Attention computation
Token 4 ─┤
Token 5 ─┘
```

This ability to scale efficiently was a major reason Transformers became so important.

---

# 35. The Complete Example — “The Capital of India Is …”

Let's put everything together.

### Step 1 — Sentence

```text
The capital of India is
```

### Step 2 — Tokens

```text
The | capital | of | India | is
```

### Step 3 — Token IDs

```text
52 | 1832 | 25 | 781 | 41
```

### Step 4 — Embeddings

```text
The      → vector
capital  → vector
of       → vector
India    → vector
is       → vector
```

### Step 5 — Position

```text
The      → position 1
capital  → position 2
of       → position 3
India    → position 4
is       → position 5
```

### Step 6 — Transformer Block

```text
Embeddings + position
        ↓
Self-attention
        ↓
Tokens exchange information
        ↓
Residual
        ↓
FFN
        ↓
Residual
```

### Step 7 — Repeat

```text
Block 1
 ↓
Block 2
 ↓
Block 3
 ↓
...
 ↓
Block N
```

### Step 8 — Final representation

```text
Rich contextual representation
```

### Step 9 — Linear layer

Scores for every vocabulary token:

```text
Delhi      → 8.5
Mumbai     → 4.2
London     → 2.1
...
```

### Step 10 — Softmax

```text
Delhi      → 90%
Mumbai     → 5%
London     → 2%
...
```

### Step 11 — Choose token

```text
Delhi
```

### Step 12 — Add it to context

```text
The capital of India is Delhi
```

### Step 13 — Repeat

Predict the next token.

```text
The capital of India is Delhi.
```

Continue until the answer is complete.

---

# 🧠 36. The Transformer in 4 Big Stages

Instead of trying to remember everything at once, remember these four stages.

## Stage 1 — Represent

```text
Text
 ↓
Tokens
 ↓
Token IDs
 ↓
Embeddings
```

**Purpose:** Convert language into numerical representations.

## Stage 2 — Exchange Information

```text
Embeddings + position
 ↓
Attention
 ↓
Tokens exchange information
```

**Purpose:** Understand relationships between positions.

## Stage 3 — Transform

```text
Attention
 ↓
Residual
 ↓
FFN
 ↓
Residual
```

**Purpose:** Transform and refine each token representation.

## Stage 4 — Predict

```text
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
Choose token
```

**Purpose:** Decide what token should come next.

---

# ⭐ 37. FFN vs Softmax — Never Mix Them Up

| Component | Main job |
|---|---|
| **Attention** | Exchange information between token positions |
| **FFN / MLP** | Transform the current token representations |
| **Softmax inside attention** | Convert attention scores into attention weights |
| **Softmax at output** | Convert vocabulary logits into next-token probabilities |

---

# 🔥 38. Final Memory Map

```text
TEXT
 ↓
TOKENIZER
 ↓
TOKENS
 ↓
TOKEN IDs
 ↓
EMBEDDINGS
 ↓
POSITION
 ↓
┌────────────────────────────┐
│       TRANSFORMER          │
│                            │
│ Attention → EXCHANGE       │
│ Residual  → PRESERVE/ADD   │
│ FFN       → TRANSFORM      │
│ Residual  → PRESERVE/ADD   │
└────────────────────────────┘
 ↓
REPEAT MANY BLOCKS
 ↓
FINAL REPRESENTATION
 ↓
LINEAR LAYER
 ↓
LOGITS
 ↓
SOFTMAX
 ↓
PROBABILITIES
 ↓
NEXT TOKEN
 ↓
ADD TO CONTEXT
 ↓
REPEAT
```

## The easiest memory trick

> **Attention = EXCHANGE**
>
> **FFN = TRANSFORM**
>
> **Softmax = SCORE → PROBABILITY**
>
> **Generation = REPEAT NEXT-TOKEN PREDICTION**

---

# ✅ 39. One-Paragraph Interview Answer

> A Transformer-based LLM first converts text into tokens, maps those tokens to token IDs, and looks up learned embeddings. Positional information is then incorporated so token order can be represented. The resulting representations pass through many Transformer blocks. Each block uses self-attention to allow tokens to exchange contextual information, residual connections to preserve and combine information, and a feed-forward network to transform the representations. After the final Transformer layer, a linear projection produces logits for the vocabulary. Softmax converts those logits into probabilities, a decoding strategy chooses the next token, and that token is added back into the context. The model repeats this process until the response is complete.

---

# 📌 40. Final One-Line Understanding

> **A Transformer takes token embeddings, lets tokens exchange information through attention, transforms that information through FFN layers, repeats this many times, then turns the final representation into probabilities and predicts the next token.**

---

## 🔗 Related Days

- [Day 01 — AI Evolution](../day-01/notes.md)
- [Day 02 — How LLMs Answer](../day-02/notes.md)
- [Day 03 — Tokens, Tokenization & Context](../day-03/notes.md)
- [Day 04 — Embeddings](../day-04/notes.md)
