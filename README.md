# 🔬 Systematic Review Pipeline

**AI-powered automation for literature search, deduplication, and abstract screening.**

A complete Jupyter notebook workflow that streamlines systematic review processes using artificial intelligence, from PubMed query generation to abstract screening.

---

## ✨ Features

- **🧠 AI Query Generation**: Automatically generates optimized PubMed search queries from protocol documents
- **🔍 PubMed Integration**: Fetches and caches study details with intelligent rate limiting
- **🧹 Smart Deduplication**: Cross-database duplicate detection using PMID, DOI, and normalized titles
- **🎯 AI-Powered Screening**: Automated abstract screening against inclusion/exclusion criteria
- **📊 Organized Export**: Session-based results with separate cache and export directories
- **💾 Intelligent Caching**: Avoids redundant API calls for queries, criteria, and search results

---

## 🚀 Quick Start

### Prerequisites

1. **Python environment** with Jupyter
2. **OpenRouter API key** (for AI features)
3. **Required libraries**: Install with `pip install pandas numpy requests openpyxl python-docx openai`

### Setup

1. **Set API key** in your terminal:
   ```bash
   export OPENROUTER_API_KEY='your-api-key-here'
   ```

2. **Prepare your protocol**: Place `protocol.docx` in the working directory (for AI mode)

3. **Optional**: Add existing databases to `old_database/` folder for deduplication

### Execution

1. Open `systematic_review_pipeline.ipynb`
2. Run all cells sequentially from top to bottom
3. Results will be saved in `export_results/session_TIMESTAMP/`

---

## 📁 Directory Structure

```
working_directory/
├── systematic_review_pipeline.ipynb    # Main notebook
├── protocol.docx                       # Your review protocol (AI mode)
├── old_database/                       # Existing study databases (optional)
│   └── *.xlsx, *.csv                  # Previous searches for deduplication
├── cache/                             # Temporary session data
│   └── session_TIMESTAMP/
│       ├── generated_query.txt        # Cached AI-generated query
│       ├── screening_criteria.json    # Cached criteria
│       └── pubmed_search_*.json      # Cached PubMed results
└── export_results/                    # Final outputs
    └── session_TIMESTAMP/
        ├── search_query.txt           # PubMed query used
        ├── screening_criteria.json    # Screening criteria
        ├── deduplicated_studies.xlsx  # Unique studies after deduplication
        └── screening_results.xlsx     # Final screening decisions
```

---

## 🔧 Configuration

### AI Models (Cell 6)

```python
LLM_CONFIG = {
    'model': 'google/gemini-2.5-flash',           # Standard screening
    'query_model': 'google/gemini-2.5-pro',       # Protocol analysis
    'temperature': 0.1,
    'max_tokens': 10000
}
```

### PubMed Settings (Cell 14)

```python
CACHE_CONFIG = {
    'max_results': 1000,           # Maximum studies to fetch
    'cache_duration_hours': 24,    # Cache validity
    'user_email': 'your@email.com' # Required by PubMed
}
```

### Manual Query Mode (Cell 8)

To skip AI generation and use your own PubMed query:

```python
USER_DEFINED_QUERY = '("your query"[tiab] AND "terms"[MeSH Terms])'
```

---

## 📊 Workflow Steps

1. **Import & Setup** (Cells 1-4): Libraries, session directories, API configuration
2. **Query Generation** (Cells 5-13): AI-generated or manual PubMed query
3. **Literature Search** (Cells 14-19): Fetch studies from PubMed with caching
4. **Deduplication** (Cells 20-23): Remove duplicates against existing databases
5. **Criteria Extraction** (Cells 24-27): AI extracts screening criteria from protocol
6. **Abstract Screening** (Cells 28-31): AI evaluates studies against criteria
7. **Export Results** (Cells 32-33): Save all outputs to organized session folder

---

## 💡 Tips & Best Practices

- **Session Management**: Each run creates a new session with unique timestamp
- **Cache Reuse**: Re-running cells within same session reuses cached data (faster, cheaper)
- **Deduplication**: Add previous search results to `old_database/` to avoid re-screening
- **API Costs**: Query generation uses advanced model; screening uses standard model
- **Rate Limiting**: Built-in delays respect PubMed API guidelines

---

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| `OPENROUTER_API_KEY not found` | Export API key in terminal before starting Jupyter |
| `No studies found` | Check PubMed query syntax and max_results limit |
| `Protocol not found` | Place `protocol.docx` in notebook directory |
| `Module not found` | Install missing libraries: `pip install [library]` |
| `Cache not loading` | Delete old cache folders or check file permissions |

---

## 📝 Citation

If you use this pipeline in your research, please cite:

```bibtex
@software{systematic_review_pipeline_2024,
  author = {Pieri, J.},
  title = {Systematic Review Pipeline: AI-Powered Literature Search and Screening},
  year = {2025},
  url = {https://github.com/jhyrachy/systematic-review-pipeline},
  note = {Jupyter notebook for automated systematic reviews}
}
```

**Plain text citation:**
> Pieri, J. (2025). Systematic Review Pipeline: AI-Powered Literature Search and Screening. 
> Available at: [GitHub URL or DOI]

---

## 📄 License

This software is provided as-is for academic and research purposes. Please retain attribution when sharing or modifying.

---

## 🙏 Acknowledgments

- **OpenRouter** for AI model access
- **NCBI E-utilities** for PubMed API

---

## 📧 Contact

**Author**: Dr. Pieri Jacopo
**GitHub**: [your-github-profile]

For bug reports, feature requests, or collaboration inquiries, please open an issue on GitHub or contact directly.

---

**Version**: 1.0.0  
**Last Updated**: October 2025 
**Status**: Feature complete
