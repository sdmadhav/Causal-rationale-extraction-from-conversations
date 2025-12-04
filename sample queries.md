# Sample Queries Dataset for Your System

Based on your conversation data, here are realistic queries users would ask your causal analysis system:

## **Format**

Each query shows what a business analyst would actually type into your system.

---

## **Category 1: Single Intent Analysis (Basic)**

```json
[
  {
    "query_id": "Q001",
    "query": "Why are customers mentioning competitors in hotel calls?",
    "expected_intent": "Cross-Brand Mentions (Hotel)",
    "complexity": "simple"
  },
  {
    "query_id": "Q002",
    "query": "What causes flight delay complaints?",
    "expected_intent": "Delay Management (Flight)",
    "complexity": "simple"
  },
  {
    "query_id": "Q003",
    "query": "Why do customers ask for refunds in retail?",
    "expected_intent": "Product Returns (Retail)",
    "complexity": "simple"
  },
  {
    "query_id": "Q004",
    "query": "What makes banking customers complain about fees?",
    "expected_intent": "Fee Complaints (Banking)",
    "complexity": "simple"
  },
  {
    "query_id": "Q005",
    "query": "Why don't customers trust insurance agents?",
    "expected_intent": "Customer Trust (Insurance)",
    "complexity": "simple"
  }
]
```

---

## **Category 2: Comparative Queries (Medium)**

```json
[
  {
    "query_id": "Q006",
    "query": "What's the difference between service complaints in hotels vs telecom?",
    "expected_intents": ["Service Complaints (Hotel)", "Connectivity Complaints (Telecom)"],
    "complexity": "medium"
  },
  {
    "query_id": "Q007",
    "query": "How do price sensitivity patterns differ between flights and retail?",
    "expected_intents": ["Price Sensitivity (Flight)", "Product Feedback (Retail)"],
    "complexity": "medium"
  },
  {
    "query_id": "Q008",
    "query": "Compare fraud alerts in banking with claims issues in insurance",
    "expected_intents": ["Fraud Alerts (Banking)", "Claims & Refunds (Insurance)"],
    "complexity": "medium"
  },
  {
    "query_id": "Q009",
    "query": "Are upgrade requests handled differently in hotels vs telecom plan upgrades?",
    "expected_intents": ["Upgrade Requests (Hotel)", "Plan Upgrades (Telecom)"],
    "complexity": "medium"
  }
]
```

---

## **Category 3: Temporal/Trend Queries (Medium)**

```json
[
  {
    "query_id": "Q010",
    "query": "When during conversations do customers start mentioning competitors?",
    "expected_intent": "Cross-Brand Mentions",
    "analysis_type": "temporal",
    "complexity": "medium"
  },
  {
    "query_id": "Q011",
    "query": "At what point in the call do customers get stressed about flight delays?",
    "expected_intent": "Urgency & Stress (Flight)",
    "analysis_type": "temporal",
    "complexity": "medium"
  },
  {
    "query_id": "Q012",
    "query": "How early in calls can we predict churn risk in telecom?",
    "expected_intent": "Churn Prediction (Telecom)",
    "analysis_type": "temporal",
    "complexity": "medium"
  }
]
```

---

## **Category 4: Root Cause Queries (Complex)**

```json
[
  {
    "query_id": "Q013",
    "query": "What are the top 3 reasons customers cancel hotel bookings?",
    "expected_intent": "Cancellation Policies (Hotel)",
    "requires": ["causal_ranking", "evidence_spans", "prevalence_stats"],
    "complexity": "complex"
  },
  {
    "query_id": "Q014",
    "query": "Why do loan applications fail in banking conversations?",
    "expected_intent": "Loan Application (Banking)",
    "requires": ["causal_factors", "failure_patterns"],
    "complexity": "complex"
  },
  {
    "query_id": "Q015",
    "query": "What causes customers to lose trust during insurance sales calls?",
    "expected_intent": "Customer Trust (Insurance)",
    "requires": ["trust_breakdown_moments", "agent_behavior_patterns"],
    "complexity": "complex"
  },
  {
    "query_id": "Q016",
    "query": "What makes retail customers choose replacement over refund?",
    "expected_intent": "Replacement vs Refund (Retail)",
    "requires": ["decision_factors", "conversation_patterns"],
    "complexity": "complex"
  }
]
```

---

## **Category 5: Actionable Insight Queries (Complex)**

