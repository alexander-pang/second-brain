---
title: Attention
status: in-progress
date: 2026-05-22
tags: [concept, attention, transformer, seq2seq]
---

# Attention

A mechanism that lets a model focus on the most relevant parts of a sequence when producing each output, rather than compressing everything into one vector.

See also: [[lectures/03-encoders-decoders-attention]]

---

## Motivation

RNN encoder-decoder compressed the entire input into a single context embedding — a bottleneck that hurt performance on long sequences. Attention gives the decoder direct access to every input token's hidden state.

## How It Works (Bahdanau / additive attention, 2014)

1. Encoder produces a **hidden state** for each input token.
2. At each decoder step, compute a **score** between the current decoder state and each encoder hidden state.
3. Softmax the scores → **attention weights** (sum to 1).
4. Weighted sum of encoder hidden states → **context vector** for this step.
5. Decoder uses context vector to produce the next token.

## Attention Weights

Higher weight = more relevant to the current output token.

```
"I love llamas" → "Ik hou van lama's"
I     → Ik      (high weight)
love  → hou/van (high weight)
llamas → lama's (high weight)
```

## Transformer Attention vs. RNN Attention

| | RNN + Attention | Transformer Self-Attention |
|---|---|---|
| Processes tokens | Sequentially | In parallel |
| Attends to | Encoder hidden states | All tokens in same sequence |
| Introduced | 2014 | 2017 |

---

## Notes

<!-- fill in after transformer attention lecture -->
