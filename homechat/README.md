# Home Assistant Add-on: HomeChat

![Supports aarch64 Architecture][aarch64-shield]
![Supports amd64 Architecture][amd64-shield]
![Supports armhf Architecture][armhf-shield]
![Supports armv7 Architecture][armv7-shield]
![Supports i386 Architecture][i386-shield]

Self-hosted chat for Home Assistant households. Built on Rails 8, SQLite, Tailwind, and Hotwire.

## About

HomeChat is designed to run on a LAN with zero Internet connectivity, making it perfect for households that want private, secure communication that doesn't rely on external services.

**Key Features:**
- **Offline-First**: Works completely without internet connectivity
- **Real-time Messaging**: Built with Rails 8 and Hotwire for instant messaging
- **User Management**: Built-in user system with admin controls
- **PWA Support**: Install as a mobile app for native-like experience
- **SQLite Database**: No external database required
- **Tailwind CSS**: Clean, responsive interface

## Configuration

### Site Name
The name that appears in the HomeChat interface header.

### Allow Signups
Control whether new users can create accounts. Disable this to lock down the chat to existing users only.

### Port
The port HomeChat will listen on (default: 3000).

### SSL
Enable SSL/TLS encryption. Requires SSL certificates in the Home Assistant SSL directory.

### Log Level
Control the verbosity of HomeChat logs (debug, info, warning, error).

## Usage

1. After installation, HomeChat will be available in your Home Assistant sidebar
2. The first user to sign up will automatically become an administrator
3. Administrators can:
   - Configure site settings
   - Control user signups
   - Manage user accounts
4. All chat data is stored locally on your Home Assistant instance

## Data Storage

- **Database**: SQLite database stored in `/data/production.sqlite3`
- **Uploads**: File uploads stored in `/data/storage/`
- **Logs**: Application logs available in Home Assistant logs

## Troubleshooting

### Add-on won't start
1. Check the Home Assistant logs for error messages
2. Ensure the port is not already in use
3. Verify sufficient disk space for the database

### Can't access the web interface
1. Check that the port is correctly configured
2. Ensure ingress is enabled in the add-on configuration
3. Try accessing directly via `http://homeassistant.local:3000`

### Database issues
The add-on will automatically create and migrate the database on first start. If you encounter database issues:
1. Stop the add-on
2. Delete `/data/production.sqlite3`
3. Restart the add-on (this will recreate the database)

## Support

For support and bug reports, please visit the [HomeChat repository](https://github.com/kebabmane/homechat).

[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg
[armhf-shield]: https://img.shields.io/badge/armhf-yes-green.svg
[armv7-shield]: https://img.shields.io/badge/armv7-yes-green.svg
[i386-shield]: https://img.shields.io/badge/i386-yes-green.svg