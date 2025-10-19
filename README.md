# RAG Olive Oil Assistant

An interactive demo that shows how to build a small Retrieval-Augmented Generation (RAG) pipeline to recommend olive oils from sensory descriptions.

This repository contains a Jupyter notebook, a synthetic olive oil sensory dataset, and the minimal requirements to reproduce the demo locally.

## Quick summary

- Goal: demonstrate how embeddings + a vector database + a local LLM can power natural-language recommendations over a small domain dataset.
- Primary artifact: `embeddings.ipynb` — a runnable notebook that walks through data loading, embedding, indexing, searching, and generating recommendations.
- Data: `Olive_Oil_Sensory_Dataset_International.csv` (synthetic/sample data for demonstration).

## Features

- Load and inspect the olive oil sensory dataset
- Generate sentence embeddings (SentenceTransformers)
- Persist vectors to Qdrant for fast similarity search
- Query the vector DB and use a local LLM (Ollama) to produce human-friendly recommendations

## Requirements

- Python 3.9+ (3.10/3.11 recommended)
- pip
- Docker (optional) — recommended for running Qdrant locally
- Ollama installed locally with a supported model (optional if you use a remote API)

# RAG Olive Oil Assistant

An interactive demo that shows how to build a small Retrieval-Augmented Generation (RAG) pipeline to recommend olive oils from sensory descriptions.

This repository contains a Jupyter notebook, a synthetic olive oil sensory dataset, and the minimal requirements to reproduce the demo locally.

## Quick summary

- Goal: demonstrate how embeddings + a vector database + a local LLM can power natural-language recommendations over a small domain dataset.
- Primary artifact: `embeddings.ipynb` — a runnable notebook that walks through data loading, embedding, indexing, searching, and generating recommendations.
- Data: `Olive_Oil_Sensory_Dataset_International.csv` (synthetic/sample data for demonstration).

## Features

- Load and inspect the olive oil sensory dataset
- Generate sentence embeddings (SentenceTransformers)
- Persist vectors to Qdrant for fast similarity search
- Query the vector DB and use a local LLM (Ollama) to produce human-friendly recommendations

## Requirements

- Python 3.9+ (3.10/3.11 recommended)
- pip
- Docker (optional) — recommended for running Qdrant locally
- Ollama installed locally with a supported model (optional if you use a remote API)

## Setup (Windows / PowerShell)

1. Create and activate a virtual environment (recommended):

```powershell
python -m venv .venv; .\.venv\Scripts\Activate.ps1
```

2. Install Python dependencies:

```powershell
pip install -r requirements.txt
```

3. (Optional) Start Qdrant with Docker (quick local server):

```powershell
docker run -p 6333:6333 -v qdrant_storage:/qdrant/storage qdrant/qdrant:latest
```

4. (Optional) Install and prepare Ollama if you want to run the model locally. For this demo we used `qwen2.5:3b`:

```powershell
# install ollama from https://ollama.com (follow their installer for Windows)
# then pull the model
ollama pull qwen2.5:3b
```

Notes:

- If you don't have Ollama, adapt the notebook to use an API-based LLM (OpenAI, Anthropic, etc.). The notebook separates retrieval and generation steps to make this easy.

## How to run the demo

1. Start Qdrant (if using locally) and ensure it's reachable at http://localhost:6333.
2. Open the notebook in Jupyter or VS Code and run the cells in order:

```powershell
# start jupyter lab or notebook
jupyter lab
# or
jupyter notebook
```

3. Notebook outline:

- Data loading & brief EDA — inspect the CSV and sample records
- Embedding generation — creates sentence embeddings for selected text fields
- Indexing into Qdrant — creates/updates a collection with the vectors
- Retrieval examples — perform similarity search with sample queries
- Generation — combine retrieved passages with prompts sent to the LLM to produce recommendations

## Example queries

- "Recommend a fruity olive oil for salads"
- "Find oils with green, grassy notes and low bitterness"

The notebook retrieves the top-k similar descriptions, then uses the LLM to craft a short recommendation explaining why the oil fits the request.

## Dataset

`Olive_Oil_Sensory_Dataset_International.csv` is a synthetic dataset included for demonstration only. It contains columns describing sensory attributes (e.g., aroma, flavor, bitterness, pungency, descriptors).

To use your own data, provide a CSV with at minimum the following columns:

- `id` — unique identifier
- `name` — oil name
- `description` or `sensory_text` — free-text sensory description

## Troubleshooting

- Qdrant connection errors: confirm Docker is running and the container is reachable on port 6333. Run `docker ps` to verify the container is up.
- Ollama errors: ensure Ollama is installed and the model is pulled. Run `ollama list` to see available models.
- Dependency issues: recreate the virtual environment and reinstall dependencies.

## Next steps / Improvements

- Build a small web UI (Flask / FastAPI) to accept user queries and return recommendations
- Add evaluation: holdout set + retrieval/generation metrics
- Add automated tests for the embedding and indexing code paths
- Make the LLM backend pluggable (local Ollama vs. API) with a small adapter layer

## License & attribution

This repository is provided for educational/demo purposes. The dataset is synthetic. No license file is included; if you want to share this project publicly, consider adding an OSI-approved license such as MIT.

---

Happy experimenting! 🌿
