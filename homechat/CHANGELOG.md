# Changelog

All notable changes to the HomeChat Home Assistant Add-on will be documented in this file.

## [1.0.17] - 2026-01-11

### Added
- **Scoped API Tokens:** Fine-grained permission system for API tokens
  - Token types: user, admin, bot
  - Scope patterns: `admin:*`, `channel:*:read`, `channel:<id>:write`, etc.
  - Channel-specific permissions with read/write/manage levels
  - Optional token expiration dates
  - Bot tokens restricted from user data endpoints
  - Backward compatible: existing tokens retain full access

### Improved
- Admin UI: Token management with scope selection and channel binding
- Token edit page for modifying permissions after creation

## [1.0.16] - 2025-01-10

### Fixed
- **Critical:** Enable image thumbnails for iOS app
  - Added `image_processing` gem for Active Storage variants
  - Added `vips` library to Docker image for image processing
  - Thumbnails now generate correctly for image attachments

## [1.0.15] - 2025-01-10

### Fixed
- **Critical:** iOS app image attachments now load correctly
  - Switched Active Storage from redirect mode to proxy mode
  - Files are now served directly through Rails without HTTP redirects
  - This fixes compatibility issues with mobile apps and CORS
  - Reference: https://github.com/rails/rails/issues/33549

## [1.0.14] - 2025-01-10

### Fixed
- **Critical:** Image attachments now persist across container restarts
  - Storage directory symlinked from /app/storage -> /data/storage
  - Existing uploads migrated automatically on upgrade
- Images were returning 404 after addon restarts due to non-persistent storage

## [1.0.13] - 2025-01-10

### Added
- Push notification callbacks moved to Message model (single source of truth)
- Mention-specific FCM notifications when @username is used
- Auto-invite mentioned users to channels

### Fixed
- Remove redundant FCM notification calls from API controller
- Notifications now work consistently across web, API, and mobile origins

### Documentation
- Updated FCM_SETUP.md with notification types table

## [1.0.12] - 2025-01-09

### Fixed
- Fix channel join routing (404 error when navigating directly to join URL)
- Fix Turbo method syntax for link_to helpers (Rails 7+ compatibility)
- Add missing googleauth gem to Gemfile.lock (was causing build failures)
- Update all gems to latest versions (Rails 8.0.4)

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