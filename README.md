# HomeChat Home Assistant Add-on Repository

This repository contains the HomeChat add-on for Home Assistant, providing self-hosted chat functionality for Home Assistant households.

## Installation

1. Add this repository to your Home Assistant add-on store:
   - Go to **Supervisor** > **Add-on Store**
   - Click the menu (three dots) and select **Repositories**
   - Add: `https://github.com/kebabmane/homechat-addon`

2. Find and install the HomeChat add-on
3. Configure the add-on options as needed
4. Start the add-on

## Add-ons in this repository

### HomeChat

Self-hosted chat for Home Assistant households. Built on Rails 8, SQLite, Tailwind, and Hotwire.

**Features:**
- Offline-first design (works without internet)
- Built-in user management
- Real-time messaging with WebSockets
- PWA support for mobile devices
- SQLite database (no external database required)
- Configurable through Home Assistant interface

![Supports aarch64 Architecture][aarch64-shield]
![Supports amd64 Architecture][amd64-shield]
![Supports armhf Architecture][armhf-shield]
![Supports armv7 Architecture][armv7-shield]
![Supports i386 Architecture][i386-shield]

[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg
[armhf-shield]: https://img.shields.io/badge/armhf-yes-green.svg
[armv7-shield]: https://img.shields.io/badge/armv7-yes-green.svg
[i386-shield]: https://img.shields.io/badge/i386-yes-green.svg