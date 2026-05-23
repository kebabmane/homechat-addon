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
- **E2EE for Private/DM Content** — Compatible clients encrypt private-channel and direct-message content before upload
- **User Management** — Built-in admin controls and permissions
- **PWA Support** — Install as a mobile app
- **AI Bots** — Optional LLM-powered assistants
- **HA Integration** — Two-way communication with automations

## E2EE Scope

HomeChat provides end-to-end encrypted message content for private channels and direct messages when used with current web, iOS, Android, or macOS clients. The server stores encrypted payloads for those conversations and rejects plaintext writes.

This does not hide all information from the server. Metadata such as users, channel membership, timestamps, message sizes, delivery activity, and encrypted blob presence remains visible. Web E2EE also depends on trusted JavaScript delivery from the add-on. Home Assistant automations, bots, and webhooks are not E2EE clients and should use public/plaintext rooms unless they are upgraded to participate in the E2EE protocol. Attachments are not E2EE yet in private/DM channels.

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
