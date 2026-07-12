---
change: CHG-0001-adopt-specsync-5-0-1-and-trust-1-0-0-governance-for-the-weather-fledge-plugin
artifact: testing
---

# Testing

- `specsync check --strict --force` at committed threshold zero
- `specsync agents status`
- `bash -n bin/fledge-weather`
- `shellcheck bin/fledge-weather`
- Offline `--help` and `--version` smoke checks
- Plugin manifest binary-path validation
- `fledge trust doctor`

Live geocoding, forecast, and IP auto-detection checks remain independently authorized and are not required for this deterministic migration gate.
