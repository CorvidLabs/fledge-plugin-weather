---
spec: weather.spec.md
---

## Context

Developers and agents need a compact terminal weather report without managing an API key. The plugin combines public geocoding and forecast services while keeping deterministic help, version, syntax, and manifest behavior available offline.

## Related Modules

- `plugin.toml` maps Fledge command and tool-interface arguments to the shell executable.

## Design Decisions

- Use Open-Meteo services because they require no repository or user secret.
- Accept positional CLI arguments and named tool-interface arguments through one parser.
- Keep live API calls outside the blocking verification lane because they depend on independent network services.
