# Azure AI Search
A cloud search service that supports full-text and vector (semantic) search over indexed documents. Key component of RAG pipelines — stores and retrieves vectorized chunks from knowledge bases.
## Index Schema with Vector Field
```json
{
  "name": "rfp-index",
  "fields": [
    {"name": "id", "type": "Edm.String", "key": true},
    {"name": "content", "type": "Edm.String", "searchable": true},
    {"name": "content_vector", "type": "Collection(Edm.Single)",
     "dimensions": 1536, "vectorSearchProfile": "hnsw-profile"}
  ],
  "vectorSearch": {
    "algorithms": [{"name": "hnsw-alg", "kind": "hnsw"}],
    "profiles": [{"name": "hnsw-profile", "algorithm": "hnsw-alg"}]
  }
}
```

## Hybrid Search (Vector + Keyword)
```python
results = search_client.search(
    search_text="data center cooling requirements",
    vector_queries=[VectorizedQuery(
        vector=embed("data center cooling requirements"),
        k_nearest_neighbors=5,
        fields="content_vector"
    )],
    select=["id", "content"],
    top=5
)
```