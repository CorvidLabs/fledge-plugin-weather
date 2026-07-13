---
spec: weather.spec.md
---

## Requirements

### REQ-weather-001

The plugin SHALL accept positional CLI locations and named `location`, `forecast`, and `units` tool arguments.

### REQ-weather-002

The plugin SHALL auto-detect a location when none is supplied and geocode explicit locations through the documented public services.

### REQ-weather-003

The plugin SHALL render current conditions and optionally a seven-day forecast using metric or imperial units.

### REQ-weather-004

The plugin SHALL return a non-zero result with an actionable message for missing dependencies, invalid options, unresolved locations, and network failures.

## Constraints

- Live reports require `curl`, `jq`, and access to the public geolocation and Open-Meteo endpoints.
- Blocking CI must remain deterministic and must not treat third-party service availability as repository correctness.

## Out of Scope

- Persisting weather history or user location.
- Providing service-availability guarantees for third-party APIs.
