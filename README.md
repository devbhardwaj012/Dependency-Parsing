# Graph-Based Dependency Parsing (MST Parser) — Complete Project

*Classical graph-based dependency parsing vs modern transformer-based parsing*

---

## Overview

This repository implements a **graph-based dependency parser** using the **Chu-Liu-Edmonds Maximum Spanning Tree (MST)** algorithm and a **structured perceptron** training loop. It is intended as an educational, reproducible demonstration of how dependency parsing was approached before the neural/transformer era, and to highlight where classical methods succeed and where modern neural models outperform them.

If this helped you, **please star the repo and give a like/upvote** — it really helps!

---

## What is Dependency Parsing?

Dependency parsing builds a **directed tree** over a sentence where:

* Every token (word) has exactly one **head** (except the ROOT).
* Edges (head → dependent) represent syntactic/grammatical relationships (subject, object, modifier, etc.).
* The parsed structure is used by downstream tasks like information extraction, semantic role labeling, and machine translation.

---

## This Project — Key Components

* **Chu-Liu-Edmonds MST algorithm**: find the maximum spanning tree in a directed graph of arc scores.
* **Feature-based scoring**: manual features (distance, direction, lexical items, suffixes, capitalization, position).
* **Structured Perceptron training**: update feature weights based on gold vs predicted trees.
* **Evaluation**: Unlabeled Attachment Score (UAS), error breakdown, and qualitative tests.
* **Visualization**: ASCII parse-tree printer and test cases covering PP-attachment, coordination, long-range dependencies, etc.

---

## Graph-Based Parsing (How it works)

1. Score every possible arc (head → dependent) using feature weights.
2. Build a complete directed graph where nodes are tokens (plus ROOT).
3. Use Chu-Liu-Edmonds to extract the **maximum spanning tree** — the highest-scoring valid dependency tree.
4. Train with structured perceptron: increase weights for gold arcs and decrease for predicted incorrect arcs.

**Strengths**

* Global tree optimization (MST finds the best tree under current arc scores).
* Interpretable, lightweight, and fast (suitable for CPU-only environments).
* Educational: shows classical structured-learning and inference.

**Limitations**

* Arc scores are computed independently — inter-arc dependencies are not modeled.
* Requires heavy **feature engineering** → brittle and sparse representations.
* Poor handling of polysemy, semantics, long-range dependencies, and rare words.
* No benefit from unlabeled corpora (no pretraining or transfer learning).

---

## Transition-Based Parsing (Context)

* Uses a stack + buffer + actions (SHIFT, LEFT-ARC, RIGHT-ARC) to build trees incrementally.
* Very fast (linear-time), but **greedy decisions** often propagate errors unless expensive beam search is used.
* Like graph-based parsers, historically dependent on hand-crafted features.

---

## Why Modern Neural / Transformer Parsers Win

Modern parsers replace manual features with learned continuous representations and global modeling techniques:

* **Contextualized embeddings (BERT, RoBERTa, etc.)**: resolve polysemy and provide rich lexical semantics.
* **Self-attention / transformers**: directly model long-range dependencies without exponential feature explosion.
* **Pretraining on massive unlabeled data**: dramatic improvements in low-resource and cross-lingual scenarios.
* **Biaffine and graph neural scoring**: capture interactions between candidate arcs and jointly refine predictions.

**Typical performance (English UAS)**:

* Classical MST (basic): 65–75%
* MST (engineered): 85–90%
* BiLSTM-based: 91–95%
* BERT-based / Transformer: 96–98%+

---

## When to Use Classical Parsers

* Educational purposes and algorithmic demonstrations.
* Resource-constrained deployment (low memory, CPU-only).
* When interpretability is important.
* As reproducible baselines in research.

---

## Quick Start

Install dependencies:

```bash
pip install conllu numpy scipy scikit-learn matplotlib
```

Download UD English EWT:

```bash
wget https://raw.githubusercontent.com/UniversalDependencies/UD_English-EWT/master/en_ewt-ud-train.conllu
wget https://raw.githubusercontent.com/UniversalDependencies/UD_English-EWT/master/en_ewt-ud-dev.conllu
wget https://raw.githubusercontent.com/UniversalDependencies/UD_English-EWT/master/en_ewt-ud-test.conllu
```

Run the notebook/script:

```bash
python your_parser_script.py
```

---

## Files & Structure

```
├── parser.py                # MST parser, feature extractor, training, evaluation
├── visualization.py         # Helpers for ASCII tree visualizations
├── mst_parser_model.pkl     # Saved model (after training)
├── data/
│   ├── en_ewt-ud-train.conllu
│   ├── en_ewt-ud-dev.conllu
│   └── en_ewt-ud-test.conllu
├── README.md                # This file
└── requirements.txt
```

---

## Evaluation & Known Failure Modes

This implementation includes a test suite for:

* PP-attachment ambiguity (e.g., “I saw the man with the telescope”)
* Long-distance dependencies (wh-extraction, relative clauses)
* Coordination ambiguity (“old men and women”)
* Garden-path sentences (“The horse raced past the barn fell”)

Common failure causes: lack of semantic knowledge, limited context, sparse features, independent arc scoring.

---

## Extending & Improving This Project

* Replace feature-based scorer with **neural scorers** (BiLSTM + MLP or Transformer encoder).
* Use **biaffine attention** for joint arc scoring.
* Fine-tune a **pretrained Transformer** (BERT/XLM-R) and build a lightweight parser head.
* Apply **multilingual pretraining / transfer learning** for low-resource languages.
* Experiment with **graph neural networks** to iteratively refine arc scores.

---

## Cite / References

* Dozat, Timothy & Manning, Christopher (2017). *Deep Biaffine Attention for Neural Dependency Parsing*.
* McDonald, Ryan et al. (2005). *Non-projective dependency parsing using spanning tree algorithms*.
* Chu-Liu-Edmonds algorithm (maximum spanning arborescence).

---

## License

MIT License

```
MIT License

Copyright (c) 2025 Dev Bhardwaj

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
```

---

## Support & Acknowledgements

If you enjoyed this project or it helped you learn parsing, **please star the repository and give it a thumbs up / upvote** — it means a lot and helps other learners find it. Thank you!

---

