# k8s-volume-basic

This workspace contains a hardened example Pod manifest and supporting notes.

What I changed:
- Replaced the simple `nginx-pod` with a hardened `secure-nginx` Pod in `pod.yaml`.
- Added pod- and container-level `securityContext` settings (`runAsNonRoot`, `fsGroup`, seccomp).
- Dropped Linux capabilities, disabled privilege escalation, and enforced a read-only root filesystem.
- Added resource `requests` and `limits` to prevent noisy-neighbor issues.
- Added `liveness`, `readiness`, and `startup` probes for robust health checks.
- Added `postStart` / `preStop` lifecycle hooks to initialize and drain gracefully.
- Kept an `emptyDir` memory-backed volume with a conservative `sizeLimit` and a `ConfigMap` mount.

How to apply
Run:

```powershell
kubectl apply -f pod.yaml
```

Notes & recommendations
- Replace the `ConfigMap` name `secure-nginx-config` with your actual configuration.
- Consider adding a `NetworkPolicy` and `PodDisruptionBudget` for production.
- For immutable security policies, use RBAC + admission controllers (e.g. PodSecurity, OPA Gatekeeper).

If you want, I can create incremental commits (45) containing the change history. Confirm and I'll proceed.