```json
[
  {
    "query_id": "Q017",
    "query": "How can agents prevent escalations in telecom technical support calls?",
    "expected_intent": "Technical Support (Telecom)",
    "requires": ["intervention_points", "recommendations", "impact_estimates"],
    "complexity": "complex"
  },
  {
    "query_id": "Q018",
    "query": "What should hotel agents say when customers mention competitor pricing?",
    "expected_intent": "Cross-Brand Mentions (Hotel)",
    "requires": ["agent_responses", "successful_patterns", "timing"],
    "complexity": "complex"
  },
  {
    "query_id": "Q019",
    "query": "When should flight agents offer compensation to stressed customers?",
    "expected_intent": "Urgency & Stress (Flight)",
    "requires": ["optimal_timing", "stress_indicators", "success_rates"],
    "complexity": "complex"
  },
  {
    "query_id": "Q020",
    "query": "How can we improve sales effectiveness in insurance calls?",
    "expected_intent": "Sales Effectiveness (Insurance)",
    "requires": ["success_patterns", "failed_patterns", "recommendations"],
    "complexity": "complex"
  }
]
```

---

## **Category 6: Multi-Turn Conversational Queries (Very Complex)**

```json
[
  {
    "query_id": "Q021",
    "conversation": [
      {
        "turn": 1,
        "user": "Why are customers churning in telecom?"
      },
      {
        "turn": 2,
        "system": "[Returns analysis of churn patterns]"
      },
      {
        "turn": 3,
        "user": "Show me examples where network outages were mentioned"
      },
      {
        "turn": 4,
        "system": "[Returns specific transcript spans]"
      },
      {
        "turn": 5,
        "user": "What did agents say in response?"
      }
    ],
    "complexity": "very_complex",
    "requires": ["context_tracking", "span_retrieval", "follow_up_handling"]
  },
  {
    "query_id": "Q022",
    "conversation": [
      {
        "turn": 1,
        "user": "Compare hotel service complaints to retail product feedback"
      },
      {
        "turn": 2,
        "system": "[Returns comparison]"
      },
      {
        "turn": 3,
        "user": "Which one has more competitor mentions?"
      },
      {
        "turn": 4,
        "system": "[Returns cross-brand statistics]"
      },
      {
        "turn": 5,
        "user": "Show me a retail example from last month"
      }
    ],
    "complexity": "very_complex"
  }
]
```

---

## **Category 7: Pattern Discovery Queries (Expert)**

```json
[
  {
    "query_id": "Q023",
    "query": "What hidden patterns predict customer dissatisfaction across all domains?",
    "scope": "all_domains",
    "requires": ["cross_domain_analysis", "pattern_mining", "predictive_signals"],
    "complexity": "expert"
  },
  {
    "query_id": "Q024",
    "query": "Which agent behaviors lead to successful upselling in insurance?",
    "expected_intent": "Upselling Strategy (Insurance)",
    "requires": ["behavior_analysis", "success_correlation", "causal_effects"],
    "complexity": "expert"
  },
  {
    "query_id": "Q025",
    "query": "Find conversation sequences that always lead to booking errors in hotels",
    "expected_intent": "Booking Errors (Hotel)",
    "requires": ["sequence_mining", "deterministic_patterns", "error_chains"],
    "complexity": "expert"
  }
]
```

---

## **Category 8: Business Impact Queries (Strategic)**

```json
[
  {
    "query_id": "Q026",
    "query": "If we reduce wait times in banking, how much would fee complaints decrease?",
    "expected_intent": "Fee Complaints (Banking)",
    "requires": ["causal_effect_estimation", "counterfactual_analysis", "impact_quantification"],
    "complexity": "strategic"
  },
  {
    "query_id": "Q027",
    "query": "What's the ROI of training agents on competitor objection handling in flights?",
    "expected_intent": "Cross-Brand Mentions (Flight)",
    "requires": ["intervention_impact", "cost_benefit", "prevalence_data"],
    "complexity": "strategic"
  },
  {
    "query_id": "Q028",
    "query": "Which customer segments are most likely to switch to competitors in telecom?",
    "expected_intent": "Churn Prediction (Telecom)",
    "requires": ["segmentation", "churn_risk_scoring", "competitor_analysis"],
    "complexity": "strategic"
  }
]
```

---

## **Category 9: Domain-Specific Deep Dives**

