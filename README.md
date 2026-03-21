This repository is a demonstration of integrating a Knowledge Graph - Neo4j, and a Large Language Model(LLM).
# KG Database - Neo4j
🌐 Graph RAG with Neo4j & LangChain

This repository provides a hands-on implementation of Graph RAG (Retrieval-Augmented Generation) by integrating a Knowledge Graph with a vector database. Using Neo4j as the underlying graph database, LangChain as the orchestration framework, and Groq's high-speed open-source model (Mixtral), this project demonstrates how to automatically transform unstructured Wikipedia text into a structured graph and build an intelligent Q&A system that supports Hybrid Retrieval and Conversational Memory.

✨ Core Features

Automated Knowledge Graph Construction: Leverages an LLM to automatically extract entities and relationships from unstructured text without manual annotation.

Hybrid Retrieval Architecture:
Structured Retrieval: Extracts entities from user queries and uses Cypher queries to retrieve relevant nodes and relationship paths in Neo4j.
Unstructured Retrieval: Converts text chunks into vector embeddings and performs semantic similarity searches using Neo4j's built-in vector search capabilities.
Dynamic Graph Visualization: Integrates yfiles_jupyter_graphs to render interactive previews of the knowledge graph directly within the Jupyter Notebook.
Context-Aware Conversational Chain: Automatically rephrases follow-up questions based on chat history to provide a seamless and coherent conversational experience.

🛠️ Tech Stack

Large Language Model (LLM): Groq (mixtral-8x7b-32768) - Handles entity extraction, graph transformation, and final answer generation.
Graph Database: Neo4j (AuraDB / Local)
Development Framework: LangChain (langchain-core, langchain-community, langchain-experimental, langchain-neo4j)
Vector Embeddings: HuggingFace (sentence-transformers/all-MiniLM-L6-v2)
Data Source: Wikipedia API
Visualization: yfiles_jupyter_graphs

🚀 Pipeline Overview

Data Ingestion: Loads topic-specific articles (e.g., Queen Elizabeth I) using WikipediaLoader and splits the text into manageable chunks using TokenTextSplitter.
Graph Extraction: Passes the chunked text through the LLMGraphTransformer, prompting the Groq model to extract GraphDocuments (Nodes and Relationships), which are then ingested into the Neo4j database.
Vector Indexing: Generates text embeddings via HuggingFace and creates a vector index in Neo4j (Neo4jVector) to enable Hybrid Search.

Intelligent Retrieval & Generation:
When a user asks a question, the system condenses the query using the chat history.
It extracts entities to generate a Cypher Query for structured graph retrieval.
It simultaneously performs a Vector Similarity Search for unstructured context.
Both contexts are combined and fed into the LLM to generate a precise, grounded answer.

💡 Example Execution

Question: "Which house did Elizabeth I belong to?"

Graph Search: Retrieves the relationship Elizabeth I - MEMBER_OF -> House Of Tudor.

Answer: "Elizabeth I belonged to the House of Tudor."

# Vector Database - ChromaDB
🚀 RAG Implementation Demos: Vector DB & Knowledge Graph
This repository showcases two distinct approaches to Retrieval-Augmented Generation (RAG). It contains Jupyter Notebooks demonstrating how to build intelligent question-answering systems using a vector database (ChromaDB) and a graph database (Neo4j).

📁 Repository Contents

1. Vector DB RAG (RAG_with_vector_db(chromaDB).ipynb)
This notebook demonstrates a standard RAG pipeline using a vector database.
Data Ingestion: Loads local PDF documents using PyPDFLoader.
Text Chunking: Splits the extracted text into manageable chunks using the RecursiveCharacterTextSplitter.
Vector Storage: Stores the document embeddings locally using ChromaDB.
Document Chatbot: Implements a conversational chain (ChatPromptTemplate and RunnableAssign) that answers user questions based strictly on the retrieved context.

2. Graph RAG (RAG_With_Knowledge_graph(Neo4j).ipynb)
This notebook explores an advanced RAG architecture using a knowledge graph, ideal for handling complex entity relationships.

Automated Graph Extraction: Uses WikipediaLoader to fetch articles and utilizes LangChain's LLMGraphTransformer to automatically extract entities and relationships from unstructured text.
Graph Database Integration: Ingests the extracted graph documents into a Neo4j database.
Dynamic Visualization: Leverages yfiles_jupyter_graphs to render interactive previews of the knowledge graph directly within the notebook.
Hybrid Search & Memory: Combines vector similarity search with structured Cypher query retrieval, and condenses follow-up questions using chat history to maintain conversational context.

🛠️ Tech Stack

Large Language Model (LLM): Utilizes the Groq API (mixtral-8x7b-32768) for fast inference and generation.
Embeddings: Uses HuggingFace (sentence-transformers/all-MiniLM-L6-v2) to convert unstructured text into dense vectors.
Framework: Orchestrates prompts, retrievers, and models using LangChain (langchain-core, langchain-community, langchain-experimental).
Databases: Uses ChromaDB for vector storage and Neo4j for graph and hybrid retrieval.

💡 Getting Started

Clone this repository.
Install the required Python packages, including langchain, chromadb, neo4j, and langchain-groq.
Set up your Groq API Key to enable model inference.
For the Graph RAG notebook, configure your Neo4j database credentials (NEO4J_URI, NEO4J_USERNAME, NEO4J_PASSWORD).
