I'm building the response generation layer for a causal analysis system over customer service conversations. The system retrieves relevant conversation segments, and now needs to generate evidence-based causal explanations.

Context:
- Retrieved conversations contain agent-customer dialogues about issues (billing, claims, cancellations)
- Business events: escalations, refunds, churn
- System must explain WHY these events happened based on conversational evidence

I need you to build a sophisticated LLM-powered generation pipeline:

1. **LLM Infrastructure Setup:**
   - Integrate with Claude API (Anthropic) - use Claude Sonnet 4 as primary
   - Add fallback to OpenAI GPT-4o for comparison
   - Implement rate limiting, retry logic, error handling
   - Add streaming support for real-time responses
   - Track token usage and costs

2. **Prompt Engineering for Causal Explanation (Task 1):**
   Create a sophisticated prompt template that:
   - Takes user query + retrieved conversation segments
   - Instructs LLM to identify causal factors (not just correlations)
   - Requires citing specific turns/utterances as evidence
   - Structures output as: Summary → Causal Factors → Supporting Evidence → Patterns
   - Handles multiple retrieved conversations (synthesize across examples)
   
   Example query: "Why are escalations happening on billing calls?"
   Expected output: "Escalations occur primarily due to: 1) Repeated unresolved issues (evidence: Customer in conversation #123 mentions 'calling for the third time')..."

3. **Citation and Evidence Linking:**
   - Ensure LLM outputs reference specific conversation IDs and turn numbers
   - Format citations clearly: [Conv: abc123, Turns 4-6]
   - Implement post-processing to validate citations exist in retrieved data
   - Create highlighted evidence snippets in the final response

4. **Response Quality Controls:**
   - Add instruction to avoid hallucination (only use provided conversations)
   - Implement consistency checking (do citations match actual content?)
   - Add confidence scoring to generated explanations
   - Detect when retrieval is insufficient and request more context

5. **Multi-Model Comparison Framework:**
   - Create pipeline to run same query through Claude, GPT-4, and optionally Llama 3.1
   - Log outputs for comparison
   - Build simple scoring for response quality (causal depth, evidence usage, clarity)

6. **Output Formatting:**
   - Generate structured JSON output with fields: summary, causal_factors (list), evidence (list of dicts), confidence_score
   - Also create human-readable markdown format
   - Support both formats simultaneously

Deliverables:
- llm_client.py (API integration with multiple providers)
- prompt_templates.py (sophisticated prompt engineering)
- response_generator.py (main generation pipeline)
- citation_validator.py (verify evidence links)
- model_comparison.py (A/B testing different LLMs)
- README_LLM.md (prompt design rationale)
- requirements.txt (anthropic, openai, tenacity, tiktoken, etc.)

Focus on prompt engineering quality - this is critical. Include examples of good vs bad prompts and iterative improvements you tested.
