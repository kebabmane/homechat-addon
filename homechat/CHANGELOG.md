# Changelog

All notable changes to the HomeChat Home Assistant Add-on will be documented in this file.

## [1.0.11] - 2025-01-09

### Fixed
- Enable mDNS/Zeroconf discovery in add-on mode (was previously disabled)
- Fix Bullet N+1 query warning in DM channels endpoint

## [1.0.10] - 2025-01-09

### Fixed
- Fix admin dashboard crash caused by incorrect route helper (admin_admin_credentials_path typo)

### Added
- Command palette (Cmd+K / Ctrl+K) for quick channel switching
- Swipe-to-open gesture for mobile sidebar navigation
- Unread message indicators in sidebar
- Message entrance animations and micro-interactions
- Custom SVG illustrations for empty states
- Send confirmation feedback (checkmark animation)
- Auto-focus message input on channel load and after sending

### Improved
- Mobile touch targets increased to 44px minimum for better accessibility
- Mobile keyboard handling with visualViewport API
- Sidebar spring animation for smoother mobile experience
- Privacy: Switched to system font stack (removed external Google Fonts dependency)

## [1.0.1] - 2024-09-19

### Fixed
- Updated HomeChat icon to match new unified branding across all platforms
- Improved icon visibility and consistency in Home Assistant dashboard
- Enhanced add-on visual identity

### Changed
- Refreshed add-on icon with modern chat bubble design
- Updated icon.png with high-quality 192x192 resolution

## [1.0.0] - 2024-12-09

### Added
- Initial release of HomeChat Home Assistant Add-on
- Self-hosted chat functionality for Home Assistant households
- Rails 8 application with SQLite database
- Offline-first design (works without internet connectivity)
- Real-time messaging with ActionCable WebSockets
- Built-in user management system
- PWA support for mobile app-like experience
- Tailwind CSS responsive interface
- Home Assistant ingress integration
- Configurable site name and signup controls
- Multi-architecture support (aarch64, amd64, armhf, armv7, i386)
- SSL/TLS support
- Configurable logging levels
- Data persistence across add-on updates
- Admin panel for site configuration
- User settings for personalization
- S6 overlay service management
- AppArmor security profile
- Comprehensive documentation and troubleshooting guide

### Technical Details
- Built on Home Assistant base images (Alpine 3.19)
- Ruby 3.3.0 runtime
- SQLite 3 database
- Rails 8 with Hotwire/Turbo
- ActionCable for real-time features
- Tailwind CSS for styling
- Database stored in `/data/production.sqlite3`
- File uploads stored in `/data/storage/`
- Default port: 3000
- Supports Home Assistant ingress
- Service managed by s6-overlay