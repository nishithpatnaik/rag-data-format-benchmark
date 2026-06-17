# Does Data Format Affect RAG?
A hands-on benchmark exploring whether identical information behaves differently inside a Retrieval-Augmented Generation (RAG) pipeline when represented as JSON, YAML, TOON, and Minified JSON.


## Why I Built This

Several months ago, I came across TOON (Token-Oriented Object Notation), a format designed around token efficiency for LLMs.

Could a format designed specifically for LLMs optimize token consumption, influence performance & behaviour inside a real Retrieval-Augmented Generation (RAG) system?

I wanted to test that theory, but at the time, I didn't have a good way to test that theory.. Later, while learning and experimenting with RAG systems, I found myself revisiting the same question. I realized I now had the tools to evaluate it properly rather than relying on assumptions or claims.

That curiosity eventually led to this case study.

What started as an interest in TOON, became a practical benchmark involving:

- Token efficiency
- Chunking behavior
- Embeddings
- Vector search
- Retrieval-Augmented Generation (RAG)
- Answer evaluation

In this repository I will document my journey capturing benchmark design, results, and lessons learned from that exploration.



## Research Question

If the underlying information is identical, will a RAG pipeline retrieve and answer the same way when the data is represented differently?



## Approach

I split the project into two parts.

### Part 1 - Format Fidelity Validation

Before comparing formats, I wanted to make sure they all preserved the same information.

The same dataset was represented as:

* JSON (Pretty)
* JSON (Minified)
* YAML
* TOON

I then validated that each format contained the same underlying data before moving to the benchmark.

### Part 2 - RAG Benchmark

Each format was processed using the same workflow:

```text
Dataset
↓
Chunking
↓
Embeddings
↓
FAISS Index
↓
Retrieval
↓
Answer Generation
```

The only thing that changed was the representation format.

Everything else remained the same making this a fair comparison of token efficiency, retrieval behavior, and answer generation.

