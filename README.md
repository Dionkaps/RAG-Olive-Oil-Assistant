# RAG Olive Oil Assistant

A small demo project that shows how to build a Retrieval-Augmented Generation (RAG) pipeline for olive-oil recommendations using a local language model and a vector database. The core is a single Jupyter notebook, `embeddings.ipynb`, which walks through data loading, embedding creation, vector storage, similarity search, and instruction-driven response generation.

## Table of contents

- Project overview
- Dataset
- Architecture and components
- Prerequisites
- Quick start
- Running the notebook (step-by-step)
- Configuration & environment
- Troubleshooting
- Contributing
- License

## Project overview

This repository demonstrates:

- How to convert textual sensory descriptions for olive oils into vector embeddings.
- How to store and query those embeddings with a vector database (Qdrant).
- How to combine retrieval results with a local LLM (via Ollama) to generate personalized recommendations and explanations.

Intended audience: developers, data scientists, and researchers who want a runnable example of RAG workflows using local tooling.

## Dataset

File: `Olive_Oil_Sensory_Dataset_International.csv`

- Contains fictional, AI-generated olive oil sensory profiles for demonstration only.
- Columns include (example): id, brand, origin, sensory_notes, bitterness, pungency, fruity_score, quality_label.
- Not for production use or scientific claims—only for demo and testing.

If you want to use your own dataset, make sure it contains a text field with human-readable sensory notes and a unique id per record.

## Architecture and components

- embeddings.ipynb — the main notebook that wires everything together.
- `requirements.txt` — Python dependencies used by the notebook.
- Ollama — provides a local LLM (example: qwen2.5:3b) used to generate recommendations. This keeps data local and reduces API costs.
- Qdrant — vector database used for storing and searching embeddings.

## Prerequisites

- Python 3.10+ (3.11 recommended)
- pip
- Jupyter / JupyterLab to run `embeddings.ipynb`
- Ollama installed and running locally (if you want to use a local LLM)
- Qdrant running locally or accessible remotely

Optional (the notebook may include alternatives):
- GPU for faster embedding generation and model inference

## Quick start

1. Clone the repository and change into the folder:

```powershell
cd C:\Users\vpddk\Desktop\Me\Github\RAG-Olive-Oil-Assistant
```

2. Install Python dependencies:

```powershell
pip install -r requirements.txt
```

3. (Optional) Start Qdrant locally (example using Docker):

```powershell
docker run -p 6333:6333 -it --rm qdrant/qdrant
```

4. (Optional) Install and start Ollama, then pull a model (example):

```powershell
# visit https://ollama.com for installer; once installed:
ollama pull qwen2.5:3b
```

5. Launch Jupyter and open `embeddings.ipynb`:

```powershell
jupyter lab
```

## Running the notebook (recommended order)

The notebook is written as a guided walkthrough. Follow cells in order. High-level steps:

1. Inspect dataset and sample rows.
2. Preprocess text (cleaning, concatenation of fields if needed).
3. Load a sentence-transformer model (or alternative embedding model) and compute embeddings.
4. Connect to Qdrant and upsert vectors (include metadata fields for later filtering).
5. Run similarity searches for sample queries and inspect nearest neighbors.
6. Build a prompt that includes retrieval results and send it to the LLM via Ollama to generate a recommendation.

Tips:
- Work on a subset of the dataset while experimenting to save time.
- Persist the Qdrant collection so you can re-run only the LLM steps.

## Configuration & environment

- The notebook may look for environment variables or configuration values such as:
  - QDRANT_URL / QDRANT_API_KEY
  - OLLAMA_HOST / OLLAMA_PORT
  - EMBEDDING_MODEL_NAME

Set them in your shell or modify the notebook to include hard-coded local values for testing.

## Troubleshooting

- If pip install fails: create or activate a virtualenv and retry.
- Qdrant connection refused: ensure the server is running and the port is correct (default 6333).
- Ollama errors: verify Ollama daemon is running and the model is pulled; check `ollama ps`.
- Slow embedding generation: try batching or using a smaller embedding model.

## Contributing

Contributions are welcome. Small, well-scoped PRs are easiest to review. Examples of helpful contributions:

- Add unit tests or example notebooks for alternative embedding models.
- Add a small script to automate Qdrant population.
- Improve prompts used for the LLM or add more example queries.

Before opening a PR:

1. Run the notebook to ensure the workflow still runs end-to-end.
2. Keep changes minimal and document them in the PR description.

## License

This project is provided for educational/demo purposes. Check the repository settings or add a LICENSE file if you plan to relicense or publish.

---

If you'd like, I can also:

- Add a short quick-run script that populates Qdrant from the CSV.
- Add a small example prompt and expected output in the README.

Tell me which extras you'd prefer and I'll implement them.