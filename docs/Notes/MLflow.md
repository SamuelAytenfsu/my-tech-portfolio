# MLflow — Experiment Tracking
An open-source platform for managing the ML lifecycle: experiment tracking, model packaging (MLflow Models), model registry, and deployment. Natively integrated into Databricks and available in Microsoft Fabric.
## Log a Training Run
```python
import mlflow
import mlflow.sklearn
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import f1_score

mlflow.set_experiment("/Fabric/predictive-maintenance")

with mlflow.start_run(run_name="rf_v3"):
    model = RandomForestClassifier(n_estimators=200, max_depth=10)
    model.fit(X_train, y_train)
    preds = model.predict(X_test)

    mlflow.log_params({"n_estimators": 200, "max_depth": 10})
    mlflow.log_metric("f1_score", f1_score(y_test, preds))
    mlflow.sklearn.log_model(model, "model")
```

## Register & Load Model
```python
# Register
mlflow.register_model("runs:/<run_id>/model", "PredictiveMaintenance")

# Load for inference
model = mlflow.sklearn.load_model("models:/PredictiveMaintenance/Production")
predictions = model.predict(X_new)
```