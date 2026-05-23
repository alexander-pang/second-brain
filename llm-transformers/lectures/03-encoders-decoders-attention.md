---
title: "Lecture 03: Encoders, Decoders, and Attention"
status: in-progress
date: 2026-05-22
tags: [lecture, rnn, encoder-decoder, attention, seq2seq, autoregressive]
---

# Lecture 03: Encoders, Decoders, and Attention

## The Problem with Static Embeddings

Word2Vec gives "bank" the same vector whether it means a financial institution or a riverbank. Meaning should shift with context.

---

## RNN Encoder-Decoder (pre-2014)

**Recurrent Neural Networks (RNNs)** process sequences by carrying a hidden state forward through each token.

Architecture for translation (`"I love llamas"` → `"Ik hou van lama's"`):

```
Input tokens
  → Encoder (RNN) → single context embedding
  → Decoder (RNN) → output tokens (autoregressive)
```

### Autoregressive Generation

Each output token is produced one at a time, feeding back into the next step:

| Step | Input | Output token |
|------|-------|-------------|
| 1 | `I love llamas` | `Ik` |
| 2 | `I love llamas Ik` | `hou` |
| 3 | `I love llamas Ik hou` | `van` |
| … | … | … |

### Bottleneck Problem

The entire input is compressed into a **single context embedding** before decoding. Long or complex sequences lose information — the single vector can't hold everything.

---

## Attention (2014)

Bahdanau et al. introduced **attention** to solve the bottleneck.

Instead of one context embedding, the decoder gets access to the **hidden state of every input token**, then learns which ones to focus on.

### Key Idea

Attention assigns a **weight** to each input token at each decoding step — higher weight = more relevant to the current output.

Example for `"I love llamas"` → `"Ik hou van lama's"`:

| Input \ Output | Ik | hou | van | lama's |
|---|---|---|---|---|
| I | **high** | low | low | low |
| love | low | **high** | **high** | low |
| llamas | low | low | low | **high** |

### With Attention: Updated Architecture

```
Input tokens
  → Encoder (RNN) → hidden state per token (not just one vector)
  → Decoder (RNN) + attention over all hidden states
  → output tokens (autoregressive)
```

The decoder attends to the most relevant input tokens at each generation step → much better output, especially for long sequences.

---

## Remaining Limitation

The RNN processes tokens **sequentially** — it can't parallelize across a sequence during training. This is slow and makes scaling hard.

→ Next lecture: transformers solve this with **self-attention**, which processes all tokens in parallel.

---

## Key Terms

- **Hidden state**: internal RNN vector encoding information about all tokens seen so far.
- **Autoregressive**: generating one token at a time, feeding each output back as input.
- **Attention weight**: a learned scalar indicating how relevant one token is to another.
- **Context embedding**: the single compressed representation of the input (the bottleneck).

---

## Related Notes

- [[concepts/encoder-decoder]]
- [[concepts/attention]]
- [[lectures/02-word2vec-embeddings]]

---

## Questions / Gaps

- [ ] How exactly are attention weights computed? (softmax over dot products — confirm next video)
- [ ] What's the difference between Bahdanau attention and the transformer's scaled dot-product attention?
- [ ] Next video: how do transformers replace the RNN with parallel self-attention?

---

## Notes

<!-- your observations -->
