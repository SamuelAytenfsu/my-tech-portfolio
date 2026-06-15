# Semantic Kernel (SK)
Open-source AI orchestration frameworks for building LLM-powered applications. Semantic Kernel (Microsoft) and LangChain (Python/JS) both support agent loops, tool binding, memory, and chain composition.
## Basic Agent with Plugin
```python
import asyncio
from semantic_kernel import Kernel
from semantic_kernel.connectors.ai.open_ai import AzureChatCompletion

kernel = Kernel()
kernel.add_service(AzureChatCompletion(
    deployment_name="gpt-4o",
    endpoint=os.environ["AZURE_OPENAI_ENDPOINT"],
    api_key=os.environ["AZURE_OPENAI_KEY"]
))

# Define a native plugin
from semantic_kernel.functions import kernel_function

class LakehousePlugin:
    @kernel_function(description="Query the Fabric Lakehouse Gold layer")
    def query_gold(self, sql: str) -> str:
        return run_sql(sql)  # Your Fabric SQL connector

kernel.add_plugin(LakehousePlugin(), "Lakehouse")
```

## SK vs LangChain Quick Pick
| | Semantic Kernel | LangChain |
|---|---|---|
| Primary language | C# / Python | Python / JS |
| Azure integration | First-class | Via adapters |
| Agent framework | Process Framework | LangGraph |