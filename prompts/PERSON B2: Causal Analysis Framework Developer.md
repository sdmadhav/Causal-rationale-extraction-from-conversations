I'm building a causal reasoning system for customer service conversation analysis. The goal is to identify WHY business events (escalations, refunds, churn) occur based on conversational patterns.

Context:
- 19,621 customer service transcripts (agent-customer dialogues)
- Business events are implicit (not labeled) - must be inferred
- Conversations have temporal structure (turns happen in sequence)
- Need to find CAUSAL patterns, not just correlations

Challenge: When a customer escalates to a supervisor, it's not random. There's usually a causal chain: repeated issue → agent unable to resolve → customer frustration → escalation request.

I need you to build a causal analysis framework:

1. **Causal Pattern Detection:**
   Design and implement detection for:
   
   **Temporal Patterns:**
   - Repeated issues (customer mentions same problem multiple times)
   - Long wait times or holds (agent: "let me check..." repeated)
   - Back-and-forth without resolution (conversation loops)
   
   **Behavioral Patterns:**
   - Agent deflection (avoiding direct answers, passing responsibility)
   - Agent rigidity (repeatedly saying "that's our policy")
   - Lack of empathy (no acknowledgment of customer frustration)
   
   **Linguistic Cues:**
   - Customer frustration signals (sentiment deterioration across turns)
   - Escalation language ("I want to speak to your manager")
   - Threat indicators ("I'll cancel", "I'll report this")
   
   **Resolution Failure:**
   - No clear action items provided
   - Unmet expectations (promises not fulfilled)
   - Information mismatches (agent gives conflicting info)

2. **Conversation Flow Analysis:**
   - Build a turn-by-turn analyzer that tracks conversation state
   - Identify critical moments (turning points where tone shifts)
   - Detect escalation triggers (the specific turn where situation deteriorates)
   - Create a "causal graph" showing how conversation evolved to the event

3. **Multi-Hop Reasoning:**
   Some causal chains are indirect:
   - Agent gives incorrect info (Turn 3) → Customer acts on it (not in conversation) → Customer calls back frustrated (Turn 15) → Escalation
   - Implement logic to connect non-obvious causal links
   - Use conversation metadata (reason_for_call: "Calling again about...") as signals

4. **Pattern Aggregation Across Corpus:**
   - When analyzing "Why escalations happen?", aggregate patterns from multiple conversations
   - Identify most common causal factors (frequency analysis)
   - Cluster similar causal chains (e.g., "billing dispute + policy rigidity" cluster)
   - Generate statistics: "67% of escalations involved repeated issues"

5. **Causal Strength Scoring:**
   - Not all patterns are equally causal
   - Score each detected pattern by strength (0-1 scale)
   - Factors: temporal proximity to event, linguistic intensity, behavioral severity
   - Combine scores to rank causal factors

6. **Integration with LLM:**
   - Create structured output (JSON) that LLMs can consume
   - Format: {"conversation_id": "...", "detected_patterns": [...], "causal_chain": [...], "critical_turns": [...]}
   - This becomes part of the context sent to LLM for explanation generation

Deliverables:
- pattern_detector.py (implements all pattern detection logic)
- conversation_analyzer.py (turn-by-turn flow analysis)
- causal_scorer.py (scoring and ranking)
- pattern_aggregator.py (corpus-level analysis)
- test_causal_analysis.py (unit tests on sample conversations)
- README_CAUSAL.md (explains reasoning approach)
- requirements.txt (nltk, spacy, textblob, scikit-learn, etc.)

This is the "intelligence" layer. Make it explainable - analysts should be able to see WHY the system identified certain patterns as causal. Include visualization of causal chains.
