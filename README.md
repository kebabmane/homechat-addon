# HomeChat Home Assistant Add-on Repository

[![Build Status][build-shield]][build-url]
[![GitHub Release][release-shield]][release-url]

Self-hosted, offline-first chat for Home Assistant households.

## Quick Installation

[![Add Repository][add-repo-shield]][add-repo-url]

Or manually:
1. Go to **Settings** > **Add-ons** > **Add-on Store**
2. Click **⋮** (menu) > **Repositories**
3. Add: `https://github.com/kebabmane/homechat-addon`
4. Find "HomeChat" and click **Install**

## Features

| Feature | Description |
|---------|-------------|
| **Offline-First** | Works without internet on your LAN |
| **Real-Time** | Instant messaging with WebSockets |
| **PWA Support** | Install as mobile app |
| **SQLite** | No external database needed |
| **Multi-Arch** | AMD64, ARM64, ARMv7, i386 |

## Add-ons in This Repository

### HomeChat

Private chat for households built on Rails 8, SQLite, and Hotwire.

![Supports aarch64][aarch64-shield]
![Supports amd64][amd64-shield]
![Supports armhf][armhf-shield]
![Supports armv7][armv7-shield]
![Supports i386][i386-shield]

**Documentation:**
- [Quick Start](homechat/README.md)
- [Configuration](homechat/DOCS.md)
- [Changelog](homechat/CHANGELOG.md)

## Architecture Support

| Architecture | Description | Tested |
|--------------|-------------|--------|
| `amd64` | Intel/AMD 64-bit | Yes |
| `aarch64` | ARM 64-bit (Pi 4, Apple Silicon) | Yes |
| `armv7` | ARM 32-bit (Pi 3) | Yes |
| `armhf` | ARM Hard Float | Yes |
| `i386` | Intel 32-bit | Yes |

## Automated Builds

Containers are automatically built and published to GitHub Container Registry:

- **Registry**: `ghcr.io/kebabmane/addon-homechat`
- **Triggers**: Commits to main, version tags
- **Multi-arch**: All architectures built in parallel

## Related Repositories

| Repository | Description |
|------------|-------------|
| [homechat](https://github.com/kebabmane/homechat) | Core Rails application |
| [homechat-integration](https://github.com/kebabmane/homechat-integration) | HA custom component |
| [homechat-android](https://github.com/kebabmane/homechat-android) | Android app |
| [homechat-ios](https://github.com/kebabmane/homechat-ios) | iOS app |

## Support

- [GitHub Issues](https://github.com/kebabmane/homechat-addon/issues)
- [Main Documentation](https://github.com/kebabmane/homechat/blob/main/docs/)

## License

MIT License

[build-shield]: https://github.com/kebabmane/homechat-addon/workflows/Build%20and%20Push%20HomeChat%20Addon/badge.svg
[build-url]: https://github.com/kebabmane/homechat-addon/actions
[release-shield]: https://img.shields.io/github/v/release/kebabmane/homechat-addon
[release-url]: https://github.com/kebabmane/homechat-addon/releases
[add-repo-shield]: https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg
[add-repo-url]: https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fkebabmane%2Fhomechat-addon
[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg
[armhf-shield]: https://img.shields.io/badge/armhf-yes-green.svg
[armv7-shield]: https://img.shields.io/badge/armv7-yes-green.svg
[i386-shield]: https://img.shields.io/badge/i386-yes-green.svg
