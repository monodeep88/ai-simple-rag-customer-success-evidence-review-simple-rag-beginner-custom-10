# Customer Success Evidence Review RAG

## Project Overview

Customer Success Evidence Review RAG is a complete full-stack AI project for **Simple RAG** at **Beginner** difficulty. It includes a FastAPI backend, a React frontend, sample documents, vector search with ChromaDB support, source citations, timeline logs, structured run storage, Docker files, and tests.

Customer Success (CS) is critical for driving product adoption, reducing churn, and increasing customer lifetime value. CS teams generate vast amounts of documentation including meeting notes, QBRs, support tickets, and feedback. Manually sifting through this evidence to identify trends, pain points, or success stories is time-consuming. This project provides a RAG solution to automate evidence review, helping CSMs quickly retrieve specific information, understand customer health, and prepare for engagements.

Difficulty controls project complexity, architecture depth, AI model selection, and how advanced the generated codebase is.

- Architecture depth: minimal backend, simple folder structure, easy README, low-cost/free model
- Selected architecture: Customer Support KB Search
- Template path: templates/simple-rag/customer-support-kb-search
- Generated stack: FastAPI backend, React UI, local vector fallback, simple tests
- README style: beginner-friendly setup and clear expected output

## Tech Stack

- Backend: Python, FastAPI, Pydantic, SQLAlchemy
- AI/RAG: LangChain-ready prompt layer, ChromaDB vector storage, local deterministic fallback model
- Workflow: Agent pipeline with planner, retrieval, tool, reasoning, and final answer steps
- Frontend: React and Vite
- Database: SQLite by default, PostgreSQL through Docker Compose
- Testing: pytest
- Difficulty: Beginner

## Generation Method

This project was generated with a template-based architecture engine. AI is used only for the blueprint, domain customization, sample data, prompts, and documentation. The codebase is produced from tested FastAPI/React/Docker templates rather than raw LLM source output.

## Project Type Satisfaction Map

This generated project satisfies **Simple RAG** through the runtime path below. The implementation is not only a README claim: the files listed after the diagram are generated in the repository and validated before GitHub push.

```text
[User]
  |
  | question / task details / tone / constraints
  v
[React Frontend]
  |
  | POST /api/ask
  v
[FastAPI Backend]
  |
  +--> [Vector Store / Sample Docs]
  |        |
  |        +-- retrieved context / cited sources
  |
  v
[Retriever]
  |
  v
[Citation Answer Builder]
  |
  v
[Final Answer Builder]
  |
  | answer + sources + timeline steps
  v
[React Frontend]
  |
  v
[User sees final output + agent timeline]
```

Runtime proof points:

- `frontend/src/App.jsx` renders the user workspace, starter prompts, answer panel, cited sources, and timeline.
- `backend/app/main.py` exposes `POST /api/ask` and returns the final answer, sources, timeline steps, and project type.
- `backend/app/services/pipeline.py` orchestrates the project-type flow: Retriever, Citation Answer Builder.
- `backend/app/services/vector_store.py` loads sample documents and retrieves relevant cited context.
- `backend/app/domain.py` contains the generated topic-specific workflow steps, business rules, tools, persona, and starter questions.
- `backend/app/db.py` stores each run so the generated app behaves like a real workflow tool instead of a static prompt demo.
- `backend/tests/test_project_contract.py` validates the API contract and project-type behavior.

Type-specific behavior:

- Flow style: User question -> load documents -> split chunks -> embed -> Chroma similarity search -> answer with citations.
- Visible output: final answer, cited sources, timeline steps, and project type.
- Validation gate: pytest, frontend build, Docker Compose config, and Docker build before repository upload.

## Folder Structure

```text
ai-simple-rag-customer-success-evidence-review-simple-rag-beginner-custom-10/
  backend/
app/
  main.py
  config.py
  db.py
  schemas.py
  data/sample_docs/
  services/
text.py
vector_store.py
llm.py
tools.py
pipeline.py
tests/
  test_project_contract.py
requirements.txt
Dockerfile
  frontend/
src/
  App.jsx
  main.jsx
  styles.css
package.json
Dockerfile
  docker-compose.yml
  .env.example
  README.md
  ARCHITECTURE.md
  WHY_THIS_PROJECT.md
  DEPLOYMENT.md
  docs/screenshots/app-preview.svg
```

