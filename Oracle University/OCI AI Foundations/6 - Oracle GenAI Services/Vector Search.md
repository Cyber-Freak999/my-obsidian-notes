# **[Oracle Database 23ai](https://docs.oracle.com/en/database/oracle/oracle-database/23/vecse/index.html): AI Vector Search Overview**

Oracle Database 23ai introduces **AI Vector Search**, fully integrated into its **converged database** architecture. It enables **semantic similarity search** across **structured and unstructured data**—natively within SQL—powering enterprise-grade **Gen AI pipelines** without external vector databases.
# [What Is AI Vector Search?](https://docs.oracle.com/en/database/oracle/oracle-database/23/vecse/overview-ai-vector-search.html#VECSE-GUID-746EAA47-9ADA-4A77-82BB-64E8EF5309BE)

AI Vector Search enables searching **by meaning** (semantics), not just keywords. It's essential for:

- **Information retrieval** in Gen AI apps    
- **Similarity searches** on embeddings from text, images, etc.
- Building **RAG (Retrieval-Augmented Generation)** pipelines

Unlike purpose-built vector databases, **Oracle supports this alongside JSON, XML, text, graph, spatial, and relational data**—in a single database engine.
## **Key Features**

- **VECTOR data type**
	- New SQL-native type to store vector embeddings.    
	- Can store dimensions explicitly or use implicit typing.
	- Flexible for evolving models without changing schema.
- **VECTOR_EMBEDDING()** function 
	- for generating embeddings using models inside the database (e.g., ONNX models like `resnet_50`).
	- accepts inputs like text or images plus the model to use.
- **VECTOR_DISTANCE()** function
	- for similarity scoring between two vectors.
	- Smaller distance means more similar.
	- Supports multiple distance metrics.
- **SQL-native** syntax and indexing for seamless querying.
- **Supports structured, semi-structured, and unstructured data**: JSON, XML, Graph, Spatial, Text, Relational, and Vectors.
## **How It Works**
### Example Workflow
Match job applicants to jobs using AI Vector Search:
``` sql
SELECT job_id, job_title
FROM jobs
WHERE VECTOR_DISTANCE(jobs.embedding, candidate_embedding) < 0.25
AND city IN ('Seattle', 'Austin')
FETCH FIRST 10 ROWS ONLY;
```
## **Vector Schema Design**
- Define tables with `VECTOR` columns.    
- Vector column can be declared with or without **fixed dimension size**.
- Schema is **forward-compatible** with evolving models.

# **Vector Indexing for Performance and Accuracy**

Indexes improve performance and control **approximation vs. accuracy**.
## How to Create:

```sql
CREATE INDEX job_vector_idx ON jobs(embedding) VECTOR (ORGANIZATION INMEMORY NEIGHBOR_GRAPH DISTANCE COSINE TARGET_ACCURACY 90);
```
## Index Options:

|Option|Purpose|
|---|---|
|`ORGANIZATION`|Chooses memory layout: `INMEMORY` vs. `NEIGHBOR_PARTITIONS`|
|`DISTANCE`|Sets similarity metric (`COSINE`, etc.)|
|`TARGET_ACCURACY`|Controls recall vs. speed trade-off|
## Approximate Search:

Use `APPROXIMATE` in `FETCH` clause:

```sql
FETCH FIRST 5 ROWS ONLY APPROXIMATE;
```

- Returns **approximate top-k results**.    
- Based on `TARGET_ACCURACY` setting (e.g., 80% = 4 out of top 5 are exact).

If no index is found or suitable, the **optimizer may fall back** to exact search.
# Multi-Table Joins with Vector Search

**Major Oracle differentiator**: Perform **vector similarity joins** across normalized enterprise schemas. Oracle uniquely supports **vector search across normalized data**. Joins supported by **cost-based optimizer** using vector indexes.
## Example:

Search fiction books by Indian authors whose **pages** match a query:

```sql
SELECT b.title
FROM authors a
JOIN books b ON a.id = b.author_id
JOIN pages p ON b.id = p.book_id
WHERE a.nationality = 'India'
AND b.genre = 'Fiction'
ORDER BY VECTOR_DISTANCE(p.embedding, :queryVec)
FETCH FIRST 5 ROWS ONLY;
```

- Joins across 3 tables
- Filters + vector search in **one SQL query**
- Optimized using **cost-based optimizer**
# Integration with Gen AI Pipelines

Oracle Database 23ai can **replace external vector databases** in RAG or Gen AI pipelines.
## End-to-End Gen AI Flow
1. **Ingest data** (e.g., PDFs, CSVs, JSON, databases)
2. **Preprocess**:
    - Clean/split content
    - Generate embeddings via in-DB models (e.g., ONNX, OCI Gen AI APIs)
3. **Store** embeddings in Oracle using `VECTOR` type
4. **Query** using semantic similarity via SQL
5. **Connect to LLMs** for retrieval-augmented generation
##  Framework Integration

Seamless plug-in with:
- **LangChain**
- **LlamaIndex**
- Oracle AI Vector Search functions appear as tools/nodes in these frameworks.
Use cases:
- Custom Gen AI apps
- Intelligent assistants
- Domain-specific RAG implementations
- Hybrid search (keyword + semantic)
