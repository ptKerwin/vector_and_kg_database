*This repository is a demonstration of building RAG, using a Knowledge Graph(Neo4j) and vector database(ChromaDB), with a Large Language Model(Groq).*
*kg_document and vector_document illustrate the program details*

## KG Database - Neo4j
*For the program detail, Please refer to the kg_document*

**Graph RAG with Neo4j & LangChain**

This repository provides a hands-on implementation of Graph RAG (Retrieval-Augmented Generation) by integrating a Knowledge Graph with a vector database. Using Neo4j as the underlying graph database, LangChain as the orchestration framework, and Groq's high-speed open-source model (Mixtral), this project demonstrates how to automatically transform unstructured Wikipedia text into a structured graph and build an intelligent Q&A system that supports Hybrid Retrieval and Conversational Memory.

**Core Features**

Automated Knowledge Graph Construction: Leverages an LLM to automatically extract entities and relationships from unstructured text without manual annotation.

**Hybrid Retrieval Architecture:**
- Structured Retrieval: Extracts entities from user queries and uses Cypher queries to retrieve relevant nodes and relationship paths in Neo4j.
- Unstructured Retrieval: Converts text chunks into vector embeddings and performs semantic similarity searches using Neo4j's built-in vector search capabilities.
- Dynamic Graph Visualization: Integrates yfiles_jupyter_graphs to render interactive previews of the knowledge graph directly within the Jupyter Notebook.
- Context-Aware Conversational Chain: Automatically rephrases follow-up questions based on chat history to provide a seamless and coherent conversational experience.

**Tech Stack**

- Large Language Model (LLM): Groq (mixtral-8x7b-32768) - Handles entity extraction, graph transformation, and final answer generation.
- Graph Database: Neo4j (AuraDB / Local)
- Development Framework: LangChain (langchain-core, langchain-community, langchain-experimental, langchain-neo4j)
- Embeddings Model: HuggingFace (sentence-transformers/all-MiniLM-L6-v2)
- Data Source: Wikipedia API
- Visualization: yfiles_jupyter_graphs

**Pipeline Overview**

1. Data Ingestion: Loads topic-specific articles (e.g., Queen Elizabeth I) using WikipediaLoader and splits the text into manageable chunks using TokenTextSplitter.
2. Graph Extraction: Passes the chunked text through the LLMGraphTransformer, prompting the Groq model to extract GraphDocuments (Nodes and Relationships), which are then ingested into the Neo4j database.
3. Vector Indexing: Generates text embeddings via HuggingFace and creates a vector index in Neo4j (Neo4jVector) to enable Hybrid Search.

**Intelligent Retrieval & Generation:**
When a user asks a question, the system condenses the query using the chat history.
It extracts entities to generate a Cypher Query for structured graph retrieval.
It simultaneously performs a Vector Similarity Search for unstructured context.
Both contexts are combined and fed into the LLM to generate a precise, grounded answer.

**Example Execution**

Question: "Which house did Elizabeth I belong to?"

Graph Search: Retrieves the relationship Elizabeth I - MEMBER_OF -> House Of Tudor.

Answer: "Elizabeth I belonged to the House of Tudor."

## Vector Database - ChromaDB
*For the program detail, Please refer to the vector_document*

This repository demonstrates how to build a Retrieval-Augmented Generation (RAG) question-answering system using a vector database (ChromaDB) and a Large Language Model (LLM) with LangChain. The workflow includes document ingestion, text chunking, embedding, vector storage, and conversational retrieval.

**Workflow**
1. Document Loading: Load local PDF documents using PyPDFLoader.
2. Text Chunking: Split the extracted text into manageable chunks with RecursiveCharacterTextSplitter.
3. Vector Embedding: Use HuggingFace's sentence-transformers/all-MiniLM-L6-v2 to convert text chunks into dense vector embeddings.
4. Vector Storage: Store the embeddings in ChromaDB for efficient similarity search.
5. Conversational Retrieval: Implement a chatbot chain using LangChain's prompt templates and Groq's LLM (mixtral-8x7b-32768) to answer user questions based strictly on retrieved context.

**Tech Stack**
- LLM: Groq (mixtral-8x7b-32768)
- Vector Database: ChromaDB
- Framework: LangChain
- Embeddings: HuggingFace sentence-transformers/all-MiniLM-L6-v2
- Document Loader: PyPDFLoader
