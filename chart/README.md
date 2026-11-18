## Container Resource Configuration

When specifying container resources in `EventSite` manifests, ensure that `resources.requests.cpu` does not exceed `resources.limits.cpu`. The Kubernetes API server validates that container resource requests are less than or equal to resource limits.

### Example Valid Configuration

```yaml
spec:
  resources:
    requests:
      cpu: "250m"
      memory: "256Mi"
    limits:
      cpu: "500m"
      memory: "512Mi"
```

Setting requests higher than limits (e.g. request `500m` with limit `250m` or default limit) will cause deployment updates to fail with `CannotObserveExternalResource` and block composition reconciliation.
