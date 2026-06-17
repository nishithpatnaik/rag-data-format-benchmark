# Does Data Format Affect RAG?
A hands-on benchmark exploring whether identical information behaves differently inside a Retrieval-Augmented Generation (RAG) pipeline when represented as JSON, YAML, TOON, and Minified JSON.


## Why I Built This

Several months ago, I came across TOON (Token-Oriented Object Notation), a format designed around token efficiency for LLMs.

Could a format designed specifically for LLMs optimize token consumption, influence behaviour inside a real Retrieval-Augmented Generation (RAG) system?

I wanted to test that theory, but at the time, I didn't have a practical way to do it.. Later, while learning and experimenting with RAG systems, I found myself revisiting the same question. I realized I now had the tools to evaluate it properly rather than relying on assumptions or claims.

That curiosity eventually led to this case study.

What started as an interest in TOON became a practical benchmark involving:

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

Before comparing formats, I wanted to make sure they all preserved the same information. Otherwise, any differences observed later could simply be the result of missing or altered data.

The same dataset was represented as:

* JSON (Pretty)
* JSON (Minified)
* YAML
* TOON

I then validated that each format preserved the same underlying information before moving to the benchmark.

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

Everything else remained the same, making it easier to isolate the uninteded impact on token efficiency, retrieval behavior, and answer generation.



## Results

### File Size and Token Comparison

| Format | Size (Bytes) | Tokens |
|----------|----------:|----------:|
| JSON Minified | 118,167 | 32,061 |
| TOON | 139,190 | 35,334 |
| YAML | 132,961 | 36,615 |
| JSON Pretty | 178,370 | 42,465 |

For this dataset, JSON Minified was the most efficient format in terms of both file size and token count.

One of my initial assumptions was that TOON would outperform traditional formats on token efficiency. That was not the case in this benchmark.



### Chunking Comparison

| Format        | Chunks |
| ------------- | -----: |
| JSON Minified |     72 |
| TOON          |     79 |
| YAML          |     82 |
| JSON Pretty   |     95 |

Even though all four formats contained the same information, they did not produce the same number of chunks.

This was my first indication that representation could influence retrieval behavior.

More chunks means:

* More embeddings
* A larger vector index
* More retrieval candidates

At this stage, the benchmark started to move beyond token efficiency and into retrieval behavior.



## Key Findings

### 1. Minified JSON was the most token-efficient format

For this dataset, JSON Minified produced the lowest file size and token count.

### 2. Pretty formatting has a measurable cost

Pretty JSON preserved the same information but required significantly more tokens and produced more chunks.

### 3. Similarity score is not answer quality

One of the more interesting observations was that a higher similarity score did not always lead to a better answer.

A lower-scoring chunk could still generate a more complete response if it contained the right context.

### 4. Identical information does not guarantee identical retrieval behavior

Even after validating that all formats preserved the same information, retrieval behavior was not always identical.

Different representations created different chunk boundaries, different retrieval paths, and occasionally different answers.




## What Surprised Me

Going into this benchmark, I expected token efficiency to be the most interesting result. But it wasn't.

The bigger surprise was seeing how different representations could influence chunking and retrieval behavior even when the underlying information remained unchanged.

That reinforced an important lesson:

In RAG systems, the way information is represented can matter just as much as the information itself.






## Conclusion

I started this project to test a claim about TOON and token efficiency.

What surprised me most was not the token counts.

It was discovering that identical information does not always behave the same way inside a RAG pipeline.

For this dataset, JSON Minified was the most efficient representation. However, the more interesting lesson was that representation can influence chunking, retrieval, and ultimately the context provided to an LLM.

In RAG systems, formatting is not just formatting.




## Repository Contents

- 01_Input_data_format_fidelity_validation.ipynb
- 02_RAG_Benchmark_JSON_TOON_YAML.ipynb






