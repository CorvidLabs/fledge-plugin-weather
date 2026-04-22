# fledge-plugin-weather

A [fledge](https://github.com/CorvidLabs/fledge) plugin that shows current weather and 7-day forecasts in your terminal, powered by [Open-Meteo](https://open-meteo.com).

## Install

```bash
fledge plugin install CorvidLabs/fledge-plugin-weather
```

## Usage

```bash
# Current weather (auto-detects location from IP)
fledge weather

# Specify a city
fledge weather "New York"
fledge weather Tokyo
fledge weather "São Paulo"

# 7-day forecast
fledge weather --forecast
fledge weather -f "London"

# Imperial units
fledge weather --units imperial
fledge weather -u imperial -f "Chicago"
```

## Options

| Flag | Description |
|------|-------------|
| `-f, --forecast` | Show 7-day forecast |
| `-u, --units` | `metric` (default) or `imperial` |
| `-h, --help` | Show help |
| `-v, --version` | Show version |

## Requirements

- `curl` — for API requests
- `jq` — for JSON parsing
- `python3` — for URL encoding (only when specifying a location name)

No API key required. Open-Meteo is free and open-source.

## License

MIT
