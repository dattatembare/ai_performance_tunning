## Performance Improvement in Azure AI Search
### Chunking

Data chunking plays important role while getting accurate responses from SearchAI. Chunking the data before uploading to the index is very crucial. 

Optimized Data chunking helps to get accurate responses for one word or one liner responses. Also, it plays important role gathering detailed response for the query.

While selecting the chunk size, overlap size is important too. Find more information here about chunking and overlap.

Indexing, vectorization & Semantic Ranking
While creating an index below things need to be considered -

**1. Algorithm selection:** m, ef_construction and ef_search helps to improve the accuracy but at same time degrades the performance too. So need to select optimized values.

Index Algorithm:
```
algorithms=[
    HnswVectorSearchAlgorithmConfiguration(
        name="myHnsw",
        kind=VectorSearchAlgorithmKind.HNSW,
        parameters=HnswParameters(
            m=5,
            ef_construction=300,
            ef_search=400,
            metric=VectorSearchAlgorithmMetric.COSINE,
        ),
    ),
    ExhaustiveKnnVectorSearchAlgorithmConfiguration(
        name="myExhaustiveKnn",
        kind=VectorSearchAlgorithmKind.EXHAUSTIVE_KNN,
        parameters=ExhaustiveKnnParameters(
            metric=VectorSearchAlgorithmMetric.COSINE,
        ),
    ),
],
```


**2. Semantic Ranking -** Semantic configuration with hybrid search helps to improve the accuracy.
Semantic Configuration:
```
semantic_config = SemanticConfiguration(
    name="my-semantic-config",
    prioritized_fields=PrioritizedFields(
        title_field=SemanticField(field_name="title"),
        # keywords_fields=[SemanticField(field_name="title")],
        prioritized_content_fields=[SemanticField(field_name="content")]
    ),
)
```

**3. Search Top k** - k value decides number of documents to be returned by SearchAI. This value is important to get enough and relevant context from SearchAI.


Here are more details about Chunking, Overlap, Indexing, Vectorization and Semantic Ranking. 

[Azure AI Search: Outperforming vector search with hybrid retrieval and ranking capabilities](https://techcommunity.microsoft.com/t5/ai-azure-ai-services-blog/azure-ai-search-outperforming-vector-search-with-hybrid/ba-p/3929167)
