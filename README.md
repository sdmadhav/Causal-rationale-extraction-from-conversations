# Conversational Causal Analysis System

An end-to-end AI-powered system for causal analysis of customer service conversations with natural language querying and evidence-based explanations.

## Overview

This system analyzes customer service conversation transcripts to identify causal factors behind business events (escalations, refunds, churn, etc.) using a multi-stage pipeline:

1. **Hybrid Retrieval**: Combines semantic search, BM25, and metadata filtering
2. **Causal Span Extraction**: BERT-based attention mechanism identifies dialogue turns causing specific intents
3. **LLM Explanation Generation**: Llama-3-8B generates structured, evidence-grounded insights
4. **Conversational Context**: Supports follow-up queries with automatic relationship detection

## System Architecture

```
User Query → Context Manager → Hybrid Retriever → Causal Extractor → LLM Explainer → Structured Output
                    ↓                                                         ↑
            Session Management ←────────────────────────────────────────────┘
```

### Key Components

- **`classifier.py`**: BERT intent classifier training (DistilBERT-base)
- **`causal_extractor.py`**: Attention-based causal span extraction
- **`retrievar.py`**: Hybrid retrieval with caching
- **`llm_explainer_v2.py`**: Context-aware explanation generation
- **`context_manager.py`**: Conversational follow-up detection
- **`server_v2.py`**: FastAPI server with session management
- **`query_simulation.py`**: Automated testing framework

## Prerequisites

- Docker and Docker Compose
- NVIDIA GPU with CUDA 11.8+ (recommended, CPU fallback available)
- Hugging Face API token (for Llama-3-8B access)
- 16GB+ RAM recommended

## Quick Start

### 1. Environment Setup

```bash
# Clone/extract the submission
cd causal-analysis-system

# Create .env file with your HF token
echo "HF_TOKEN=your_huggingface_token_here" > .env
```

### 2. Data Preparation

Place your conversation dataset at:
```
data/transcripts/final_transcripts_domain_corrected.json
```

**Expected format:**
```json
[
  {
    "transcript_id": "unique_id",
    "domain": "Hotel",
    "intent": "Competitor Comparison",
    "conversation": [
      {"speaker": "Agent", "text": "..."},
      {"speaker": "Customer", "text": "..."}
    ]
  }
]
```

### 3. Model Training (Optional - Pre-trained Available)

If training from scratch:

```bash
docker-compose run --rm app python classifier.py
```

This trains the intent classifier and saves:
- `best_model.pt` - Model checkpoint
- `label_mappings.json` - Intent labels
- `training_results.json` - Training metrics

**Training time**: ~2-3 hours on GPU (GTX 1080 or better)

### 4. Build and Run

```bash
# Build Docker image
docker-compose build

# Start the server
docker-compose up
```

The system will:
1. Load the conversation dataset (19,621 transcripts)
2. Build/load cached embeddings
3. Initialize models (DistilBERT + Llama-3-8B)
4. Start server on http://localhost:8000

**Startup time**: ~5-10 minutes (first run with embedding generation)

### 5. Access the System

Open browser: http://localhost:8000

Or use API directly:

```bash
curl -X POST http://localhost:8000/api/analyze \
  -H "Content-Type: application/json" \
  -d '{"query": "Why are customers mentioning competitors?"}'
```

## API Documentation

### Create Session
```bash
POST /api/session/create
Response: {"session_id": "uuid", "created_at": "timestamp"}
```

### Analyze Query
```bash
POST /api/analyze
Body: {
  "query": "Why do customers escalate calls?",
  "session_id": "optional_uuid",
  "domain_filter": "Hotel",  # optional
  "intent_filter": "Complaint"  # optional
}

Response: {
  "session_id": "uuid",
  "explanation": {
    "summary": "...",
    "causal_factors": [...],
    "recommendations": [...],
    "overall_confidence": "high"
  },
  "is_followup": false,
  "relationship_info": {...}
}
```

### Get Session History
```bash
GET /api/session/{session_id}
```

### System Statistics
```bash
GET /api/stats
```

## Automated Testing

Run the simulation framework to test with curated queries:

```bash
# Process all queries from CSV
docker-compose run --rm app python query_simulation.py \
  --csv data/queries.csv \
  --server http://localhost:8000

# Or limit to first 10 queries
docker-compose run --rm app python query_simulation.py \
  --csv data/queries.csv \
  --limit 10
```

**Output location**: `simulation_outputs/`

Generated files:
- `full_results_TIMESTAMP.json` - Complete results
- `summary_TIMESTAMP.csv` - Performance metrics
- `detailed_TIMESTAMP/` - Per-query outputs
- `simulation_report_TIMESTAMP.md` - Comprehensive report

### Sample Query Results

From testing on 19,621 conversations:

**Simple Query**: "Why are customers mentioning competitors?"
- Retrieved: 1000 candidates
- Analyzed: 50 with causal spans
- Response time: ~12s
- Causal factors: 5 distinct patterns identified

**Complex Query**: "What causes escalations after competitor mentions in hotel domain?"
- Retrieved: 847 candidates (domain filtered)
- Analyzed: 50 with causal spans
- Response time: ~18s
- Causal factors: 3 high-confidence patterns

## System Configuration

### Key Parameters (in code)

**Retrieval** (`retrievar.py`):
```python
RetrievalConfig(
    top_k=1000,              # Candidates to retrieve
    semantic_weight=0.5,     # Embedding similarity weight
    bm25_weight=0.3,         # Keyword matching weight
    metadata_weight=0.2      # Domain/intent matching weight
)
```

