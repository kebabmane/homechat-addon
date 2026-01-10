# Home Assistant Add-on: HomeChat

![Supports aarch64][aarch64-shield]
![Supports amd64][amd64-shield]
![Supports armhf][armhf-shield]
![Supports armv7][armv7-shield]
![Supports i386][i386-shield]

Self-hosted, offline-first chat for Home Assistant households.

## About

HomeChat is a private chat platform designed to work completely offline on your local network. No cloud dependencies, no external services — just secure communication for your household.

**Key Features:**
- **Offline-First** — Works without internet connectivity
- **Real-Time Messaging** — Instant updates via WebSockets
- **User Management** — Built-in admin controls and permissions
- **PWA Support** — Install as a mobile app
- **AI Bots** — Optional LLM-powered assistants
- **HA Integration** — Two-way communication with automations

## Quick Start

1. **Install** the add-on from the add-on store
2. **Start** the add-on
3. **Open** HomeChat from the HA sidebar
4. **Sign up** — First user becomes admin

## Configuration

See [DOCS.md](DOCS.md) for complete configuration reference.

### Basic Settings

| Option | Default | Description |
|--------|---------|-------------|
| `site_name` | HomeChat | Display name in header |
| `allow_signups` | true | Allow new user registration |
| `port` | 3000 | HTTP port |
| `log_level` | info | Logging verbosity |

### Home Assistant Integration

| Option | Default | Description |
|--------|---------|-------------|
| `enable_integrations` | true | Enable API endpoints |
| `auto_create_api_token` | false | Generate API token on start |
| `home_assistant_integration` | false | Enable HA-specific features |

## Data Storage

All data persists across updates in `/data/`:

```
/data/
├── production.sqlite3    # Database
├── storage/              # File uploads
└── secret_key_base       # Encryption key
```

## First User Setup

The first user to sign up automatically becomes an administrator with access to:
- Admin settings (`/admin/settings`)
- User management
- Integration configuration
- Bot management

## Support

- [Configuration Reference](DOCS.md)
- [GitHub Issues](https://github.com/kebabmane/homechat/issues)
- [Main Documentation](https://github.com/kebabmane/homechat/blob/main/docs/)

[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg
[armhf-shield]: https://img.shields.io/badge/armhf-yes-green.svg
[armv7-shield]: https://img.shields.io/badge/armv7-yes-green.svg
[i386-shield]: https://img.shields.io/badge/i386-yes-green.svg
