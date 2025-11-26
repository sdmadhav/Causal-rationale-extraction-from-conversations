I'm working on a causal analysis system for customer service conversations. I have two JSON files:
- final_transcripts.json
- final_transcripts_domain_corrected.json

Each contains 19,621 transcripts with this structure:
- transcript_id
- time_of_interaction
- domain (e.g., "Insurance")
- intent (e.g., "Discounts & Promotions")
- reason_for_call
- conversation: list of turns with speaker (Agent/Customer) and text

Sample conversation:
Customer: "Hi I'm calling about my health claim again. I've sent the documents twice already..."
Agent: "I'm really sorry you've had to go through this, sir. Let me pull up your file first..."

I need you to create a comprehensive data preprocessing pipeline in Python that:

1. **Data Loading & Comparison:**
   - Load both JSON files
   - Compare them to understand what "domain_corrected" means
   - Recommend which file to use and why
   - Handle missing/null metadata fields gracefully

2. **Data Cleaning:**
   - Clean conversational noise (ill punctuations, pauses like "(pause)", non-grammatical segments)
   - Standardize speaker labels (Agent/Customer)
   - Handle edge cases (empty turns, missing speakers)
   - Preserve metadata integrity

3. **Statistical Analysis:**
   - Generate comprehensive statistics: conversation length distribution, turns per conversation, domain breakdown, intent categories, temporal patterns
   - Identify conversations with business-critical signals (keywords like "escalate", "refund", "cancel", "frustrated", "manager")
   - Create visualizations (use matplotlib/seaborn)

4. **Structured Output:**
   - Create a unified conversation format optimized for downstream retrieval and LLM processing
   - Add computed fields: conversation_length, customer_sentiment_signals, potential_business_events
   - Export to JSON and pickle format

5. **Documentation:**
   - Write detailed docstrings
   - Create a data_analysis_report.md with findings
   - Include sample outputs

Deliverables:
- preprocess.py (main script)
- data_analyzer.py (analysis utilities)
- config.yaml (for configurable parameters)
- data_analysis_report.md
- requirements.txt (pandas, numpy, matplotlib, seaborn, tqdm, etc.)

Make it production-ready with error handling, logging, and progress bars. Structure code with clear functions that can be imported by other team members.
