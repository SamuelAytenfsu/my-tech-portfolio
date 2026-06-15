# CI/CD for Fabric Data Pipelines
The practice of applying software engineering deployment automation to data assets — using Git version control, automated testing, and deployment pipelines (Azure DevOps, GitHub Actions) to promote Fabric items across Dev/Test/Prod workspaces.
## Fabric Git Integration
```
Workspace (Dev)
    │  Git sync
    ▼
GitHub repo: main branch
    │  PR merge triggers
    ▼
GitHub Actions workflow
    │  Fabric REST API deploy
    ▼
Workspace (Prod)
```

## Deploy via Fabric REST API (Python)
```python
import requests

def deploy_notebook(workspace_id, notebook_path, token):
    with open(notebook_path, "rb") as f:
        content_b64 = base64.b64encode(f.read()).decode()
    
    response = requests.post(
        f"https://api.fabric.microsoft.com/v1/workspaces/{workspace_id}/notebooks",
        headers={"Authorization": f"Bearer {token}"},
        json={"displayName": "SalesETL", "definition": {"parts": [
            {"path": "notebook-content.py", "payload": content_b64, "payloadType": "InlineBase64"}
        ]}}
    )
    return response.json()
```