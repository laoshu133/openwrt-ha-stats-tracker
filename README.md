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

1. Create installation directory and download files:
```bash
mkdir -p /etc/config/openwrt-ha-stats-tracker && cd $_
curl -O https://github.com/laoshu133/openwrt-ha-stats-tracker/raw/refs/heads/master/ha-stats-tracker
chmod +x ha-stats-tracker
```

2. Configure settings using the setup wizard:
```bash
./ha-stats-tracker setup
```

3. Set up autostart service:
```bash
./ha-stats-tracker startup
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

### v1.2.0
- Added `setup` command for interactive configuration
- Added `help` command to display available commands
- Improved error handling and user experience

### v1.1.0
- Added `startup` command to automatically install and configure the service for boot
- Added `remove_all_entities` command to remove all entities from Home Assistant

### v1.0.0
- Initial release with core features including CPU temperature, system load, and CPU usage monitoring

## License

MIT License
