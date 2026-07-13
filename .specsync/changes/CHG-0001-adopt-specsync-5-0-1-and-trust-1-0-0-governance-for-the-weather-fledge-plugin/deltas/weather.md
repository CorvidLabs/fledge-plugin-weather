## MODIFIED
### SPEC SECTION Change Log
| Version | Date | Changes |
|---------|------|---------|
| 1 | 2026-05-18 | Added named-argument support for the Weather command. |
| 2 | 2026-05-27 | Corrected international geocoding and removed the Python dependency. |
| 3 | 2026-07-13 | Reconciled existing command documentation and stable requirement IDs for SpecSync 5.0.1 governance; runtime behavior is unchanged. |

### REQUIREMENT REQ-weather-001
The plugin SHALL accept positional CLI locations and named location, forecast, and units tool arguments.

Acceptance Criteria
- Offline help smoke verifies the positional location and forecast and units flags remain exposed.
- Deterministic manifest validation confirms the Weather command retains the location, forecast, and units tool arguments without making live service calls.

