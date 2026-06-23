# Generation Notes

Mode: ai

Model: gemini / gemini-2.5-flash

Fallback reason: OpenAI limit reached. Automatically switched to Gemini.

Architecture: Customer Support KB Search

Template path: templates/simple-rag/customer-support-kb-search

Short description:

A beginner-friendly RAG system for analyzing customer success documentation, enabling quick extraction of key insights, challenges, and outcomes from unstructured text.

Architecture notes:

- This architecture emphasizes simplicity and ease of setup for beginners. FastAPI is chosen for its high performance and ease of learning Python APIs. React provides a modern, component-based UI. ChromaDB is an excellent choice for a beginner RAG project due to its straightforward API and capability to run in-memory or as a lightweight persistent store without complex external dependencies. Using a local embedding model (Sentence Transformers) avoids external API costs and dependencies for a core RAG component. The LLM can be swapped between a local Ollama setup (for full local control) or a standard API (like GPT-3.5-turbo) by configuring the backend, making it flexible for development and deployment. The focus is on a single-tenant, document-based RAG flow.

Project planner agent workflow:

- Architecture Agent: Define app boundaries, data flow, runtime stack, and integration points. Outputs: This architecture emphasizes simplicity and ease of setup for beginners. FastAPI is chosen for its high performance and ease of learning Python APIs. React provides a modern, component-based UI. ChromaDB is an excellent choice for a beginner RAG project due to its straightforward API and capability to run in-memory or as a lightweight persistent store without complex external dependencies. Using a local embedding model (Sentence Transformers) avoids external API costs and dependencies for a core RAG component. The LLM can be swapped between a local Ollama setup (for full local control) or a standard API (like GPT-3.5-turbo) by configuring the backend, making it flexible for development and deployment. The focus is on a single-tenant, document-based RAG flow.
- Backend Agent: Design FastAPI modules, service contracts, validation, and error handling. Outputs: Document Ingestion Service: Handles file uploads, processes documents into chunks, generates embeddings, and stores them in ChromaDB.; RAG Query Service: Receives user queries, embeds them, performs vector search in ChromaDB, retrieves relevant document chunks, constructs a prompt, and sends it to the LLM for generating an answer.; Health Check Service: Provides a simple endpoint to check the backend's operational status.
- Frontend Agent: Design React screens, state flow, controls, and user feedback states. Outputs: File Upload Interface: Allows users to drag-and-drop or select multiple text-based documents (PDF, TXT, DOCX) for ingestion.; Search Bar: An input field for users to type natural language questions related to their uploaded customer success documents.; Response Display Area: Shows the AI-generated answer clearly, along with citations to the original source documents and specific text chunks.; Loading Indicators: Visual feedback during document processing and query response generation.; Error Handling UI: Displays user-friendly messages for file upload failures or API errors.
- Database Agent: Design persistence models, sample data, indexes, and audit records. Outputs: Run history; Source document metadata; Generated workflow audit records
- Testing Agent: Define contract tests, smoke tests, and generated project validation. Outputs: For backend: Test individual functions like chunking, embedding generation, vector search logic, and prompt construction. For frontend: Test individual React components for rendering and basic interaction.; Test the full RAG pipeline: upload document -> query -> get response with citations. Verify correct data flow between services (FastAPI, ChromaDB, LLM integration).; Simulate user interaction (e.g., Cypress/Playwright) to ensure the UI behaves as expected when interacting with the backend and displaying results.; Basic tests to measure latency for document ingestion and query response times with a small dataset to ensure beginner-friendly performance.; Using a small, fixed set of documents and queries, assert that the RAG system returns relevant information and correct citations.
- DevOps Agent: Define environment variables, Docker workflow, and repository packaging. Outputs: Docker-ready project; Environment sample file; GitHub repository upload
- Reviewer Agent: Review the generated plan for completeness, security, and portfolio quality. Outputs: 1. User navigates to the application's home page.; 2. User uploads customer success documents (e.g., 'customer_acme_q1_review.txt', 'customer_globex_feedback.txt') via the drag-and-drop interface.; 3. Backend receives documents, performs OCR (if PDF) and text extraction, chunks the text, generates embeddings using the local embedding model, and stores chunks and embeddings in ChromaDB.; 4. Frontend indicates 'Documents processed successfully'.; 5. User enters a natural language query into the search bar, e.g., 'What were Acme Corp's Q1 challenges?'.; 6. Frontend sends the query to the backend's RAG Query Service.
