---
module: weather
version: 3
status: stable
files:
  - bin/fledge-weather
  - plugin.toml
db_tables: []
depends_on: []
---

# Weather Plugin Spec

## Purpose

Single-shot terminal weather report (current conditions + optional 7-day forecast) for a given city. Powered by Open-Meteo's free public API — no API key required.

## Files

- `bin/fledge-weather` — bash binary that does geocoding, fetches forecast, and prints
- `plugin.toml` — declares the `weather` command and its `args` so both CLI users and tool-interface callers (LLM agents) can invoke it

## Public API

The plugin registers one command:

### Command Interface

| Command | Args | Description |
|---------|------|-------------|
| `weather` | `location?`, `forecast?`, `units?` | Print current weather + optional 7-day forecast |

### Args

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `location` | string | no | auto-detect from public IP | City name. Append a country name to disambiguate, e.g. "São Paulo, Brazil" — recognized country names are mapped to Open-Meteo's `countryCode` filter. Bare 2-letter suffixes are treated as part of the name to avoid colliding with US state codes (so "Springfield, IL" still resolves to Illinois). |
| `forecast` | boolean | no | `false` | Include a 7-day forecast in addition to current conditions |
| `units` | string | no | `metric` | `metric` (°C, km/h) or `imperial` (°F, mph) |

## Invariants

1. Both calling conventions must work:
   - CLI: `fledge plugins run weather -- Denver --forecast` (positional + flag)
   - Tool: `[weather(location="Denver", forecast=true)]` (named-only)
2. When `location` is empty, auto-detect via `ipinfo.io` and fall back with a clear error if that lookup fails.
3. Unknown options exit non-zero with `usage` printed.
4. Network failures (geocoding or forecast) print a clear error and exit non-zero; the agent must not see an empty success.

## Behavioral Examples

```
Given the agent calls [weather(location="Denver")]
When the plugin runs
Then fledge invokes `bin/fledge-weather --location Denver`
And the binary geocodes "Denver" via Open-Meteo
And prints current weather for the first match
```

```
Given the agent calls [weather()] with no args
When the plugin runs
Then the binary attempts IP-based location detection
And on success prints weather for that city
And on failure exits 1 with "Could not auto-detect location"
```

```
Given the agent calls [weather(location="Tokyo", forecast=true, units="imperial")]
When the plugin runs
Then fledge invokes `bin/fledge-weather --location Tokyo --forecast --units imperial`
And the binary prints current conditions in °F + 7-day forecast
```

## Error Cases

| Error | When | Behavior |
|-------|------|----------|
| Could not auto-detect location | Empty `location` + IP geolocation fails | Exit 1 with hint to pass `--location` |
| Could not find location '$X' | Geocoding API returns no match for the city name | Exit 1 with the input echoed back |
| `curl` / `jq` not installed | Missing host dependency | Exit 1 with install hint |
| `--units` invalid value | Anything other than `metric` / `imperial` | Open-Meteo treats unknown as default; the binary doesn't pre-validate |
| Open-Meteo API down | Network error / 5xx | jq parsing fails, output is empty/garbage — see follow-up |

## Dependencies

- `curl` — HTTP client
- `jq` — JSON parsing and URL encoding (via `@uri`)
- Open-Meteo public APIs (no key) — forecast + geocoding
- `ipapi.co` (no key) — IP geolocation fallback when no location given

## Change Log

| Version | Date | Changes |
|---------|------|---------|
| 1 | 2026-05-18 | Added named-argument support for the Weather command. |
| 2 | 2026-05-27 | Corrected international geocoding and removed the Python dependency. |
| 3 | 2026-07-13 | Reconciled existing command documentation and stable requirement IDs for SpecSync 5.0.1 governance; runtime behavior is unchanged. |
| 2026-07-13 | CHG-0001-adopt-specsync-5-0-1-and-trust-1-0-0-governance-for-the-weather-fledge-plugin: Adopt SpecSync 5.0.1 and Trust 1.0.0 governance for the weather Fledge plugin |
