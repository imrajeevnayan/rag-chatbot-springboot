# Spring Boot RAG Document Q&A

This project is a production-style starter for a PDF based RAG system:

PDF upload -> text extraction -> chunking -> embeddings -> Qdrant retrieval -> OpenRouter LLM answer.

## Run Locally

1. Start Qdrant:

```powershell
docker compose up -d
```

2. Set your OpenRouter API key:

```powershell
$env:OPENROUTER_API_KEY="your-key"
```

3. Start the app:

```powershell
mvn spring-boot:run
```

4. Open API docs:

```text
http://localhost:8080/swagger-ui/index.html
```

## APIs

Upload a PDF:

```powershell
curl.exe -F "file=@C:\path\document.pdf" http://localhost:8080/upload
```

Ask a question:

```powershell
curl.exe -H "Content-Type: application/json" -d "{\"question\":\"What is this document about?\",\"topK\":5}" http://localhost:8080/ask
```

## Important Production Note

The included `HashingEmbeddingClient` is deterministic and local so the pipeline works immediately. For higher answer quality, replace it with a real embedding model behind the `EmbeddingClient` interface.
