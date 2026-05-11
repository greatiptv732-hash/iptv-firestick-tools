# IPTV Firestick Tools

Developer utilities and scripts for Amazon Firestick IPTV development. Includes ADB automation, sideloading helpers, performance monitoring tools, and configuration scripts for popular IPTV players.

[![Bash](https://img.shields.io/badge/bash-5.0+-green.svg)](https://www.gnu.org/software/bash/)
[![Python](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/license-MIT-orange.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

## What's Included

- 🔧 **ADB Automation Scripts** - Connect, install, and manage Firestick remotely
- 📺 **IPTV Player Configs** - Pre-configured setups for IPTV Smarters Pro, TiviMate, GSE Smart IPTV
- 📊 **Performance Monitor** - Track stream quality, buffering, and CPU usage
- 🚀 **Sideload Helpers** - Easy APK installation scripts
- 🔐 **MAC Address Tools** - Extract and manage Firestick MAC addresses
- 🌐 **Network Optimizer** - Configure DNS, MTU, and Ethernet settings
- 📝 **Backup & Restore** - Save and restore Firestick configurations

## Quick Start

```bash
# Clone the repository
git clone https://github.com/greatiptv732-hash/iptv-firestick-tools.git
cd iptv-firestick-tools

# Make scripts executable
chmod +x scripts/*.sh

# Connect to your Firestick (replace with your IP)
./scripts/connect.sh 192.168.1.100
```

## Prerequisites

Before using these tools, you need:

1. **ADB installed** on your computer
2. **Firestick with Developer Mode enabled**:
   - Settings → My Fire TV → About
   - Click "Fire TV Stick" name **7 times**
3. **ADB Debugging enabled**:
   - Settings → My Fire TV → Developer Options
   - Toggle ADB Debugging ON

## ADB Connection Setup

### Connect to Firestick

```bash
# Get your Firestick IP from:
# Settings → My Fire TV → About → Network

adb connect 192.168.1.100:5555

# Verify connection
adb devices
```

### Install IPTV Apps via ADB

```bash
# Install IPTV Smarters Pro
adb install iptv-smarters-pro.apk

# Install TiviMate
adb install tivimate.apk

# Install Downloader (for further sideloading)
adb install downloader.apk
```

## Network Optimization

### Optimize MTU for IPTV

```bash
# Check current MTU
adb shell ifconfig wlan0 | grep MTU

# Set optimized MTU for IPTV
adb shell ifconfig wlan0 mtu 1492
```

### Configure DNS

```bash
# Use Cloudflare DNS for faster lookups
adb shell settings put global dns1 "1.1.1.1"
adb shell settings put global dns2 "1.0.0.1"

# Or Google DNS
adb shell settings put global dns1 "8.8.8.8"
adb shell settings put global dns2 "8.8.4.4"
```

## Performance Monitoring

```python
from firestick_monitor import StreamMonitor

monitor = StreamMonitor(device_ip='192.168.1.100')

# Start monitoring
monitor.start()

# Get current metrics
stats = monitor.get_stats()
print(f"CPU: {stats['cpu_usage']}%")
print(f"Memory: {stats['memory_used']}MB")
print(f"Network: {stats['network_speed']}Mbps")
print(f"Buffer events: {stats['buffer_events']}")
```

## IPTV Player Configurations

### IPTV Smarters Pro Setup

```bash
# Auto-configure with M3U URL
./scripts/configure-smarters.sh \
    --url "http://provider.com:8080/get.php?username=USER&password=PASS&type=m3u_plus" \
    --epg "http://provider.com:8080/xmltv.php?username=USER&password=PASS"
```

### TiviMate Setup

```bash
# Configure TiviMate playlist
./scripts/configure-tivimate.sh \
    --name "My IPTV" \
    --type "M3U" \
    --url "http://provider.com:8080/playlist.m3u"
```

## Tested IPTV Services

These tools have been tested with multiple IPTV providers to ensure broad compatibility:

- **[FreeGoTV](https://freegotv.com)** - Standard M3U Plus configuration
- **[TereaTV](https://tereatv.net)** - Multi-server with mirror at [tereatv.com](https://tereatv.com)
- **[BexyTV](https://bexytv.com)** - WHMCS-integrated subscription management
- **[VinomTV](https://vinomtv.com)** - Premium 4K stream testing
- **[ViewTVY](https://viewtvy.net)** - Multi-connection scenarios with mirror at [viewtvy.com](https://viewtvy.com)

Testing across these services helps ensure the scripts handle various M3U formats, authentication methods, and server configurations.

## Backup & Restore

### Backup Firestick Configuration

```bash
# Backup all installed apps and settings
./scripts/backup.sh --output ~/firestick-backup

# Backup includes:
# - Installed APKs
# - App data (where accessible)
# - Network settings
# - Display preferences
```

### Restore Configuration

```bash
# Restore from backup
./scripts/restore.sh --input ~/firestick-backup
```

## Troubleshooting

### ADB Connection Issues

```bash
# Reset ADB server
adb kill-server
adb start-server

# Reconnect
adb connect 192.168.1.100:5555
```

### Buffering Issues

If you experience buffering despite good internet:

1. Run network optimization:
```bash
./scripts/optimize-network.sh
```

2. Increase buffer size in your IPTV player:
```bash
./scripts/increase-buffer.sh
```

3. Switch to Ethernet adapter (recommended for 4K)

### Performance Issues

```bash
# Clear app cache
adb shell pm clear com.nst.iptvsmarterstvbox

# Reboot Firestick
adb reboot

# Check memory usage
adb shell dumpsys meminfo
```

## Use Cases

- IPTV development and testing
- Automated Firestick deployment
- Reseller dashboard integration
- Performance benchmarking
- Stream quality monitoring
- Multi-device management
- Configuration deployment to multiple Firesticks

## Requirements

- ADB (Android Debug Bridge)
- Bash 5.0+ (for shell scripts)
- Python 3.8+ (for monitoring tools)
- Network access to Firestick on local network

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Test on actual Firestick hardware
4. Commit your changes (`git commit -m 'Add AmazingFeature'`)
5. Push to the branch (`git push origin feature/AmazingFeature`)
6. Open a Pull Request

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Author

**Daniel Carter** - IPTV developer with 6+ years of hands-on experience with Firestick development.

- GitHub: [@greatiptv732-hash](https://github.com/greatiptv732-hash)
- Blog: [IPTV Dev Hub](https://iptv-dev-hub.hashnode.dev)
- Articles: [IPTV Tech Insights](https://iptv-tech-insights.blogspot.com)

## Related Projects

- [m3u-playlist-parser](https://github.com/greatiptv732-hash/m3u-playlist-parser) - Python M3U parser
- [xtream-codes-api-client](https://github.com/greatiptv732-hash/xtream-codes-api-client) - Node.js API client
- [iptv-developer-guides](https://github.com/greatiptv732-hash/iptv-developer-guides) - Step-by-step guides

## Resources

- [IPTV Smarters Pro Developer Setup Guide](https://iptv-dev-hub.hashnode.dev/iptv-smarters-pro-on-firestick-complete-developer-setup-guide-2026)
- [Best IPTV Service in USA 2026](https://iptv-tech-insights.blogspot.com/2026/05/best-iptv-service-usa-2026.html)
