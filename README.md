# 🏥 Medical Chatbot with LLMs, LangChain, Pinecone, Flask & AWS

A production-ready, end-to-end **Generative AI Medical Chatbot** that answers natural language medical queries by intelligently retrieving information from a medical book PDF. Built with LangChain, a **local Ollama Llama 3.2 model**, HuggingFace embeddings, Pinecone vector database, and deployable on AWS via a fully automated CI/CD pipeline.


---

## 📋 Table of Contents

- [Overview](#overview)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [How It Works](#how-it-works)
- [Local Setup](#local-setup)
- [AWS CI/CD Deployment](#aws-cicd-deployment-with-github-actions)
- [Environment Variables](#environment-variables)
- [License](#license)

---

## Overview

This project demonstrates how to convert a large medical book (PDF) into a searchable, conversational knowledge base using **Retrieval-Augmented Generation (RAG)** — entirely with a **free, locally-run LLM** (no OpenAI API key required for inference).

Users can ask natural language questions and receive accurate, contextually grounded answers drawn directly from the source document. The welcome message and interface are in French, making it suitable for French-speaking users.

Key capabilities:
- Parses and chunks a medical PDF into semantically meaningful segments
- Generates embeddings using HuggingFace sentence transformers (free, local)
- Stores and retrieves embeddings from Pinecone for fast similarity search
- Uses **Ollama + Llama 3.2** (running locally) as the LLM — no OpenAI cost
- Serves the chatbot through a Flask web application
- Deploys to AWS EC2 via Docker, ECR, and GitHub Actions

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Python 3.10 |
| LLM | [Ollama](https://ollama.com/) — Llama 3.2 (default: `llama3.2:1b`) |
| Embeddings | HuggingFace Sentence Transformers (local) |
| Orchestration | LangChain |
| Vector Database | Pinecone |
| Web Framework | Flask |
| Containerization | Docker |
| CI/CD | GitHub Actions |
| Cloud | AWS EC2 + ECR |

---

## Project Structure

```
├── .github/
│   └── workflows/          # GitHub Actions CI/CD pipeline
├── data/
│   └── Medical_book.pdf    # Source medical document
├── research/               # Notebooks for experimentation
├── src/
│   ├── helper.py           # HuggingFace embeddings loader
│   └── prompt.py           # System prompt definition
├── static/                 # CSS and front-end assets
├── templates/
│   └── chat.html           # Flask chat UI template
├── app.py                  # Flask application entrypoint
├── store_index.py          # Script to embed & store vectors in Pinecone
├── requirements.txt        # Python dependencies
├── setup.py                # Package setup
├── Dockerfile              # Docker container definition
├── template.sh             # Project scaffolding script
└── .env                    # Environment variables (not committed)
```

---

## How It Works

1. **PDF Ingestion** — `store_index.py` loads the medical PDF using LangChain document loaders.
2. **Text Chunking** — The document is split into overlapping chunks for better semantic coverage.
3. **Embedding** — Each chunk is converted to a vector using **HuggingFace sentence transformers** (runs locally, no API cost).
4. **Vector Storage** — Embeddings are upserted into a Pinecone index (`medical-chatbot`) for fast nearest-neighbor retrieval.
5. **Query Flow** — When a user submits a question:
   - The query is embedded using the same HuggingFace model
   - Top 3 most similar chunks are retrieved from Pinecone (`k=3`)
   - Retrieved context + the question are passed to **Ollama Llama 3.2** via a RAG chain
   - The LLM generates a grounded answer from the context
6. **Web Interface** — Flask serves the chat UI at `http://localhost:8080`.

---

## Local Setup

### Prerequisites

- Python 3.10
- Conda
- [Ollama](https://ollama.com/download) installed and running locally
- A [Pinecone](https://www.pinecone.io/) account and API key

### Steps

**1. Clone the repository**

```bash
git clone https://github.com/chouaieb161/Build-a-Complete-Medical-Chatbot-with-LLMs-LangChain-Pinecone-Flask-AWS.git
cd Build-a-Complete-Medical-Chatbot-with-LLMs-LangChain-Pinecone-Flask-AWS
```

**2. Pull the Llama 3.2 model via Ollama**

```bash
ollama pull llama3.2:1b
```

Make sure the Ollama server is running before launching the app:

```bash
ollama serve
```

**3. Create and activate a conda environment**

```bash
conda create -n medibot python=3.10 -y
conda activate medibot
```

**4. Install dependencies**

```bash
pip install -r requirements.txt
```

**5. Configure environment variables**

Create a `.env` file in the root directory:

```env
PINECONE_API_KEY=your_pinecone_api_key_here
OLLAMA_MODEL=llama3.2:1b   # optional, this is the default
```

**6. Build and store the Pinecone index**

Run this **once** to process the PDF and populate Pinecone with embeddings:

```bash
python store_index.py
```

**7. Launch the application**

```bash
python app.py
```

Open your browser and navigate to `http://localhost:8080`.

---

## Environment Variables

| Variable | Required | Default | Description |
|---|---|---|---|
| `PINECONE_API_KEY` | ✅ Yes | — | Your Pinecone project API key |
| `OLLAMA_MODEL` | ❌ No | `llama3.2:1b` | Ollama model tag to use for inference |

> No OpenAI API key is needed. Both the LLM (Ollama) and embeddings (HuggingFace) run locally.

---
# AWS-CICD-Deployment-with-Github-Actions

## 1. Login to AWS console.

## 2. Create IAM user for deployment

	#with specific access

	1. EC2 access : It is virtual machine

	2. ECR: Elastic Container registry to save your docker image in aws


	#Description: About the deployment

	1. Build docker image of the source code

	2. Push your docker image to ECR

	3. Launch Your EC2 

	4. Pull Your image from ECR in EC2

	5. Lauch your docker image in EC2

	#Policy:

	1. AmazonEC2ContainerRegistryFullAccess

	2. AmazonEC2FullAccess

	
## 3. Create ECR repo to store/save docker image
    - Save the URI: 315865595366.dkr.ecr.us-east-1.amazonaws.com/medicalbot

	
## 4. Create EC2 machine (Ubuntu) 

## 5. Open EC2 and Install docker in EC2 Machine:
	
	
	#optinal

	sudo apt-get update -y

	sudo apt-get upgrade
	
	#required

	curl -fsSL https://get.docker.com -o get-docker.sh

	sudo sh get-docker.sh

	sudo usermod -aG docker ubuntu

	newgrp docker
	
# 6. Configure EC2 as self-hosted runner:
    setting>actions>runner>new self hosted runner> choose os> then run command one by one


# 7. Setup github secrets:

   - AWS_ACCESS_KEY_ID
   - AWS_SECRET_ACCESS_KEY
   - AWS_DEFAULT_REGION
   - ECR_REPO
   - PINECONE_API_KEY
