# Box Embedding Transformer

This repository contains a prototype implementation of a **decoder-only transformer** that integrates **box embeddings** into the training objective. The goal is to explore whether richer embedding geometries (beyond simple point embeddings) can improve interpretability, rare word generalization, and semantic modeling in large language models.

---

## Motivation

Conventional transformers encode tokens as points in a high-dimensional vector space. While effective, point embeddings struggle with:

- **Rare words and long-tail semantics**
- **Polysemy (multiple meanings per word)**
- **Hierarchical relationships and inclusion**
- **Data efficiency**

**Box embeddings** represent tokens as high-dimensional axis-aligned hyperrectangles. This allows explicit modeling of inclusion, intersection, and uncertainty, offering a more expressive representation space.

---

## Implementation

The current prototype implements:

- **BoxTensor & BoxEmbedding modules**  
  - Tokens represented by lower/upper corner vectors  
  - Initialization ensures small, non-degenerate boxes  

- **Word2Box-inspired scoring**  
  - Intersection-based similarity functions  
  - Supports auxiliary box-specific losses  

- **Hybrid Loss**  
  - Standard cross-entropy for language modeling  
  - Max-margin loss encouraging semantic overlap consistency  

- **Weight Tying**  
  - Input embeddings, box embeddings, and output projection are tied for parameter efficiency  

---

## Limitations

- **Shallow integration**: Transformer forward pass does not yet use box geometry. It still operates on vector embeddings.
- **Loss functions**: A very simple margin-based loss is used on box intersection volume.
- **Evaluation**: No systematic benchmarking on rare words, polysemy, or uncertainty estimation yet.

---

## Research Directions

This project is a **starting point** for deeper exploration. Proposed directions include:

1. **Deep integration**  
   - Operate directly on box embeddings throughout the transformer stack  
   - Develop attention mechanisms based on box intersection volumes

2. **New loss functions & regularization**  
   - Geometry-aware penalties (e.g. box size, overlap ratios, hierarchical constraints)  
   - Reinforcement-style objectives tied to downstream performance  

3. **Explore alternative embedding families**  
   - Regional embeddings (hyperbolic, spherical, or other non-Euclidean geometries)
   - Probabilistic embeddings (Gaussian, mixture models)
   - Hybrid embeddings (points + regions/probabilistic)

4. **Evaluation benchmarks**  
   - Rare word generalization, polysemy, compositionality  
   - Uncertainty calibration and interpretability  
   - Data efficiency

---

## Acknowledgments

- Inspired by [Word2Box (Dasgupta et al., 2021)](https://arxiv.org/abs/2106.14361) and related regional embedding research.
- Box embedding utilities adapted from the official [Word2Box repository](https://github.com/iesl/word2box#).
