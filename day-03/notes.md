# 🤖 Day 03 — Tokens, Tokenization & Context Window

> **Goal:** Understand how human text becomes the numerical input an LLM can process.

## 🧭 Day 03 Learning Flow

```text
Human Text
    ↓
Tokenizer
    ↓
Tokens
    ↓
Token IDs
    ↓
Embeddings
    ↓
Model processing
```

---

## 1. Why Do LLMs Need Tokens?

A language model does not directly process text the way humans read it.

A model works with numerical representations.

```text
"I love AI"
     ↓
Tokenizer
     ↓
["I", " love", " AI"]
     ↓
Token IDs
     ↓
[...numbers...]
     ↓
Model
```

The exact tokenization depends on the tokenizer used by the model.

> **Key idea:** Text is converted into tokens, and tokens are mapped to IDs before the neural network processes them.

---

## 2. What Is a Token?

A **token** is a piece of text defined by a tokenizer.

A token can be:

- A whole word
- Part of a word
- Punctuation
- A whitespace-related piece
- A symbol
- A special token
- A code fragment

### Important

> **Token ≠ Word**

For example, a tokenizer might represent a word as one token, while another word may be split into several subword tokens.

The exact split is tokenizer-dependent.

---

## 3. What Is Tokenization?

**Tokenization** is the process of converting text into token pieces.

```text
Text
 ↓
Tokenization
 ↓
Token pieces
```

Example conceptually:

```text
unbelievable
     ↓
un + believ + able
```

This is only an illustration. The actual tokenizer may split the word differently.

---

## 4. What Is a Tokenizer?

A **tokenizer** is the algorithm/software that performs tokenization.

Its job is to answer:

> "How should this text be divided into the token pieces in this model's vocabulary?"

Different models can use different tokenization algorithms and vocabularies.

Therefore:

```text
Same text
   ↓
Tokenizer A → token sequence A
Tokenizer B → token sequence B
```

Do not assume all models produce the same tokens or token count.

---

## 5. What Is a Vocabulary?

A **vocabulary** is the collection of token entries a tokenizer/model knows how to map to token IDs.

Simplified example:

```text
Token         ID
-----------------
"the"         10
"AI"          11
"ing"         12
"!"           13
```

The real vocabulary contains many more entries and special tokens.

### Important

> The vocabulary defines the available token pieces. The token ID is the numeric identifier assigned to one entry.

---

## 6. Token vs Token ID

These are different concepts.

```text
Token
 ↓
Text piece

Token ID
 ↓
Number assigned to that token in the vocabulary
```

Example:

```text
"hello" → token
"hello" → ID 1234   ← illustrative only
```

### Critical distinction

> **A token ID is an identifier, not the semantic meaning of the token.**

Meaning is learned later through the model's representations, including embeddings and contextual processing.

---

## 7. Why Not Use One Token per Word?

A vocabulary containing every possible word would be impractical.

Language has:

- Huge vocabularies
- New words
- Names
- Misspellings
- Morphological variations
- Technical terms
- Code
- Multiple languages

Subword tokenization provides a useful compromise.

```text
Whole-word vocabulary
        ↓
Huge and difficult to cover

Subword vocabulary
        ↓
Reuse smaller pieces
        ↓
Can represent many unseen combinations
```

---

## 8. Subword Tokenization

Instead of requiring every full word to be in the vocabulary, a tokenizer can reuse smaller pieces.

Conceptually:

```text
unhappiness
    ↓
un + happi + ness
```

Again, the exact split depends on the tokenizer.

### Why it is useful

The model can represent a new or rare word by combining known pieces rather than requiring one vocabulary entry for the complete word.

---

## 9. BPE — Byte Pair Encoding

**BPE** is a common family of subword tokenization methods.

The basic idea is to start from smaller units and repeatedly merge frequently occurring neighboring pieces.

```text
Small pieces
    ↓
Find frequent pair
    ↓
Merge pair
    ↓
Larger useful token
    ↓
Repeat
```

The result is a vocabulary of reusable subword pieces.

### Why BPE became useful

It provides a balance between:

```text
Character-level representation
        ↕
Whole-word representation
```

It can efficiently represent both common words and rare/unseen combinations.

