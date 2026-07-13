---
change: CHG-0001-adopt-specsync-5-0-1-and-trust-1-0-0-governance-for-the-weather-fledge-plugin
artifact: design
---

# Design

Preserve the stable spec and existing CI. Add companion requirements with stable IDs and a separate job named `trust`, pinned to immutable Trust 1.0.0. The Fledge lifecycle runs Bash syntax, ShellCheck, offline help/version smoke tests, and manifest validation. Risk is blocking, provenance is progressive, Atlas is off, and contract coverage is advisory zero with the extensionless-file rationale.
