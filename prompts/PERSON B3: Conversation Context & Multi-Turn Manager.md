I'm building the conversational AI layer for a causal analysis system. This system already handles single queries (Task 1), but needs to support natural follow-up conversations (Task 2).

Context:
- User asks: "Why are escalations happening on billing calls?"
- System responds with analysis
- User follows up: "Show me examples from insurance domain" or "What about refund patterns?" or "Tell me more about the third factor you mentioned"

The system must maintain context, understand references, and provide coherent multi-turn interactions.

I need you to build a conversation context management system:

1. **Conversation State Management:**
   - Design a state schema that tracks:
     * Full conversation history (user queries + system responses)
     * Retrieved conversations from previous turns (don't re-retrieve unnecessarily)
     * Current analysis context (which business event, domain filters applied)
     * User's focus (what aspect they're drilling into)
   - Implement state persistence (in-memory for now, design for future database storage)
   - Handle session management (each user gets isolated context)

2. **Query Reformulation:**
   When user asks follow-up questions with pronouns/references:
   - "Show me more examples" → reformulate to "Show more escalation examples from billing domain"
   - "What about refunds?" → reformulate based on previous domain context
   - "Tell me about the second factor" → resolve reference to previously mentioned causal factor
   
   Implement:
   - Coreference resolution (resolve "it", "that", "those")
   - Context expansion (add implicit filters from previous queries)
   - Ambiguity handling (ask clarifying questions when needed)

3. **Contextual Retrieval:**
   - For follow-ups, don't start retrieval from scratch
   - Implement incremental retrieval:
     * If asking for "more examples", retrieve next best candidates
     * If narrowing domain, filter previous results
     * If shifting focus (escalations → refunds), new retrieval with context
   - Cache previous retrievals for efficiency
   - Track what user has already seen (avoid showing same conversations twice)

4. **Conversation Flow Control:**
   Support different follow-up types:
   
   **Clarification:** "What do you mean by agent rigidity?"
   - Provide expanded explanation of previously mentioned concept
   
   **Drill-down:** "Show me conversations where customers mentioned billing errors specifically"
   - Narrow focus within current analysis
   
   **Comparison:** "How does this compare to refund patterns?"
   - Switch business event while maintaining domain context
   
   **Example Request:** "Show me the actual conversation where this happened"
   - Fetch and display full conversation transcripts
   
   **Meta Query:** "How confident are you in this analysis?"
   - Return system confidence scores and data coverage

5. **Context-Aware Response Generation:**
   - Modify prompts sent to LLM to include conversation history
   - Add instructions like "The user previously asked about X, now they're asking about Y"
   - Handle context window limits (summarize older turns if conversation gets long)
   - Maintain coherent narrative across turns (don't contradict previous responses)

6. **Conversation Memory Optimization:**
   - Implement smart context pruning (keep relevant history, discard tangents)
   - Compress older conversation turns (keep key points, discard verbose details)
   - Prioritize recent context + original query
   - Maximum context window: design for ~10 turns without degradation

7. **User Intent Classification:**
   For each follow-up query, classify intent:
   - NEW_QUERY (fresh analysis)
   - CLARIFICATION (explain previous response)
   - DRILL_DOWN (narrow focus)
   - EXPAND (broader view)
   - EXAMPLE_REQUEST (show data)
   - COMPARISON (contrast with other aspect)
   
   Route to appropriate handler based on intent.

Deliverables:
- context_manager.py (state management)
- query_reformulator.py (follow-up understanding)
- conversation_handler.py (orchestrates multi-turn flow)
- intent_classifier.py (categorize follow-up types)
- test_conversations.py (simulate multi-turn interactions)
- README_CONVERSATION.md (explains context handling design)
- requirements.txt (spacy, transformers, redis [for future], etc.)

Create a demo script that simulates a 5-turn conversation showing how context is maintained. This is critical for Task 2 evaluation.