```json
[
  {
    "query_id": "Q029",
    "query": "In hotel calls, what's the relationship between upgrade requests and loyalty program mentions?",
    "expected_intents": ["Upgrade Requests (Hotel)", "Brand Loyalty (Hotel)"],
    "analysis_type": "correlation_and_causation",
    "complexity": "complex"
  },
  {
    "query_id": "Q030",
    "query": "Do customers who mention refund policies early in flight calls end up canceling?",
    "expected_intent": "Refund Policy (Flight)",
    "analysis_type": "predictive",
    "complexity": "complex"
  },
  {
    "query_id": "Q031",
    "query": "How do hesitation patterns differ between successful vs failed loan applications?",
    "expected_intent": "Loan Application (Banking)",
    "requires": ["linguistic_analysis", "outcome_comparison"],
    "complexity": "complex"
  }
]
```

---

## **Category 10: Real-World User Queries (Natural Language)**

```json
[
  {
    "query_id": "Q032",
    "query": "Why are customers so angry about delivery delays?",
    "expected_intent": "Delivery Delays (Retail)",
    "note": "Natural, emotional query",
    "complexity": "simple"
  },
  {
    "query_id": "Q033",
    "query": "Our hotel agents keep losing bookings to Hilton - what's going wrong?",
    "expected_intent": "Cross-Brand Mentions (Hotel)",
    "note": "Business problem framing",
    "complexity": "complex"
  },
  {
    "query_id": "Q034",
    "query": "Can you find conversations where the agent did everything right?",
    "scope": "positive_examples",
    "note": "Success pattern query",
    "complexity": "medium"
  },
  {
    "query_id": "Q035",
    "query": "Show me the worst service complaint call from last week",
    "expected_intent": "Service Complaints",
    "note": "Extreme case query",
    "complexity": "simple"
  }
]
```

---

## **Full Dataset Structure**

```json
{
  "query_dataset": {
    "version": "1.0",
    "total_queries": 35,
    "categories": {
      "single_intent": 5,
      "comparative": 4,
      "temporal": 3,
      "root_cause": 4,
      "actionable": 4,
      "multi_turn": 2,
      "pattern_discovery": 3,
      "business_impact": 3,
      "domain_specific": 3,
      "natural_language": 4
    },
    "complexity_distribution": {
      "simple": 7,
      "medium": 9,
      "complex": 12,
      "very_complex": 2,
      "expert": 3,
      "strategic": 3
    }
  }
}
```

---

## **Expected System Responses (Examples)**

### **For Q001: "Why are customers mentioning competitors in hotel calls?"**

```json
{
  "summary": "Competitor mentions in hotel calls occur primarily when customers are price-shopping and comparing value propositions.",
  "causal_factors": [
    {
      "factor": "Customer discusses pricing before agent offers best discount",
      "evidence_spans": [
        {"transcript_id": "ce44aa4b...", "turns": [8, 9], "causal_score": 0.87}
      ],
      "prevalence": "67% of competitor mentions",
      "effect_size": "+43% probability of competitor mention",
      "recommendation": "Train agents to proactively offer best rates in turns 3-5"
    },
    {
      "factor": "Agent doesn't acknowledge competitor offers directly",
      "evidence_spans": [
        {"transcript_id": "ce44aa4b...", "turns": [10, 11], "causal_score": 0.72}
      ],
      "prevalence": "54% of competitor mentions",
      "effect_size": "+31% probability",
      "recommendation": "Validate customer research, then differentiate on value"
    }
  ],
  "impact_estimate": "Addressing top 2 factors could reduce competitor mentions by 38%"
}
```

---

## **For Competition Evaluation**

