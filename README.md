# RAG NVIDIA Training

This repository contains the notebooks and supporting code used to build and evaluate Retrieval-Augmented Generation (RAG) workflows with LangChain, FAISS, and NVIDIA endpoints (ChatNVIDIA, NVIDIAEmbeddings). It follows the sequence of course notebooks:

- `03_langchain_intro.ipynb`: LCEL basics and simple chat examples.
- `04_running_state.ipynb`: Running-state chains and dialog management.
- `05_documents.ipynb`: Document chunking and progressive summarization.
- `06_embeddings_old.ipynb`: Embedding models and similarity experiments.
- `07_vectorstores.ipynb`: Building vector stores for RAG.
- `08_evaluation.ipynb`: LLM-as-a-judge evaluation of the RAG pipeline.
- `09_langserve.ipynb`: Exposing chains via LangServe (`/basic_chat`, `/retriever`, `/generator`).
- `64_guardrails.ipynb`: Semantic guardrailing with embeddings and classifiers.

To serve the RAG API (LangServe):
1) Ensure `docstore_index.tgz` is present (built from your documents with the same embedder).
2) Run `server_app.py` (written from `09_langserve.ipynb`) to expose:
   - `/basic_chat`
   - `/retriever`
   - `/generator`
3) Point the frontend or evaluator to `http://<host>:9012/`.

To evaluate (Notebook 8):
- Load `docstore_index.tgz`, rebuild the RAG chain, generate synthetic Q/A pairs, and run the LLM judge to score grounding quality.

Notes:
- Use the same embedding model for building and loading FAISS (e.g., `nvidia/nv-embed-v1`).
- Include at least one recent Arxiv paper in the index for the assessment.
- If retrieval feels weak, increase top-k (e.g., `k=4..6`) and keep prompts strict: “answer only from context; say if insufficient.”

License: MIT (add your preferred license if different).

