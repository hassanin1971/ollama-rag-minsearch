Ollama RAG Course Assistant 🚀

An end-to-end, locally deployed Retrieval-Augmented Generation (RAG) system designed to act as an intelligent FAQ assistant for course participants. By pivoting from centralized cloud models to a decentralized, sovereign architecture, this project leverages local LLM execution to guarantee absolute data privacy and rapid response times.

🛠️ Architecture Overview

The system operates on a dual-stage architecture engineered for high-performance context injection:

Information Retrieval Stage: Utilizes a lightweight, memory-efficient inverted index (minsearch) to parse data collections and fetch the top-N relevant document blocks based on semantic or lexical matching.

Contextual Inference Stage: Orchestrates a local instance of Ollama (llama3.2:latest) to synthesize the retrieved knowledge boundaries and formulate precise, hallucination-free responses.

[User Question] ──> [minsearch (Inverted Index)] ──> [Context Extracted]
                                                             │
[Accurate Answer] <── [Ollama Inference Engine] <────────────┘


📋 Prerequisites

Ensure your system meets the following foundational technical requirements:

Python: v3.10 or higher

Ollama Runtime: Installed and running in the background. Download Ollama here.

Local Hardware: A modern CPU/GPU environment capable of containerizing local model weights.

🚀 Local Setup and Installation

Follow these methodical execution steps to replicate the environment on your local machine:

1. Clone the Repository

git clone https://github.com/YOUR_USERNAME/ollama-rag-minsearch.git
cd ollama-rag-minsearch


2. Initialize Virtual Environment and Dependencies

This project utilizes modern package management. Ensure your dependencies are aligned:

# Create virtual environment
python -m venv .venv
source .venv/bin/activate  # On Windows use: .venv\Scripts\activate

# Install the verified dependency stack
pip install jupyter minsearch openai python-dotenv requests sqlitesearch ollama


3. Pull the Local Inference Model

Make sure the Ollama daemon is active, then download the targeted lightweight model weights:

ollama pull llama3.2:latest


4. Environment Configuration

Create a .env file in the root directory to store your execution parameters dynamically:

OLLAMA_HOST=http://localhost:11434
OLLAMA_MODEL=llama3.2:latest
ENVIRONMENT=development


🏃‍♂️ Running the Pipeline

The codebase is split into an ingestion script and an object-oriented execution assistant:

Step 1: Ingest the Knowledge Base

Run the ingestion mechanism to download, clear, parse, and structure the data into the local index:

python ingest.py


Step 2: Query the RAG Assistant

Open the interactive environment (notebook.ipynb) or execute a Python script to initiate the agent:

import ollama
from minsearch import Index
from rag_helper import RAGBase

# 1. Initialize and fit your index with documents
index = Index(
    text_fields=['question', 'section', 'answer'],
    keyword_fields=['course']
)
# Assumes 'documents' list is populated via ingestion
index.fit(documents)

# 2. Instantiate the Object-Oriented Assistant
assistant = RAGBase(index=index, llm_client=ollama, model='llama3.2:latest')

# 3. Prompt the engine safely
response = assistant.rag('I just discovered the course, can I still join?')
print(response)


🛡️ Sovereign AI & Data Privacy

Unlike conventional setups that offload enterprise prompts to external cloud black-boxes, this system processes data completely within your edge boundary. No data ever leaves your machine, transforming this pipeline into an ideal template for processing secure or sensitive operational records.

📄 License

This repository is open-source and available under the MIT License.