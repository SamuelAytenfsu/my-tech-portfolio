# Vector Embedding
A numerical representation of text, images, or other data in a high-dimensional space, where semantically similar items cluster close together. Used in search, recommendations, and RAG pipelines.
## Definition
Converts unstructured content into dense numeric arrays (e.g., 1536 dimensions for text-embedding-ada-002).

## Azure AI Search Setup
```python
from openai import AzureOpenAI

client = AzureOpenAI(
    api_key=os.environ["AZURE_OPENAI_KEY"],
    api_version="2024-02-01",
    azure_endpoint=os.environ["AZURE_OPENAI_ENDPOINT"]
)

def embed(text: str) -> list[float]:
    response = client.embeddings.create(
        input=text,
        model="text-embedding-ada-002"
    )
    return response.data[0].embedding
```

## When to Use
- Semantic search over Lakehouse documents
- Deduplication (cosine similarity threshold ≥ 0.95)
- RFP retrieval by intent, not keyword