---

## 10. Token Boundaries Are Not Meaning Boundaries

A tokenization split is a representation decision.

For example:

```text
un + believable
```

does **not** mean the model internally treats those pieces as two complete semantic concepts.

Tokenization answers:

> "How do we encode this text?"

It does not by itself answer:

> "What does this text mean?"

Meaning is learned by the model after tokenization through embeddings and subsequent neural-network processing.

---

## 11. Tokenization Depends on Language

Equivalent sentences in different languages can require different numbers of tokens.

Reasons include:

- Writing system
- Vocabulary design
- Word structure
- Morphology
- Character frequency
- Tokenizer training data

So:

```text
Same meaning
    ↓
Different language
    ↓
Possibly different token count
```

### Interview point

> Token count is tokenizer-dependent; you cannot reliably estimate tokens from word count alone.

---

## 12. Tokenization Fertility

**Tokenization fertility** is a way to describe how many tokens are produced for a text unit.

Conceptually:

```text
Text unit
   ↓
Tokenizer
   ↓
Number of tokens
```

Higher fertility means the same text is split into more tokens.

Lower fertility means fewer tokens.

This matters because more tokens can increase:

- Context usage
- Processing cost
- Latency
- Output/input budget pressure

---

## 13. Punctuation, Whitespace, Emoji and Code

Tokenizers do not only process ordinary words.

They also handle things such as:

```text
Hello,
Hello!
hello
HELLO
😀
function()
```

These may be tokenized differently.

### Important trap

> One visible character, symbol, or emoji does **not** necessarily equal one token.

Similarly:

> One visual word does **not** necessarily equal one token.

---

## 14. Special Tokens

Token vocabularies can also contain special/control tokens used by a model's training or inference format.

Examples can represent concepts such as:

- Beginning/end markers
- Padding
- Unknown/other special states
- Role or message boundaries
- Tool or structured-control markers

The exact special tokens depend on the model/tokenizer.

---

## 15. The Complete Text-to-ID Pipeline

```text
                    HUMAN TEXT
                        │
                        ▼
                  ┌───────────┐
                  │ Tokenizer │
                  └─────┬─────┘
                        │
                        ▼
                Token sequence
                        │
                        ▼
                Vocabulary lookup
                        │
                        ▼
                   Token IDs
                        │
                        ▼
                   Embeddings
                        │
                        ▼
                 Neural network
```

### Remember the order

```text
Text
 → Tokens
 → Token IDs
 → Embeddings
 → Model processing
```

---

# 🧠 Context Window

## 16. What Is a Context Window?

A **context window** is the amount of tokenized information a model can use as context for a request.

Think of it as the model's **working desk**.

```text
┌──────────────────────────────────────┐
│              CONTEXT                 │
│                                      │
│ System instructions                  │
│ Conversation history                 │
│ Current user prompt                  │
│ Retrieved documents                  │
│ Tool results                         │
│ Other model-visible context          │
│                                      │
└──────────────────────────────────────┘
```

All of this consumes context capacity.

---

## 17. Context Is Measured in Tokens

The context window is generally described in **tokens**, not words.

Therefore:

```text
More text
   ↓
More tokens
   ↓
More context usage
```

And because tokenization differs:

```text
Same number of words
       ≠
Same number of tokens
```

---

## 18. What Can Occupy the Context?

Depending on the application, the model may receive:

```text
System instructions
        +
User messages
        +
Previous conversation
        +
Retrieved RAG chunks
        +
Tool outputs
        +
Current request
        ↓
Model context
```

This is why a long conversation can eventually consume a large amount of context.

---

## 19. What Happens When Context Gets Too Large?

An application must manage the available context.

Possible strategies include:

```text
Large history
     ↓
Trim old messages
     OR
Summarize history
     OR
Retrieve only relevant history
     OR
Use memory/storage outside the immediate context
```

The exact behavior depends on the model and application.

### Important

> Context-window management is an application/design problem as well as a model-capacity problem.

---

# 🔗 Tokenization and Cost

## 20. Why Token Count Matters

Token count can influence:

- Context usage
- Latency
- Cost in token-based APIs
- Maximum prompt size
- Maximum output budget

