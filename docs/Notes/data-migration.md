
### 3. `docs/notes/data-migration.md`
Documenting your AX 2012 to D365 experience here is high-value for recruiters.

```markdown
# Legacy Migration Patterns (AX 2012 -> D365)

## The Migration Framework
* **Extraction:** Exporting SQL-based schema to Azure Blob Storage using self-hosted Integration Runtimes.
* **Transformation:** Mapping legacy fields to the Common Data Service (CDS) / Dataverse model.
* **Validation:** Automated reconciliation reports to ensure 100% data fidelity.

## Lessons Learned
1. **Schema Drift:** Metadata mapping is the most significant bottleneck. 
2. **Performance:** Utilize partitioned parallel execution to reduce cutover time during the migration window.