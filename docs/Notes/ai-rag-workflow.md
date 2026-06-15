# Agentic RAG Workflows

## Core Components
1. **Orchestration:** Using Azure AI Services or LangChain to manage state.
2. **Retrieval:** Vectorizing data from the Lakehouse Gold layer into an Azure AI Search index.
3. **Generation:** GPT-4o model context injection for precise, grounded answers.

## Architectural Flow
```mermaid
graph LR
    A[User Query] --> B[Orchestrator]
    B --> C[Vector Database]
    C --> B
    B --> D[LLM (GPT)]
    D --> E[Final Response]