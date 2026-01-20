Abstract-Only PubMed RAG — README (Brief)

What this is?

A proof-of-concept RAG pipeline built on PubMed titles/abstracts only (no PDFs). It’s designed to support implant/knee arthroplasty literature grounding while avoiding full-text parsing issues.

Pipeline overview
	1.	PubMed retrieval: Query PubMed (topic-based), pull PMIDs + metadata + abstracts in batches, apply basic rate limiting, and save to a structured table (CSV).
	2.	Chunking: Split each abstract into smaller chunks to improve retrieval granularity and reduce mixed-topic hits; retain full provenance metadata per chunk (PMID, title, journal, year, chunk index, etc.).
	3.	Embedding + Vector DB: Embed each chunk with an open-source model and store vectors + metadata in Qdrant for semantic search.
	4.	Hybrid retrieval: For a user query, retrieve candidates using BM25 (lexical) + dense vector search, then fuse results (e.g., Reciprocal Rank Fusion) to return a final top-k set for LLM context.

What to review / comment on
	•	Whether the PubMed search strategy (terms + AND/OR logic + date limits) is appropriately inclusive.
	•	Chunk size/overlap defaults for abstracts.
	•	The choice of embedding model for the first baseline.
	•	The chosen top-k for context and fusion strategy for hybrid retrieval.

Next optional step

A small proof-of-concept evaluation using ~46k abstracts and a set of realistic implant-selection queries to sanity-check retrieval quality before scaling further.
