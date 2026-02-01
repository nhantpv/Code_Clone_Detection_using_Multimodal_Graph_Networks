# Graph-based Code Clone Detection with Graph Matcher

## 📌 Overview
This project focuses on **code clone detection** using **graph-based representations of source code** and **Graph Neural Networks (GNNs)** combined with a **Graph Matching mechanism**. The core idea is to model source code as a **Code Property Graph (CPG)** that captures both syntactic and semantic information, and then learn clone similarity through deep graph representations.

---

## 🎯 Objectives
- Detect **semantic and structural code clones** (Type-1 → Type-4)
- Go beyond token/AST-based methods by leveraging **CPG (AST + CFG + PDG)**
- Design an **effective Graph Matcher** for pairwise code comparison
- Build an extensible and research-friendly pipeline for experimentation

---

## 🧠 Key Concepts

### 1. Code Property Graph (CPG)
Each Java source file is transformed into a graph that integrates:
- **AST (Abstract Syntax Tree)** – syntactic structure
- **CFG (Control Flow Graph)** – execution flow
- **DFG / PDG (Data & Program Dependency Graph)** – data and control dependencies


The CPG is built using a **Python-based pipeline**, leveraging tools such as:
- `javalang` / JavaParser (via JPype)
- `networkx` for graph construction & visualization
- `torch_geometric` for deep learning compatibility

---

### 2. Graph Neural Network Encoder
Each CPG is encoded into a vector representation using GNNs:
- **GINConv** – strong structural discrimination
- **GATConv** – attention over important neighbors
- **Batch Normalization & Dropout** – training stability
- **Global Pooling** (mean + sum) – graph-level embedding


---

### 3. Graph Matcher
To compare two code graphs, the project introduces a **Graph Matching module**:
- Takes embeddings from two graphs
- Applies feature interaction (e.g., concatenation, difference, element-wise product)
- Learns similarity through an MLP-based matcher

This approach allows the model to:
- Capture **fine-grained structural similarity**
- Handle **semantic-preserving transformations**
- Perform well on higher-level clone types (Type-3 / Type-4)

---

### 4. Clone Detection Model Architecture
The overall architecture can be summarized as:

```
Java Source Code (Pair)
        ↓
 Code Property Graphs (CPG)
        ↓
 Shared GNN Encoder
        ↓
 Graph Embeddings (g1, g2)
        ↓
 Graph Matcher
        ↓
 Clone Classification (Softmax / Binary)
```

The final classifier supports **multi-class clone labels** or **binary clone detection**, depending on the dataset.

---