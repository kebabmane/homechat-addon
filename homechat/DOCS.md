# HomeChat Add-on Configuration

Complete configuration reference for the HomeChat Home Assistant add-on.

## Configuration Options

### Site Settings

#### Site Name
| | |
|-|-|
| **Key** | `site_name` |
| **Type** | String |
| **Default** | `HomeChat` |

Display name shown in the header and browser title.

#### Allow Signups
| | |
|-|-|
| **Key** | `allow_signups` |
| **Type** | Boolean |
| **Default** | `true` |

- `true` — Anyone can create an account
- `false` — Only existing users can log in

> **Note**: First user always becomes admin, regardless of this setting.

### Network Settings

#### Port
| | |
|-|-|
| **Key** | `port` |
| **Type** | Integer (1-65535) |
| **Default** | `3000` |

HTTP port HomeChat listens on.

#### SSL
| | |
|-|-|
| **Key** | `ssl` |
| **Type** | Boolean |
| **Default** | `false` |

Enable HTTPS. Requires certificates in `/ssl/`.

> **Tip**: HA ingress provides SSL automatically. Only enable for direct access.

#### Access Mode
| | |
|-|-|
| **Key** | `access_mode` |
| **Type** | Enum |
| **Default** | `ingress` |

| Value | Description | mDNS Discovery |
|-------|-------------|----------------|
| `ingress` | Access through HA sidebar | Not available |
| `direct_ssl` | Direct HTTPS access | Works |
| `direct_http` | Direct HTTP access | Works |

> **Note**: mDNS/Bonjour discovery (for iOS app auto-detection) only works with `direct_http` or `direct_ssl` modes because it requires host network access.

#### Discovery Mode
| | |
|-|-|
| **Key** | `discovery_mode` |
| **Type** | Enum |
| **Default** | `auto` |

| Value | Description |
|-------|-------------|
| `auto` | mDNS + Nabu Casa if available |
| `local_only` | mDNS only (no cloud) |
| `disabled` | No discovery |

> **Tip**: Use `direct_http` access mode for LAN discovery to work. The iOS app can auto-detect HomeChat servers via mDNS when using direct access modes.

#### Network Range
| | |
|-|-|
| **Key** | `network_range` |
| **Type** | CIDR notation |
| **Default** | `192.168.0.0/16` |

Network range for trusted proxy configuration. Used for CSRF protection with ingress.

**Common values:**
| Your HA IP | Use Range |
|------------|-----------|
| `192.168.x.x` | `192.168.0.0/16` |
| `10.x.x.x` | `10.0.0.0/8` |
| `172.16-31.x.x` | `172.16.0.0/12` |

### Integration Settings

#### Enable Integrations
| | |
|-|-|
| **Key** | `enable_integrations` |
| **Type** | Boolean |
| **Default** | `true` |

Enable API endpoints for external integrations.

#### Auto-Create API Token
| | |
|-|-|
| **Key** | `auto_create_api_token` |
| **Type** | Boolean |
| **Default** | `false` |

Automatically generate an API token on startup. Token is shown in logs.

#### Home Assistant Integration
| | |
|-|-|
| **Key** | `home_assistant_integration` |
| **Type** | Boolean |
| **Default** | `false` |

Enable Home Assistant-specific features for the [homechat-integration](https://github.com/kebabmane/homechat-integration).

### Logging

#### Log Level
| | |
|-|-|
| **Key** | `log_level` |
| **Type** | Enum |
| **Default** | `info` |

| Level | Description |
|-------|-------------|
| `debug` | Detailed debugging info |
| `info` | Normal operation |
| `warning` | Warnings and errors only |
| `error` | Errors only |

## Data Persistence

All data is stored in `/data/` and persists across updates:

| Path | Contents |
|------|----------|
| `/data/production.sqlite3` | Database (users, messages, channels) |
| `/data/storage/` | File uploads and attachments |
| `/data/secret_key_base` | Encryption key (auto-generated) |
| `/data/admin_credentials.json` | Auto-generated admin (if enabled) |

## Access Methods

### Via Home Assistant Ingress (Recommended)

1. Click HomeChat in the HA sidebar
2. SSL provided by Home Assistant
3. Uses HA authentication session

### Direct Access

1. Navigate to `http://[HA_IP]:3000`
2. Or `http://homeassistant.local:3000`
3. Requires HomeChat login

### External Access

1. Configure HA for external access
2. Access via HA ingress (recommended)
3. Or port forward and enable SSL

## First Time Setup

1. **Start the add-on**
2. **Open HomeChat** from sidebar or direct URL
3. **Create first account** — becomes admin automatically
4. **Configure settings** at `/admin/settings`
5. **Disable signups** if desired (for security)

## Admin Features

Administrators (`/admin/`) can:

- **Settings** — Site name, signups, integrations
- **Users** — View and manage accounts
- **Bots** — Create AI assistants
- **Integrations** — API tokens, webhooks
- **System** — View system information

## User Features

Each user (`/settings`) can:

- Change username and password
- Enable two-factor authentication
- Set timezone preferences
- Configure "Enter to send"

## Backup & Restore

### Backup

Included in HA backups automatically. For manual backup:

```bash
# Stop add-on first
cp -r /addon_configs/local_homechat/data/ /backup/homechat/
```

### Restore

```bash
# Stop add-on first
cp -r /backup/homechat/data/* /addon_configs/local_homechat/data/
# Start add-on
```

## Troubleshooting

### Add-on Won't Start

| Check | Solution |
|-------|----------|
| Disk space | Free up space |
| Port conflict | Change port or stop conflicting service |
| Logs | Check HA > Settings > Add-ons > HomeChat > Log |

### Can't Access Web Interface

| Check | Solution |
|-------|----------|
| Add-on running | Start the add-on |
| Port correct | Verify port in config |
| Firewall | Allow port through firewall |
| Ingress | Try direct URL access |

### Database Issues

```bash
# Stop add-on
# Backup current database (if possible)
cp /data/production.sqlite3 /data/production.sqlite3.bak
# Delete corrupted database
rm /data/production.sqlite3
# Start add-on (creates fresh database)
```

### Login Problems

| Issue | Solution |
|-------|----------|
| Forgot password | Reset via admin or recreate database |
| Account locked | Wait 30 min or unlock via console |
| 2FA lost | Admin can disable, or use backup codes |

### Performance Issues

| Check | Solution |
|-------|----------|
| Log level | Set to `info` (not `debug`) |
| Database size | Large databases may slow down |
| Resources | Check HA system resources |

## FAQ

**Q: Can I use HomeChat without Home Assistant?**
A: Yes! Use the [Docker deployment](https://github.com/kebabmane/homechat) for standalone use.

**Q: How do I connect the HA integration?**
A: Install [homechat-integration](https://github.com/kebabmane/homechat-integration) and use the API token from admin panel.

**Q: Is my data encrypted?**
A: Passwords are bcrypt hashed. Enable SSL for encrypted connections.

**Q: Can I migrate from Docker to the add-on?**
A: Copy the `/data/` directory contents to the add-on data directory.

## Related Documentation

- [Main HomeChat Docs](https://github.com/kebabmane/homechat/blob/main/docs/)
- [HA Integration Setup](https://github.com/kebabmane/homechat/blob/main/docs/deployment/home-assistant.md)
- [Security Guide](https://github.com/kebabmane/homechat/blob/main/docs/security/hardening-guide.md)
