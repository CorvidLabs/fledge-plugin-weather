---
change: CHG-0001-adopt-specsync-5-0-1-and-trust-1-0-0-governance-for-the-weather-fledge-plugin
artifact: context
---

# Context

The weather plugin predates verified SDD governance and already has a stable canonical specification. It is an extensionless Bash executable backed by public geolocation and weather APIs. Existing CI intentionally validates syntax, ShellCheck, help, and version behavior without depending on third-party network availability.