**Causal Extraction** (`causal_extractor.py`):
```python
top_k=3                      # Causal spans per conversation
layer_index=-1               # BERT layer for attention (-1 = last)
```

**LLM Generation** (`llm_explainer_v2.py`):
```python
LLMConfig(
    model_name="meta-llama/Meta-Llama-3-8B",
    temperature=0.1,         # Low for factual responses
    max_tokens=2048
)
```

### Cache Management

Embeddings are cached for faster restarts:

```bash
# Clear cache
docker-compose run --rm app python -c "from pathlib import Path; [f.unlink() for f in Path('cache').glob('*.pkl')]"

# Force rebuild
docker-compose run --rm app python -c "from retrievar import HybridRetriever; r = HybridRetriever(); r.load_conversations('data/transcripts/final_transcripts_domain_corrected.json', force_rebuild=True)"
```

## Performance Metrics

**From simulation testing** (based on provided output):

| Metric | Value |
|--------|-------|
| Total Conversations | 19,621 |
| Success Rate | 100% (all queries processed) |
| Avg Response Time | ~15s |
| Avg Retrieved Docs | 900-1000 |
| Avg Causal Factors | 3-5 per query |
| Cache Hit Benefit | ~10x faster startup |

**Resource Usage**:
- Memory: ~8-12GB (with GPU)
- GPU VRAM: ~4-6GB
- Disk: ~2GB (models + embeddings)

## Troubleshooting

### Server won't start

**Check GPU availability**:
```bash
docker-compose run --rm app python -c "import torch; print(torch.cuda.is_available())"
```

If False, system will use CPU (slower but functional).

**Check HF token**:
```bash
docker-compose run --rm app python -c "import os; print('HF_TOKEN' in os.environ)"
```

### Slow responses

1. **First query is slow**: Normal - loads models into memory
2. **All queries slow**: Check if using CPU instead of GPU
3. **Out of memory**: Reduce `batch_size` in `classifier.py` or use smaller model

### Cache issues

```bash
# Verify cache exists
ls -lh cache/

# Regenerate if corrupted
rm cache/*.pkl
docker-compose restart
```

## File Structure

```
.
├── classifier.py              # Intent classifier training
├── causal_extractor.py        # Causal span extraction
├── retrievar.py               # Hybrid retrieval
├── llm_explainer_v2.py        # LLM explanation generation
├── context_manager.py         # Conversational context
├── server_v2.py               # FastAPI server
├── query_simulation.py        # Testing framework
├── Dockerfile                 # Container definition
├── docker-compose.yml         # Service orchestration
├── requirements.txt           # Python dependencies
├── .env                       # Environment variables (create this)
├── data/
│   └── transcripts/
│       └── final_transcripts_domain_corrected.json
├── cache/                     # Auto-generated embeddings cache
├── static/                    # Web interface (if applicable)
├── simulation_outputs/        # Test results
└── README.md                  # This file
```

## Key Features

### 1. Evidence-Based Explanations
Every causal factor includes:
- Transcript ID reference
- Specific dialogue spans
- Causal confidence score
- Evidence grounding

### 2. Multi-Domain Support
Handles conversations across:
- Hotel bookings
- Flight reservations
- Banking services
- Insurance claims
- Retail support
- Telecom services

### 3. Conversational Follow-up
Automatically detects follow-up queries:
```
Query 1: "Why do customers mention competitors?"
Query 2: "How many escalations happened after those mentions?"
         ↑ System recognizes relationship and reuses relevant transcripts
```

### 4. Hybrid Retrieval
Combines three retrieval strategies:
- **Semantic**: Dense embeddings (all-MiniLM-L6-v2)
- **Lexical**: BM25 keyword matching
- **Metadata**: Domain/intent filtering

### 5. Attention-Based Causality
Uses BERT attention weights to identify which conversation turns causally influenced the predicted intent.

## Model Details

### Intent Classifier
- **Base**: DistilBERT-base-uncased
- **Task**: Multi-class classification (23 intent classes)
- **Training**: 80/10/10 split, 3 epochs
- **Accuracy**: ~85% on test set
- **Input**: Full conversation text (max 256 tokens)

### Causal Extractor
- Uses trained classifier's attention weights
- Aggregates token-level attention to turn-level scores
- Identifies top-k most influential dialogue turns
- Output: Causal spans with confidence scores

### LLM Explainer
- **Model**: Llama-3-8B-Instruct
- **Task**: Generate structured explanations from evidence
- **Output**: JSON with summary, causal factors, recommendations
- **Context window**: Includes previous query artifacts for follow-ups

## Citations and References

This implementation uses:
- Hugging Face Transformers (Wolf et al., 2020)
- Sentence-Transformers (Reimers & Gurevych, 2019)
- BM25 (Robertson & Zaragoza, 2009)
- FastAPI (Ramírez, 2018)

## Known Limitations

1. **Language**: English only
2. **Context window**: Limited to last 2 conversation turns for follow-ups
3. **Real-time**: Not optimized for <1s response times
4. **Scalability**: Single-node deployment (not distributed)
5. **GPU requirement**: Strongly recommended for acceptable performance

## License and Usage

This system is provided for evaluation purposes as part of the Inter IIT Tech Meet competition submission. Not for production deployment without further hardening and optimization.

---

**Submission Date**: December 5, 2024  
**System Version**: 2.0.0  
**Tested On**: Ubuntu 20.04, Docker 24.0.7, CUDA 11.8