## Environment Variables

```env
OPENAI_API_KEY=
OPENAI_MODEL=gpt-4o-mini
USE_CREWAI_RUNTIME=false
PINECONE_API_KEY=
PINECONE_INDEX_NAME=
DATABASE_URL=sqlite:///./app.db
ALLOWED_ORIGINS=http://localhost:5173,http://localhost:3000
VITE_API_URL=http://localhost:8000
```

The app runs without an OpenAI key by using a deterministic local answer model. Add `OPENAI_API_KEY` to use LangChain with OpenAI. For CrewAI projects, set `USE_CREWAI_RUNTIME=true` after installing dependencies to run the live CrewAI Agent/Task/Crew workflow; otherwise the app uses a deterministic CrewAI-shaped fallback.

For Pinecone projects, add `PINECONE_API_KEY` and `PINECONE_INDEX_NAME` to use a live Pinecone index. Without them, the repo still runs using local ChromaDB/local retrieval fallback.

## Installation

```bash
cd backend
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

```bash
cd ../frontend
npm install
```

## Run Backend

```bash
cd backend
uvicorn app.main:app --reload --port 8000
```

## Run Frontend

```bash
cd frontend
npm run dev
```

## Run With Docker

```bash
docker compose up --build
```

## Example API Request

```bash
curl -X POST http://localhost:8000/api/ask ^
  -H "Content-Type: application/json" ^
  -d "{\"question\": \"What is the refund policy?\"}"
