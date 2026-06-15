# Tool Calling (Function Calling)
A capability where an LLM can invoke predefined external functions or APIs by emitting structured JSON specifying the function name and arguments. Enables agentic workflows where the model uses tools to gather data or take actions.
## Define a Tool (Azure OpenAI)
```python
tools = [
    {
        "type": "function",
        "function": {
            "name": "query_lakehouse",
            "description": "Run a SQL query against the Fabric Lakehouse Gold layer",
            "parameters": {
                "type": "object",
                "properties": {
                    "sql": {"type": "string", "description": "SQL query to execute"}
                },
                "required": ["sql"]
            }
        }
    }
]

response = client.chat.completions.create(
    model="gpt-4o",
    messages=messages,
    tools=tools,
    tool_choice="auto"
)
```

## Handle the Response
```python
tool_call = response.choices[0].message.tool_calls[0]
if tool_call.function.name == "query_lakehouse":
    args = json.loads(tool_call.function.arguments)
    result = run_sql(args["sql"])  # Your execution function
```