# RAG Olive Oil Assistant

A Jupyter Notebook that demonstrates a Retrieval-Augmented Generation (RAG) system for recommending olive oils based on sensory descriptions.

## Features

- Loads olive oil sensory data
- Creates vector embeddings using Sentence Transformers
- Stores vectors in Qdrant for similarity search
- Uses a local LLM (via Ollama) to generate personalized recommendations

## Dataset

The dataset (`Olive_Oil_Sensory_Dataset_International.csv`) is AI-generated and contains fictional olive oil descriptions for demonstration purposes.

## Setup

1. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

2. Ensure Ollama is installed and running locally with the qwen2.5:3b model:
   ```
   ollama pull qwen2.5:3b
   ```

3. Run the notebook cells in order.

## Usage

Execute the cells in the `embeddings.ipynb` notebook to:
- Load and process data
- Build the vector database
- Perform searches and generate recommendations

## Note

This is a demo project. The dataset is synthetic and not based on real data.