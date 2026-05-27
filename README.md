# fledge-plugin-weather

[![CI](https://github.com/CorvidLabs/fledge-plugin-weather/actions/workflows/ci.yml/badge.svg)](https://github.com/CorvidLabs/fledge-plugin-weather/actions/workflows/ci.yml)

A [fledge](https://github.com/CorvidLabs/fledge) plugin that shows current weather and 7-day forecasts in your terminal, powered by [Open-Meteo](https://open-meteo.com).

## Install

```bash
fledge plugins install CorvidLabs/fledge-plugin-weather
```

## Usage

```bash
# Current weather (auto-detects location from IP)
fledge weather

# Specify a city
fledge weather "New York"
fledge weather Tokyo
fledge weather "São Paulo"

# Disambiguate by appending a country name
fledge weather "São Paulo, Brazil"
fledge weather "Paris, France"

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
| `-u, --units <SYSTEM>` | `metric` (default) or `imperial` |
| `-h, --help` | Show help |
| `-v, --version` | Show version |

## Requirements

- `curl` -- for API requests
- `jq` -- for JSON parsing (also used for URL encoding)

No API key required. Open-Meteo is free and open-source.

## How It Works

1. **Location resolution** -- If no city is provided, the plugin auto-detects your location from your IP address via ipapi.co. Otherwise it geocodes the city name through Open-Meteo's geocoding API.
2. **Weather data** -- Current conditions and a 7-day forecast are fetched from the Open-Meteo forecast API.
3. **Terminal display** -- Results are rendered with color and weather icons directly in your terminal.

## Development

```bash
# Syntax check
bash -n bin/fledge-weather

# Lint
shellcheck bin/fledge-weather

# Smoke test
bash bin/fledge-weather --help
bash bin/fledge-weather --version
```

Or using fledge tasks:

```bash
fledge run lint
fledge run test
fledge run check
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Ensure `shellcheck bin/fledge-weather` passes with no warnings
4. Open a pull request

## License

MIT
