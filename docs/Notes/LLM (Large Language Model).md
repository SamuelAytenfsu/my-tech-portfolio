# LLM — Large Language Model
A deep neural network trained on massive text corpora to predict and generate natural language. Foundation for GPT-4o, Claude, Gemini, and open-source models like Llama 3.
## Key Properties
| Property | Explanation |
|---|---|
| Context window | Max tokens the model can process at once (GPT-4o: 128k) |
| Temperature | Controls randomness (0 = deterministic, 1 = creative) |
| Top-p / Top-k | Nucleus sampling controls |
| System prompt | Persistent instructions prepended to every turn |

## Azure OpenAI Call (Python)
```python
from openai import AzureOpenAI

client = AzureOpenAI(
    api_key=os.environ["AZURE_OPENAI_KEY"],
    api_version="2024-05-01-preview",
    azure_endpoint=os.environ["AZURE_OPENAI_ENDPOINT"]
)

response = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": "You are a data engineering assistant."},
        {"role": "user", "content": "Summarize this RFP document: ..."}
    ],
    temperature=0.2,
    max_tokens=1000
)
print(response.choices[0].message.content)
```