---
spec: weather.spec.md
---

## Test Plan

### Deterministic Tests

- Run `bash -n` and ShellCheck against the executable.
- Verify `--help` and `--version` return successfully without network access.
- Verify the plugin manifest names the extensionless executable.

### Independently Authorized Live Tests

- Exercise explicit-city, forecast, imperial-unit, and IP auto-detection paths only when network access is intentionally authorized.
- Treat third-party availability failures as environmental evidence rather than weakening the deterministic gate.
