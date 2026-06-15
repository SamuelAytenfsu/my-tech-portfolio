# Prompt Engineering
The practice of crafting inputs to LLMs to elicit accurate, relevant, and safe outputs. Techniques include few-shot examples, chain-of-thought, role prompting, and structured output constraints.
## Techniques
### Few-Shot Prompting
```
System: Extract structured data from RFP text.
User: 
Examples:
Input: "Need 500 units delivered by March 2025"
Output: {"quantity": 500, "deadline": "2025-03"}

Input: "Seeking vendor for IT support services, budget ~$200k"
Output: {"service": "IT support", "budget_usd": 200000}

Now extract: "Procuring 3 years of cloud hosting for 10TB workload"
```

### Chain-of-Thought
```
"Think step by step before answering. 
First identify the requirement type, 
then extract quantities and dates, 
then output JSON."
```

## Anti-patterns to Avoid
- Vague instructions ("summarize this")
- No output format specified
- No grounding with retrieval (hallucination risk)
- Overly long system prompts that exceed attention span