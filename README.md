
# MediChat: Your Personal Medical Assistant
# Overview

MediChat is a Flask-based generative AI medical chatbot built with LangChain, Pinecone, and Hugging Face models. It allows users to ask medical questions and get AI-generated answers, grounded in trusted medical sources (e.g., Gale Encyclopedia of Medicine). This project demonstrates retrieval-augmented generation (RAG) for healthcare knowledge.
Clone the repository 

# Features
- Conversational medical Q&A interface with context awareness

- RAG pipeline: combines embeddings + Pinecone vector database + Hugging Face LLM

- Backend powered by Flask

- Knowledge base built from the Gale Encyclopedia of Medicine

- Modular code structure (src/ helpers & prompts)

- Easy-to-extend for other domains beyond healthcare

# Project Structure
├── app.py # Flask app (chat backend)

├── store_index.py # Script to index PDF data into Pinecone

├── template.py # Boilerplate file creator

├── requirements.txt # Python dependencies

├── setup.py # Package setup

├── Data/ # Medical reference PDFs

│ └── Gale Encyclopedia of Medicine Vol.1.pdf

├── src/

│ ├── helper.py # Utilities: PDF loading, text splitting, embeddings

│ ├── prompt.py # System prompts

│ └── __init__.py

└── research/trails.ipynb # Jupyter notebook (experiments)

# Installation

1) Clone the repository:
   
- git clone <repo_url>
- cd medichat
  
2) Create and activate a virtual environment:
   
  - python -m venv .venv
  - .\.venv\Scripts\activate
  
3)Install dependencies:

- pip install -r requirements.txt
  
4)Create a .env file in the root directory:

- PINECONE_API_KEY=your_pinecone_api_key

# Indexing Knowledge Base

Before running the chatbot, index the medical PDF into Pinecone:
- python store_index.py

This will:
- Load PDFs from Data/
- Split text into chunks
- Generate embeddings (sentence-transformers)
- Store them in Pinecone index medicine

# Running the Chatbot

Start the Flask server:
- python app.py

The app will run at: http://localhost:8080

# Key Components
- Embeddings: Hugging Face sentence-transformers (384-dim vectors)
- Vector Store: Pinecone (cosine similarity search)
- LLM: google/flan-t5-base via HuggingFacePipeline
- Framework: LangChain for RAG orchestration
- Frontend: HTML template served with Flask (index.html)

# Workflow (RAG Pipeline)

1)User submits a query through the chat UI.

2)Query is converted into embeddings.

3)Pinecone retrieves the most relevant chunks from the medical knowledge base.

4)Retrieved text + user query are passed into flan-t5-base via LangChain.

5)LLM generates a natural language answer.

6)Response is returned to the frontend.

# License

This project is licensed under the MIT License.
