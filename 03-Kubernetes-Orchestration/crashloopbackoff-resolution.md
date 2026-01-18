# Resolving Pod CrashLoopBackOff
**Scenario:** A Pod keeps restarting and never reaches a "Running" state.

### 1. Investigation "Golden Path"
1. **Events:** `kubectl get events --sort-by=.metadata.creationTimestamp` (Check for scheduling/image issues).
2. **Describe:** `kubectl describe pod [pod_name]` (Check for Liveness/Readiness probe failures).
3. **Logs:** `kubectl logs [pod_name] --previous` (Crucial: checks the logs of the container *before* it crashed).

### 2. Common Causes
* **Config Errors:** Missing environment variables or secret keys.
* **Resource Limits:** The pod is hitting its Memory Limit and getting OOMKilled.
