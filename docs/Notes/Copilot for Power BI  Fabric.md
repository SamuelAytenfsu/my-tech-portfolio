# Copilot for Power BI / Fabric
AI-assisted authoring built into Microsoft Fabric and Power BI. Enables natural-language report creation, DAX measure generation, narrative summaries, and pipeline authoring using GPT-4 models integrated into the Fabric platform.
## Capabilities by Surface
| Surface | Copilot Can Do |
|---|---|
| Power BI report | Generate visuals from prompt, write summaries |
| Semantic model | Suggest/write DAX measures |
| Notebook | Generate PySpark code, explain errors |
| Data Pipeline | Suggest activity config |
| Real-Time Dashboard | Create KQL queries from natural language |

## Requirements for Semantic Model Copilot
- F64 capacity or Premium P1 minimum
- Tenant switch: "Users can use Copilot and Azure OpenAI workloads" = On
- Semantic model must be published to Power BI service (not local)

## Example Prompt → DAX
Prompt: "Create a measure for 12-month rolling revenue"
Generated:
```dax
Rolling 12M Revenue =
CALCULATE(
    [Total Revenue],
    DATESINPERIOD(DimDate[Date], LASTDATE(DimDate[Date]), -12, MONTH)
)
```