## Category 1: Single Intent Analysis (Basic)
```json
[
  {
    "query_id": "Q036",
    "query": "Which calls show customers confused about insurance features?",
    "expected_intent": "Feature Understanding (Insurance)",
    "complexity": "simple"
  },
  {
    "query_id": "Q037",
    "query": "What triggers technical support calls in telecom?",
    "expected_intent": "Technical Support (Telecom)",
    "complexity": "simple"
  },
  {
    "query_id": "Q038",
    "query": "Why do customers request hotel room upgrades?",
    "expected_intent": "Upgrade Requests (Hotel)",
    "complexity": "simple"
  },
  {
    "query_id": "Q039",
    "query": "Which conversations indicate credit limit requests in banking?",
    "expected_intent": "Credit Limit Requests (Banking)",
    "complexity": "simple"
  },
  {
    "query_id": "Q040",
    "query": "What causes product replacement requests in retail?",
    "expected_intent": "Replacement vs Refund (Retail)",
    "complexity": "simple"
  }
]

Category 2: Comparative Queries (Medium)
[
  {
    "query_id": "Q041",
    "query": "Compare refund request patterns between flights and retail",
    "expected_intents": ["Refund Policy (Flight)", "Product Returns (Retail)"],
    "complexity": "medium"
  },
  {
    "query_id": "Q042",
    "query": "Which domain shows more loyalty program mentions: retail or flights?",
    "expected_intents": ["Loyalty Program (Retail)", "Loyalty Program (Flight)"],
    "complexity": "medium"
  },
  {
    "query_id": "Q043",
    "query": "How do cancellation complaints differ between hotels and flights?",
    "expected_intents": ["Cancellation Policies (Hotel)", "Refund Policy (Flight)"],
    "complexity": "medium"
  },
  {
    "query_id": "Q044",
    "query": "Compare connectivity complaints vs feature requests in telecom",
    "expected_intents": ["Connectivity Complaints (Telecom)", "Feature Requests (Telecom)"],
    "complexity": "medium"
  }
]

Category 3: Temporal/Trend Queries (Medium)
[
  {
    "query_id": "Q045",
    "query": "During which turn do banking customers start complaining about fees?",
    "expected_intent": "Fee Complaints (Banking)",
    "analysis_type": "temporal",
    "complexity": "medium"
  },
  {
    "query_id": "Q046",
    "query": "At what point do flight customers ask about price differences?",
    "expected_intent": "Price Sensitivity (Flight)",
    "analysis_type": "temporal",
    "complexity": "medium"
  },
  {
    "query_id": "Q047",
    "query": "When do retail customers typically request replacements in a call?",
    "expected_intent": "Replacement vs Refund (Retail)",
    "analysis_type": "temporal",
    "complexity": "medium"
  }
]

Category 4: Root Cause Queries (Complex)
[
  {
    "query_id": "Q048",
    "query": "What causes network outages to generate repeated telecom calls?",
    "expected_intent": "Network Outages (Telecom)",
    "requires": ["causal_factors", "repeat_call_patterns"],
    "complexity": "complex"
  },
  {
    "query_id": "Q049",
    "query": "Why do insurance policy renewals fail?",
    "expected_intent": "Policy Renewal (Insurance)",
    "requires": ["causal_factors", "customer_behavior_patterns"],
    "complexity": "complex"
  },
  {
    "query_id": "Q050",
    "query": "What triggers complaints about hotel service quality?",
    "expected_intent": "Service Complaints (Hotel)",
    "requires": ["root_cause_analysis", "conversation_patterns"],
    "complexity": "complex"
  },
  {
    "query_id": "Q051",
    "query": "Why are flight refunds delayed according to customer conversations?",
    "expected_intent": "Refund Policy (Flight)",
    "requires": ["causal_factors", "process_analysis"],
    "complexity": "complex"
  }
]

Category 5: Actionable Insight Queries (Complex)
[
  {
    "query_id": "Q052",
    "query": "How can agents reduce refund disputes in retail calls?",
    "expected_intent": "Product Returns (Retail)",
    "requires": ["intervention_points", "recommendations", "impact_estimates"],
    "complexity": "complex"
  },
  {
    "query_id": "Q053",
    "query": "Which actions improve customer trust in insurance calls?",
    "expected_intent": "Customer Trust (Insurance)",
    "requires": ["agent_behavior_patterns", "success_metrics"],
    "complexity": "complex"
  },
  {
    "query_id": "Q054",
    "query": "How can flight agents reduce customer stress during delays?",
    "expected_intent": "Urgency & Stress (Flight)",
    "requires": ["stress_indicators", "successful_interventions"],
    "complexity": "complex"
  },
  {
    "query_id": "Q055",
    "query": "What steps improve upselling success in insurance calls?",
    "expected_intent": "Upselling Strategy (Insurance)",
    "requires": ["success_patterns", "failed_patterns", "recommendations"],
    "complexity": "complex"
  }
]
```
✅ **Evidence Quality**: Are cited transcript spans actually relevant?  
✅ **Actionability**: Are recommendations practical?  
✅ **Explainability**: Can judges understand the reasoning?  
✅ **Multi-turn**: Can it handle follow-up questions?

This query dataset tests all these dimensions! 🎯
