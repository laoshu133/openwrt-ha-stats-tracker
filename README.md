# OpenWrt HA Stats Tracker

A Node.js-based system monitoring tool that collects OpenWrt system statistics and reports them to Home Assistant.

## Features

- Real-time system metrics monitoring:
  - CPU Temperature
  - System Load (1min, 5min, 15min averages)
  - CPU Usage
- Uses 'push' model for efficient, real-time updates
- No external dependencies (uses built-in Node.js modules)

## Requirements

- Node.js >= 18.0.0

## Installation

1. Clone the repository to your OpenWrt device:
```bash
git clone https://github.com/laoshu133/openwrt-ha-stats-tracker.git
```

2. Copy the example configuration:
```bash
cp settings.json.example settings.json
```

3. Configure your settings:
   To get a Long-Lived Access Token:
    - In Home Assistant, click on your user profile icon (usually in the bottom left corner).
    - Scroll down to the "Long-Lived Access Tokens" section.
    - Click "CREATE TOKEN".
    - Give it a name (e.g., `OpenWrt Stats Tracker`).
    - Copy the generated token. **Important: This token will only be shown once. Store it securely.**

```json
{
  "hass_url": "http://homeassistant.local:8123",
  "hass_token": "<Your_Long_Lived_Access_Token>",
  "update_interval": 60,
  "debug": false
}
```

## Configuration Options

The settings file supports the following options:

- `hass_url`: Your Home Assistant instance URL (default: http://homeassistant.local:8123)
- `hass_token`: Long-lived access token from Home Assistant (required)
- `update_interval`: Update frequency in seconds (default: 60)
- `debug`: Enable debug logging (default: false)

## Home Assistant Integration

The tool creates the following sensors in Home Assistant:

- `sensor.<device_name>_temperature`: System temperature in °C
- `sensor.<device_name>_load_1min`: 1-minute load average
- `sensor.<device_name>_load_5min`: 5-minute load average
- `sensor.<device_name>_load_15min`: 15-minute load average
- `sensor.<device_name>_cpu_usage`: CPU usage percentage
- `sensor.<device_name>_stats_detector_version`: Version of the running tracker

Each sensor includes:
- Friendly name
- Appropriate unit of measurement
- Material Design icon
- Current value

## Troubleshooting

1. Check system logs:
```bash
logread | grep "HA Stats Tracker"
```

2. Report issues:
    - Copy the log output from step 1
    - Create a new issue on GitHub Issues
    - Include your configuration (remember to remove the access token)
    - Describe the problem you're experiencing
    - Paste the log output in a code block

## Changelog

### v1.1.0
- Added `startup` command to automatically install and configure the service for boot
- Added `remove_all_entities` command to remove all entities from Home Assistant

### v1.0.0
- Initial release with core features including CPU temperature, system load, and CPU usage monitoring

## License

MIT License
