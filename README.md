Graph-Based Dependency Parsing Using the MST Algorithm

This repository contains an implementation of a classical graph-based dependency parser based on the Chu–Liu–Edmonds Maximum Spanning Tree (MST) algorithm. The project demonstrates how dependency parsing was performed before the introduction of neural and transformer-based models, using manually engineered features and structured perceptron training.

The primary goal of this project is educational: to illustrate the strengths and limitations of traditional dependency parsing methods and to provide a clear comparison with modern approaches based on contextual embeddings and self-attention mechanisms.

Project Structure

The repository consists of:

dependency-parsing/
│
├── dependency-parsing.ipynb   # Complete implementation, training, evaluation, and analysis
└── README.md                  # Project documentation


All parsing logic, feature extraction, training procedures, evaluation, and visualizations are contained within the single Jupyter Notebook.

Overview of Dependency Parsing

Dependency parsing converts a sentence into a directed tree where:

Each word has exactly one syntactic head (except the root), and

Edges represent grammatical relations such as subject, object, modifier, etc.

Dependency structures are fundamental to downstream tasks such as machine translation, semantic role labeling, question answering, and information extraction.

Classical Dependency Parsing Methods
1. Graph-Based Dependency Parsing

This project implements this approach.

Graph-based parsers treat parsing as a global optimization problem:

Each possible head → dependent arc is assigned a score using a feature-based model.

A complete directed graph is constructed with these scores.

The MST algorithm selects the highest-scoring valid dependency tree.

A structured perceptron updates weights based on the difference between predicted and gold-standard trees.

Strengths

Global inference over the entire tree.

Mathematically principled and deterministic.

Interpretable scoring functions.

Efficient in terms of runtime and memory.

Limitations

Arc scores are computed independently; interactions between arcs are not modeled.

Manual feature engineering leads to sparse and brittle representations.

Limited ability to capture long-range dependencies.

No semantic understanding (treats words as symbols, not meanings).

Poor performance on polysemy, ambiguity, and out-of-vocabulary words.

2. Transition-Based Dependency Parsing

Although not implemented here, this approach provides important context.

Transition-based parsers use a stack, buffer, and a sequence of actions (SHIFT, LEFT-ARC, RIGHT-ARC) to build a parse incrementally.

Strengths

Very fast (linear-time).

Suitable for incremental parsing.

Limitations

Greedy and prone to error propagation.

Requires manual feature templates.

Struggles with complex syntax and long-range dependencies.

Why Classical Parsers Are Limited

Traditional parsers rely on:

Manually crafted features (distance, direction, suffixes, capitalization).

Sparse input representations.

Local or shallow contextual windows.

No ability to leverage large unlabeled corpora.

No contextual understanding or semantic generalization.

As a result, classical models plateau around 85–90% UAS (Unlabeled Attachment Score) even with heavy feature engineering.

Modern Neural and Transformer-Based Models

Modern dependency parsers rely on deep learning, contextual embeddings, and self-attention.

Advantages Over Classical Methods

Contextual Embeddings
Models such as BERT and RoBERTa provide different vector representations for the same word depending on context, addressing polysemy and ambiguity.

Self-Attention Mechanisms
Transformers consider the entire sentence simultaneously, allowing direct modeling of long-range dependencies.

Pretraining on Large Corpora
Neural models acquire syntactic, semantic, and world knowledge from billions of tokens, which is not possible in classical approaches.

Better Generalization
Dense embeddings enable the model to generalize across related words and structures, improving performance on rare and unseen phenomena.

Superior Accuracy
Typical performance levels:

Classical MST parser: 65–90% UAS

BiLSTM-based parsers: 91–95% UAS

Transformer-based parsers: 96–98%+ UAS

Transformer-based parsers now approach near–human-level performance.

Running the Notebook

Install required dependencies:

pip install conllu numpy scipy scikit-learn matplotlib


Download the Universal Dependencies English EWT treebank:

wget https://raw.githubusercontent.com/UniversalDependencies/UD_English-EWT/master/en_ewt-ud-train.conllu
wget https://raw.githubusercontent.com/UniversalDependencies/UD_English-EWT/master/en_ewt-ud-dev.conllu
wget https://raw.githubusercontent.com/UniversalDependencies/UD_English-EWT/master/en_ewt-ud-test.conllu


Open the notebook:

dependency-parsing.ipynb


and execute all cells. The notebook covers:

Data loading

Feature extraction

MST decoding

Structured perceptron training

Evaluation (UAS, error categories)

Visualization of dependency trees

Analysis of linguistic phenomena

Discussion of failure cases

Features Included in the Notebook

Chu–Liu–Edmonds maximum spanning tree algorithm

Structured perceptron training loop

Comprehensive feature extractor

ASCII dependency-tree visualization

Evaluation on development and test sets

Qualitative analysis on:

PP-attachment ambiguity

Coordination structures

Long-range dependencies

Relative clauses

Garden-path sentences

License

This project is distributed under the MIT License:

MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...


(Full MIT License text continues.)

Acknowledgment

If this project is useful to you, please consider starring the repository or sharing it. It helps others discover educational material on classical and modern dependency parsing.
