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
[![Build Status][build-shield]][build-url]
[![Container Image][image-shield]][image-url]

## 🏗️ Automated Builds

HomeChat addon containers are automatically built and published to GitHub Container Registry:

- **Multi-architecture support**: AMD64 (Intel/AMD) and ARM64 (Apple Silicon, modern ARM)
- **Automatic updates**: New builds triggered on every commit to main branch
- **Versioned releases**: Semantic versioning with git tags (v1.0.0)
- **Registry**: `ghcr.io/kebabmane/addon-homechat`

### Build Process
- Uses GitHub Actions with Docker Buildx for cross-platform builds
- Optimized layer caching for faster builds
- Comprehensive OCI labels and metadata
- Automated addon configuration updates

[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg
[build-shield]: https://github.com/kebabmane/homechat-addon/workflows/Build%20and%20Push%20HomeChat%20Addon/badge.svg
[build-url]: https://github.com/kebabmane/homechat-addon/actions
[image-shield]: https://ghcr-badge.egpl.dev/kebabmane/addon-homechat/latest_by_date?label=Image%20Size
[image-url]: https://github.com/users/kebabmane/packages/container/package/addon-homechat