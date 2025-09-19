# HomeChat Configuration

## Options

### Site Name
**Default**: `HomeChat`
**Type**: String (optional)

The display name for your HomeChat instance. This appears in the web interface header and browser title.

### Allow Signups
**Default**: `true`
**Type**: Boolean

Controls whether new users can create accounts:
- `true`: Anyone can sign up for an account
- `false`: Only existing users can log in (lockdown mode)

**Note**: The first user to sign up automatically becomes an administrator, regardless of this setting.

### Port
**Default**: `3000`
**Type**: Port number (1-65535)

The port number HomeChat will listen on. If you change this, make sure to update any bookmarks or direct links.

### SSL
**Default**: `false`
**Type**: Boolean

Enable SSL/TLS encryption for HomeChat:
- `true`: Use HTTPS (requires SSL certificates in `/ssl/`)
- `false`: Use HTTP

**Note**: Home Assistant's ingress provides SSL automatically, so this is typically not needed unless accessing HomeChat directly.

### Log Level
**Default**: `info`
**Type**: Selection (debug, info, warning, error)

Controls the verbosity of HomeChat application logs:
- `debug`: Very detailed logs (useful for troubleshooting)
- `info`: Standard operational logs
- `warning`: Only warnings and errors
- `error`: Only error messages

## Data Persistence

HomeChat stores all data in the `/data/` directory, which persists across add-on updates:

- **Database**: `/data/production.sqlite3` - All chat messages, users, and settings
- **Storage**: `/data/storage/` - File uploads and attachments (if enabled)
- **Logs**: Application logs are available through Home Assistant's log viewer

## First Time Setup

1. Install and start the HomeChat add-on
2. Access HomeChat through the Home Assistant sidebar or web UI link
3. Sign up for the first account - this user becomes the administrator
4. Configure site settings in the admin panel (`/admin/settings`)
5. Optionally disable signups to lock down the chat

## Admin Features

The first user to sign up becomes an administrator and can:
- Access admin settings at `/admin/settings`
- Change the site name
- Enable/disable user signups
- View system information
- Manage user accounts (future feature)

## User Management

### Creating Users
- If signups are enabled: Users can create accounts at `/users/sign_up`
- If signups are disabled: Only administrators can create accounts

### User Settings
Each user can customize their experience at `/settings`:
- Change username and password
- Configure "Enter to send" preference
- Update profile information

### Network Range
**Default**: `192.168.0.0/16`
**Type**: String (optional)

Specifies the network range where your Home Assistant server is located. This is used to configure trusted proxies for proper request handling when accessing HomeChat through Home Assistant's ingress interface.

**Common values**:
- `192.168.0.0/16` - Covers most home networks (192.168.x.x)
- `192.168.1.0/24` - Specific subnet (192.168.1.x only)
- `10.0.0.0/8` - Private networks using 10.x.x.x
- `172.16.0.0/12` - Private networks using 172.16-31.x.x

**How to determine your network range**:
1. Find your Home Assistant server's IP address (e.g., 192.168.1.161)
2. Use the appropriate range that includes this IP:
   - If HA IP is 192.168.1.161, use `192.168.0.0/16` or `192.168.1.0/24`
   - If HA IP is 10.0.1.100, use `10.0.0.0/8`

**Note**: This setting is crucial for proper CSRF protection and request handling when using Home Assistant's ingress feature.

## Networking

### Internal Access
HomeChat is accessible through:
- Home Assistant sidebar (recommended)
- Direct URL: `http://homeassistant.local:PORT`
- IP address: `http://[HA_IP]:PORT`

### External Access
To access HomeChat from outside your network:
1. Configure Home Assistant for external access
2. Use Home Assistant's ingress feature (recommended)
3. Or forward the HomeChat port through your router

## Backup and Restore

### Backup
The SQLite database and storage directory should be included in your regular Home Assistant backups. For manual backup:
1. Stop the HomeChat add-on
2. Copy `/addon_configs/local_homechat/data/` to a safe location

### Restore
1. Stop the HomeChat add-on
2. Replace the `/data/` directory contents
3. Restart the add-on

## Troubleshooting

### Common Issues

**Add-on fails to start**
- Check available disk space
- Verify port is not in use by another service
- Check Home Assistant logs for detailed error messages

**Database corruption**
- Stop the add-on
- Backup your data if possible
- Delete `/data/production.sqlite3`
- Restart the add-on (will create a fresh database)

**Performance issues**
- Check system resources (CPU, memory, disk)
- Review log level setting (debug logs can impact performance)
- Consider hardware limitations on older Raspberry Pi models

**Can't access web interface**
- Verify the add-on is running
- Check port configuration
- Try accessing directly via IP address
- Check Home Assistant ingress settings

### Log Files
- Add-on logs: Available in Home Assistant > Settings > Add-ons > HomeChat > Log
- Application logs: Rails logs are forwarded to the add-on logs
- Database logs: SQLite operations logged at debug level