```

## Example User Question

```text
What should I do if a customer asks for a refund without an order id?
```

## Expected Output

The API returns:

- `answer`: a grounded answer generated from retrieved context
- `sources`: cited document chunks with similarity scores
- `steps`: planner, retriever, reasoning, tool-call, and final-answer timeline logs
- `project_type`: `Simple RAG`

## How The RAG/Agent Flow Works

User question -> load documents -> split chunks -> embed -> Chroma similarity search -> answer with citations.

## Project Planner Agent Workflow

User -> React Dashboard -> FastAPI -> Project Planner Agent -> Specialist Agents -> Generated Project -> Auto Testing -> GitHub Repository Creation -> Push Code -> Return GitHub URL

- **Architecture Agent**: Define app boundaries, data flow, runtime stack, and integration points. Outputs: This architecture emphasizes simplicity and ease of setup for beginners. FastAPI is chosen for its high performance and ease of learning Python APIs. React provides a modern, component-based UI. ChromaDB is an excellent choice for a beginner RAG project due to its straightforward API and capability to run in-memory or as a lightweight persistent store without complex external dependencies. Using a local embedding model (Sentence Transformers) avoids external API costs and dependencies for a core RAG component. The LLM can be swapped between a local Ollama setup (for full local control) or a standard API (like GPT-3.5-turbo) by configuring the backend, making it flexible for development and deployment. The focus is on a single-tenant, document-based RAG flow..
- **Backend Agent**: Design FastAPI modules, service contracts, validation, and error handling. Outputs: Document Ingestion Service: Handles file uploads, processes documents into chunks, generates embeddings, and stores them in ChromaDB.; RAG Query Service: Receives user queries, embeds them, performs vector search in ChromaDB, retrieves relevant document chunks, constructs a prompt, and sends it to the LLM for generating an answer.; Health Check Service: Provides a simple endpoint to check the backend's operational status..
- **Frontend Agent**: Design React screens, state flow, controls, and user feedback states. Outputs: File Upload Interface: Allows users to drag-and-drop or select multiple text-based documents (PDF, TXT, DOCX) for ingestion.; Search Bar: An input field for users to type natural language questions related to their uploaded customer success documents.; Response Display Area: Shows the AI-generated answer clearly, along with citations to the original source documents and specific text chunks.; Loading Indicators: Visual feedback during document processing and query response generation.; Error Handling UI: Displays user-friendly messages for file upload failures or API errors..
- **Database Agent**: Design persistence models, sample data, indexes, and audit records. Outputs: Run history; Source document metadata; Generated workflow audit records.
- **Testing Agent**: Define contract tests, smoke tests, and generated project validation. Outputs: For backend: Test individual functions like chunking, embedding generation, vector search logic, and prompt construction. For frontend: Test individual React components for rendering and basic interaction.; Test the full RAG pipeline: upload document -> query -> get response with citations. Verify correct data flow between services (FastAPI, ChromaDB, LLM integration).; Simulate user interaction (e.g., Cypress/Playwright) to ensure the UI behaves as expected when interacting with the backend and displaying results.; Basic tests to measure latency for document ingestion and query response times with a small dataset to ensure beginner-friendly performance.; Using a small, fixed set of documents and queries, assert that the RAG system returns relevant information and correct citations..
- **DevOps Agent**: Define environment variables, Docker workflow, and repository packaging. Outputs: Docker-ready project; Environment sample file; GitHub repository upload.
- **Reviewer Agent**: Review the generated plan for completeness, security, and portfolio quality. Outputs: 1. User navigates to the application's home page.; 2. User uploads customer success documents (e.g., 'customer_acme_q1_review.txt', 'customer_globex_feedback.txt') via the drag-and-drop interface.; 3. Backend receives documents, performs OCR (if PDF) and text extraction, chunks the text, generates embeddings using the local embedding model, and stores chunks and embeddings in ChromaDB.; 4. Frontend indicates 'Documents processed successfully'.; 5. User enters a natural language query into the search bar, e.g., 'What were Acme Corp's Q1 challenges?'.; 6. Frontend sends the query to the backend's RAG Query Service..

## AI-Customized Domain Workflow

- 1. User navigates to the application's home page.
- 2. User uploads customer success documents (e.g., 'customer_acme_q1_review.txt', 'customer_globex_feedback.txt') via the drag-and-drop interface.
- 3. Backend receives documents, performs OCR (if PDF) and text extraction, chunks the text, generates embeddings using the local embedding model, and stores chunks and embeddings in ChromaDB.
- 4. Frontend indicates 'Documents processed successfully'.
- 5. User enters a natural language query into the search bar, e.g., 'What were Acme Corp's Q1 challenges?'.
- 6. Frontend sends the query to the backend's RAG Query Service.
- 7. Backend embeds the user query, performs a vector search in ChromaDB to retrieve the most relevant text chunks.
- 8. Backend constructs a prompt using the retrieved chunks as context and the user's original query.

## Business Rules

- All AI-generated responses must cite the specific source document(s) and relevant text chunks they were derived from.
- If information cannot be found within the provided documents, the system must explicitly state that it does not have the answer based on the available context.
- Document ingestion should support .txt, .pdf, and .docx file types.
- Maximum file size for upload is 10MB per document (configurable).
- Retrieved chunks for RAG should be limited to the top 5 most relevant for brevity and cost/token management.
- Only text content from documents is indexed; images or other media are ignored.
- Embeddings for a document must be regenerated if the document content is updated/re-uploaded (simple re-ingestion workflow).

1. The backend loads sample documents from `backend/app/data/sample_docs`.
2. Documents are split into chunks.
3. Chunks are embedded and stored in ChromaDB when available, with a local fallback for development.
4. User questions are matched against relevant chunks.
5. Agent-specific steps run: planner, retriever, tool call, reasoning, reviewer, or graph nodes.
6. The final answer is returned with source citations and a timeline.

## Testing

```bash
cd backend
pytest
```

## Validation Gates Before GitHub Push

The SaaS validates generated projects before creating and pushing the GitHub repository:

- `pytest`
- `npm install`
- `npm run build`
- `docker compose config`
- `docker compose build`

## Portfolio Proof Files

- `WHY_THIS_PROJECT.md`: explains why this repo satisfies the selected project type.
- `ARCHITECTURE.md`: documents the runtime flow, agents/nodes, and validation strategy.
- `DEPLOYMENT.md`: gives Render, Railway, Vercel, and Docker deployment options.
- `docs/screenshots/app-preview.svg`: generated UI preview image for README/profile use.

## Deployment

See `DEPLOYMENT.md` for Render, Railway, Vercel, and Docker deployment steps.
