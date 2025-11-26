I'm building the retrieval layer for a causal analysis system that processes customer service conversations. The system already has:
- Vector database with multi-level indexed conversations (turn-level, segment-level, full conversation)
- Embeddings generated for 19,621 transcripts
- Metadata: domain, intent, reason_for_call

Challenge: When users ask queries like "Why do customers escalate on billing calls?" or "What conversational patterns lead to refunds?", I need to:
1. Retrieve the MOST RELEVANT conversation segments
2. Identify CAUSAL SPANS (specific turns that triggered the business event)
3. Rank results by relevance and causal strength

I need you to build a sophisticated retrieval strategy system:

1. **Query Understanding Module:**
   - Parse natural language queries to extract:
     * Business event type (escalation, refund, churn, complaint)
     * Domain/intent filters (if mentioned)
     * Temporal constraints (recent, last month, etc.)
     * Causal vs descriptive questions
   - Generate multiple query variations for better retrieval
   - Implement query expansion (synonyms, related terms)

2. **Multi-Stage Retrieval Pipeline:**
   - **Stage 1:** Broad retrieval (top 100-200 candidates from vector DB)
   - **Stage 2:** Reranking using cross-encoder or Cohere rerank
   - **Stage 3:** Causal relevance scoring (prioritize segments near business events)
   - **Stage 4:** Diversity filtering (avoid redundant conversations)

3. **Business Event Detection:**
   - Create heuristics to detect escalations (keywords: "manager", "supervisor", "escalate", "complaint")
   - Detect refund requests (keywords: "refund", "money back", "reimburse")
   - Detect churn signals (keywords: "cancel", "close account", "switch provider")
   - Assign confidence scores to detected events

4. **Evidence Span Extraction:**
   - For retrieved conversations, identify the specific 2-5 turn sequences that likely caused the event
   - Use contextual analysis: turns before the event signal + customer emotional cues
   - Create a "causal chain" showing conversation flow leading to the event

5. **Contextual Retrieval for Follow-ups:**
   - Implement conversation memory for multi-turn queries
   - Handle follow-up questions like "Show me more examples" or "What about in insurance domain?"
   - Maintain query context across interactions

6. **Evaluation Framework:**
   - Create test queries with ground truth relevant conversations
   - Measure: Precision@k, Recall@k, MRR (Mean Reciprocal Rank)
   - Compare with baseline (simple vector search without reranking)

Deliverables:
- query_processor.py (query understanding)
- retriever.py (multi-stage retrieval)
- event_detector.py (business event identification)
- span_extractor.py (causal span extraction)
- evaluation.py (metrics and testing)
- README_RETRIEVAL.md (strategy documentation)
- requirements.txt (rerankers, transformers, regex, etc.)

Design this as a flexible pipeline where different strategies can be A/B tested. Include extensive logging for debugging retrieval quality.
