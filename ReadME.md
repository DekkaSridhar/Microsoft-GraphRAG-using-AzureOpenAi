# GraphRAG: Context-Enriched Search using Knowledge Graphs

This project automates document ingestion, knowledge graph construction, and retrieval-augmented generation (RAG) for scientific documents such as medical research PDFs.

---

## 🔧 Setup

```bash
# Create input directory
mkdir -p ./ragtest/input

# Initialize GraphRAG workspace
python -m graphrag.index --init --root ./ragtest
```

---

## ✨ Generate Custom Prompts (Optional)

```bash
python -m graphrag.prompt_tune \
  --root ./ragtest \
  --domain "medical experiments research articles" \
  --method random \
  --limit 10 \
  --max-tokens 2048 \
  --chunk-size 256 \
  --no-entity-types \
  --output ./prompt_medical_experiments_research_articles
```

---

## 📁 Preprocessing & Indexing

1. **PDF to Text Conversion**  
   Each `.pdf` file in the `pdfs` folder is converted to `.txt`.

2. **Indexing with GraphRAG**  
   Runs `graphrag.index` for each document to generate the knowledge graph artifacts.

3. **Input-Output Mapping**  
   Maps each input `.txt` to the corresponding output knowledge graph directory.

---

## 🔍 Search Modes

### 1. **Local Search**
Uses structured knowledge (entities, relationships, reports) to answer queries using an LLM.  
Components include:
- Entity and relationship embeddings
- Community-level insights
- Context control via `context_builder_params`

### 2. **Global Search**
Performs broader search across entire corpus of community reports.  
Includes:
- Full or summarized community reports
- Optional use of entity-based ranking
- LLM map-reduce summarization

---

## 🧪 Sample Query Execution

To run a query:

```python
result = local_search(output_dir="your_output_id", prompt="your question")
# OR
result = global_search(output_dir="your_output_id", prompt="your question")
```

Both return structured responses along with the knowledge graph context used.

---

## 📊 Additional Context Mapping

- Maintains mapping of PDF to output artifacts for tracking.
- Excel sheets for region-level metadata and citation references are also loaded for additional data merging.

---

## ✅ Requirements

- Python 3.9+
- Dependencies defined within `graphrag` package
- Azure OpenAI access (API key & deployment details)

---

## 📁 Folder Structure

```
ragtest/
├── pdfs/              # Input PDFs
├── input/             # Converted text files
├── output/            # Indexed KG artifacts
└── pubmeds/           # Metadata & Mappings
```

---

## 🔐 Notes

Ensure you set correct Azure API credentials inside the script:
```python
api_key = "YOUR_KEY"
api_base = "https://YOUR_RESOURCE.openai.azure.com/"
deployment_name = "gpt-4o"
```

---
