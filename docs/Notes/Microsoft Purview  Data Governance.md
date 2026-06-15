# Microsoft Purview
Microsoft's unified data governance service for discovery, classification, lineage, and access control across the data estate. Integrated into Microsoft Fabric for workspace-level data catalog and sensitivity labels.
## Core Capabilities
```
Purview
  ├── Data Catalog      → Discover & classify assets
  ├── Data Map          → Scan sources, build lineage
  ├── Sensitivity Labels→ Classify PII, financial, etc.
  └── Data Policy       → Enforce access at source
```

## Sensitivity Labels in Fabric
```python
# Programmatically apply label via REST API
import requests

url = "https://api.fabric.microsoft.com/v1/workspaces/{id}/items/{itemId}/sensitivityLabel"
payload = {
    "sensitivityLabelId": "<label-guid>",
    "assignmentMethod": "Privileged"
}
headers = {"Authorization": f"Bearer {token}"}
response = requests.patch(url, json=payload, headers=headers)
```

## DP-600 Exam Focus
- Workspace-level vs item-level sensitivity labels
- Endorsement (Certified vs Promoted)
- Lineage view in Fabric portal