Conceptually:

```text
More tokens
   ↓
More computation/data to process
   ↓
Potentially higher latency/cost
```

Exact pricing and limits depend on the model/provider.

---

# ⚠️ Common Mistakes & Traps

## Mistake 1 — Token = word

❌ Wrong.

A word can be one token or several tokens, and a token can also represent something other than a full word.

## Mistake 2 — Token ID = meaning

❌ Wrong.

A token ID is an identifier into a vocabulary.

## Mistake 3 — All tokenizers tokenize the same way

❌ Wrong.

Tokenization is tokenizer/model dependent.

## Mistake 4 — One emoji = one token

❌ Not guaranteed.

## Mistake 5 — Context window = memory

❌ Not exactly.

The context window is the model's current tokenized working context. Persistent memory, application storage, retrieval systems, and context are different concepts.

## Mistake 6 — Bigger vocabulary automatically means better model

❌ Not necessarily.

Tokenizer design involves trade-offs between vocabulary size, sequence length, coverage, and efficiency.

---

# 🎯 Interview Questions

### Junior

**Q1. What is a token?**

A token is a tokenizer-defined piece of text that is mapped to a numeric ID for model processing.

**Q2. Is one token always one word?**

No. A token can be a whole word, part of a word, punctuation, whitespace-related piece, symbol, or special token.

**Q3. What is a tokenizer?**

A tokenizer converts raw text into a sequence of token pieces according to a model-specific vocabulary and tokenization algorithm.

### Mid-level

**Q4. What is the difference between a token and a token ID?**

A token is the text piece; the token ID is the numeric identifier assigned to that token in the vocabulary.

**Q5. Why do modern LLMs use subword tokenization?**

It provides a practical balance between vocabulary size and the ability to represent rare, new, and morphologically varied words.

**Q6. What is BPE?**

Byte Pair Encoding is a subword tokenization approach that builds useful token units by repeatedly merging frequent neighboring pieces.

**Q7. Why can the same sentence have different token counts in different models?**

Because tokenization depends on the tokenizer's vocabulary and algorithm.

### Senior

**Q8. Why does tokenization affect LLM cost and latency?**

Token count affects how much input must be processed and how much context capacity is consumed; in token-priced APIs it can also affect cost.

**Q9. Why is tokenization not the same as understanding?**

Tokenization converts text into model-readable pieces. Semantic representations and contextual understanding are developed by later neural-network layers.

**Q10. What is a context window?**

It is the maximum amount of tokenized information a model can use as context for a request under that model's supported limits.

---

# 🧪 Practice Questions

### 1. Predict the conceptual pipeline

What happens between:

```text
"I love AI"
```

and the neural network receiving the input?

### 2. Explain the difference

Explain these three terms:

```text
Token
Token ID
Embedding
```

### 3. Interview challenge

Why might a 20-word sentence consume 30 tokens in one tokenizer and a different number in another tokenizer?

### 4. Context challenge

A conversation contains:

```text
System instructions
+ 50 previous messages
+ retrieved documents
+ current question
```

What determines whether everything can fit into the model's context?

---

# ⚡ Quick Revision

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
MODEL
```

### Remember

| Concept | Simple meaning |
|---|---|
| Token | Text piece created by tokenizer |
| Tokenizer | Converts text into token pieces |
| Vocabulary | Collection of token entries |
| Token ID | Numeric ID for a vocabulary token |
| BPE | Common subword tokenization approach |
| Context window | Token capacity available as model context |
| Tokenization fertility | How many tokens a text unit produces |

### One-line memory rule

> **Tokenization converts text into token pieces; token IDs identify those pieces; embeddings turn IDs into vectors that the neural network can process.**

---

# ✅ Day 03 Checklist

- [ ] I understand what a token is
- [ ] I understand what a tokenizer does
- [ ] I know token ≠ word
- [ ] I understand vocabulary
- [ ] I understand token IDs
- [ ] I understand subword tokenization
- [ ] I understand BPE at a conceptual level
- [ ] I understand tokenization fertility
- [ ] I understand special tokens
- [ ] I understand context windows
- [ ] I understand why token count matters
- [ ] I can explain Text → Tokens → IDs → Embeddings
