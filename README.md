# Does Data Format Affect RAG?
A hands-on benchmark exploring whether identical information behaves differently inside a Retrieval-Augmented Generation (RAG) pipeline when represented as JSON, YAML, TOON, and Minified JSON.


## Why I Built This

Several months ago, I came across TOON (Token-Oriented Object Notation), a format designed around token efficiency for Large Language Models.

The idea was interesting:

Could a format designed specifically for LLMs outperform traditional formats such as JSON?

Rather than accepting the claim at face value, I decided to test it.

What started as curiosity about data formats eventually became a practical benchmark involving:

- Token efficiency
- Chunking behavior
- Embeddings
- Vector search
- Retrieval-Augmented Generation (RAG)
- Answer evaluation

This repository documents that journey and the findings that came from it.



## Research Question

If the underlying information is identical, will a RAG pipeline retrieve and answer the same way when the data is represented differently?
