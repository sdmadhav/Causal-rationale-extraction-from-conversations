
## [Dataset Link](https://drive.google.com/drive/folders/13b6T7CEVMli2atBU6rSz_kGtXBZrAuAK) 
## **Team Structure: 2 Teams of 3**

### **Team A: Data & Retrieval Pipeline**
**Focus:** Building the foundation for finding relevant conversations

### **Team B: Reasoning & Generation Pipeline**
**Focus:** Causal analysis and response generation

---

## **Phase 1: Days 1-3 (Foundation)**

### **Team A Tasks:**
1. **Person A1 - Data Analysis & Preprocessing**
   - Analyze both JSON files (compare `final_transcripts.json` vs `final_transcripts_domain_corrected.json`)
   - Build conversation parsing pipeline
   - Create structured data format with metadata preservation
   - Generate statistics: conversation length distribution, domain breakdown, intent categories

2. **Person A2 - Embedding & Indexing**
   - Design chunking strategy (turn-level, segment-level, conversation-level)
   - Build vector database (use Chroma/FAISS/Qdrant)
   - Create multiple indexes: full conversation, turn-by-turn, metadata-filtered
   - Implement hybrid search (semantic + keyword)

3. **Person A3 - Retrieval Strategy**
   - Develop query understanding module
   - Build retrieval pipelines with reranking
   - Create business event detection logic
   - Design evidence span extraction methods

### **Team B Tasks:**
1. **Person B1 - LLM Integration & Prompting**
   - Set up LLM infrastructure (API or local)
   - Design prompt templates for causal explanation
   - Build response generation pipeline
   - Create citation/evidence linking system

2. **Person B2 - Causal Analysis Framework**
   - Design causal reasoning patterns (temporal, behavioral, linguistic cues)
   - Build pattern detection for escalations/refunds/churn
   - Create conversation flow analysis
   - Develop multi-hop reasoning chains

3. **Person B3 - Conversation Context Manager**
   - Build conversation history tracking (Task 2)
   - Design context window management
   - Create query reformulation logic
   - Implement follow-up handling

---

## **Phase 2: Days 4-6 (Integration & Testing)**

### **Team A:**
- **A1:** Integration testing of preprocessing → retrieval
- **A2:** Optimize retrieval latency and relevance
- **A3:** Build evaluation metrics for retrieval (recall@k, MRR)

### **Team B:**
- **B1:** Integrate retrieval outputs with LLM pipeline
- **B2:** Test causal explanation quality
- **B3:** Implement multi-turn conversation flow

### **Joint Work:**
- Daily sync to ensure pipeline compatibility
- Create end-to-end test cases
- Build initial query dataset (20-30 queries)

---

## **Phase 3: Days 7-8 (Query Generation & Evaluation)**

### **Both Teams Split Differently:**

**Query Generation Squad (A1, B1, B3):**
- Use LLMs to generate 100+ diverse queries
- Categorize by: task type, difficulty, use-case
- Create both "success" and "failure" examples
- Document query simulation framework

**Evaluation Squad (A2, A3, B2):**
- Design evaluation metrics (causal explanation quality, evidence relevance, coherence)
- Build baseline comparisons (simpler RAG, direct LLM)
- Run ablation studies (with/without reranking, different chunking)
- Error analysis framework

---

## **Phase 4: Days 9-10 (Documentation & Polish)**

### **Team A:**
- Dockerization
- README documentation
- Code cleanup and commenting

### **Team B:**
- Technical report writing (LaTeX)
- Presentation preparation
- Demo video/live demo setup

---

## **Critical Early Decisions (Day 1 - Whole Team)**

Before splitting, have a 2-hour session to decide:

1. **Which JSON file to use?**
   - Compare both files - what's "domain corrected"?
   - Decision: Use the corrected one, keep original for comparison

2. **LLM Choice:**
   - Budget: OpenAI GPT-4 vs Claude vs open-source (Llama 3.1/Qwen)
   - Recommendation: Use Claude Sonnet 4 for quality, test 2-3 for ablation

3. **Architecture Pattern:**
   - Simple RAG vs Agentic RAG vs Graph-based reasoning
   - Recommendation: Start with enhanced RAG (retrieval + reranking + structured prompting)

4. **Business Events to Focus:**
   - Escalations, refunds, churn are mentioned
   - From metadata: also look at `intent` and `reason_for_call` patterns

5. **Chunking Strategy:**
   - Turn-level (each agent/customer utterance)
   - Sliding window (3-5 turns)
   - Full conversation
   - Recommendation: Multi-level indexing

---

## **Key Success Factors**

1. **Daily 30-min standups:** Each person shares progress + blockers
2. **Shared code repository:** Use Git with clear branching strategy
3. **Common data formats:** Define interfaces between pipelines early
4. **Documentation-first:** Write README sections as you build
5. **Iterative testing:** Don't wait till day 7 to test end-to-end

---

## **Suggested Tech Stack**

- **Embeddings:** OpenAI `text-embedding-3-large` or `bge-large-en-v1.5`
- **Vector DB:** ChromaDB (simple) or Qdrant (scalable)
- **LLM:** Claude Sonnet 4 (main), GPT-4o (comparison)
- **Reranker:** Cohere rerank or `ms-marco-MiniLM`
- **Framework:** LangChain or LlamaIndex (choose one)
- **Containerization:** Docker with docker-compose

---

## **Risk Mitigation**

- **Risk:** Retrieval doesn't find relevant conversations
  - **Mitigation:** A2 and A3 should test retrieval by Day 3
  
- **Risk:** LLM generates poor causal explanations
  - **Mitigation:** B1 and B2 iterate on prompts with sample data by Day 4

- **Risk:** Integration issues between teams
  - **Mitigation:** Define clear data interfaces on Day 1, test integration by Day 5

---

## **What to Build First (Day 1 Afternoon)**

1. **A1:** Load both JSON files, parse 100 conversations, print statistics
2. **A2:** Embed 100 conversations, store in vector DB, test basic retrieval
3. **A3:** Write 5 sample queries, test retrieval quality manually
4. **B1:** Set up LLM API, test basic prompt with sample conversation
5. **B2:** Manually analyze 10 conversations with escalations, note patterns
6. **B3:** Design conversation state schema for multi-turn tracking

By end of Day 1, everyone should have a working proof-of-concept for their component.
