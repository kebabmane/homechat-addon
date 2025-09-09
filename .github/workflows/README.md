# HomeChat Addon Build Workflow

This GitHub Actions workflow automatically builds and publishes HomeChat addon container images for Home Assistant.

## 🏗️ Build Process

### Platforms Built
- **linux/amd64** - Intel/AMD 64-bit (most cloud servers, Intel Macs)
- **linux/arm64** - ARM 64-bit (Apple Silicon, modern ARM servers, Raspberry Pi 4+)

### Registry
- **GitHub Container Registry (GHCR)**: `ghcr.io/kebabmane/addon-homechat`

## 🚀 Triggers

The workflow runs on:
- **Push to main branch** - Builds and pushes `latest` tag
- **Git tags** (v1.0.0) - Builds and pushes versioned releases  
- **Pull requests** - Builds images for testing (no push)

## 📦 Image Tags

| Trigger | Tag | Description |
|---------|-----|-------------|
| `main` branch | `latest` | Latest development build |
| `v1.2.3` tag | `1.2.3`, `1.2`, `1` | Semantic versioning |
| PR | `pr-123` | Pull request builds |

## 🔧 Build Features

### Multi-Architecture Support
- Uses Docker Buildx with QEMU for cross-platform builds
- Creates multi-arch manifest for single image reference
- Optimized build contexts and layer caching

### Security
- Uses GitHub's built-in `GITHUB_TOKEN` for authentication
- Minimal permissions (contents: read, packages: write)
- No external secrets required

### Performance
- **GitHub Actions caching** for faster builds
- **Layer caching** to reuse unchanged layers
- **Parallel builds** across architectures

### Automation
- **Auto-updates addon config** with latest image reference
- **Automatic semantic versioning** from git tags
- **Build metadata** injected as OCI labels

## 🏷️ Image Labels

Built images include comprehensive metadata:
```yaml
org.opencontainers.image.title: "Home Assistant Add-on: HomeChat"
org.opencontainers.image.description: "Self-hosted chat for Home Assistant households"  
org.opencontainers.image.source: "https://github.com/kebabmane/homechat-addon"
org.opencontainers.image.version: "1.0.0"
org.opencontainers.image.created: "2024-01-01T00:00:00Z"
org.opencontainers.image.revision: "abc123..."
```

## 🔍 Build Context

The workflow:
1. **Checks out both repositories**:
   - `kebabmane/homechat` - Rails application source
   - `kebabmane/homechat-addon` - Addon configuration and Dockerfile

2. **Builds from addon Dockerfile** with Rails app as context
3. **Pushes to GHCR** with proper tagging
4. **Updates addon config** to reference new image

## 📋 Manual Triggering

To manually trigger a build:

```bash
# Create and push a tag
git tag v1.0.0
git push origin v1.0.0

# Or push to main branch  
git push origin main
```

## 🐛 Troubleshooting

### Build Failures
- Check the Actions tab for detailed logs
- Verify Dockerfile syntax and base image availability
- Ensure all required files are present in both repositories

### Permission Issues
- Verify repository has packages write permission
- Check that GITHUB_TOKEN has sufficient scope
- Ensure actor has push access to repository

### Image Issues
- Test locally with Docker Buildx:
```bash
docker buildx build --platform linux/amd64,linux/arm64 \
  -t test-image \
  -f homechat/Dockerfile .
```

## 🔄 Workflow Status

Current workflow status: [![Build Status](https://github.com/kebabmane/homechat-addon/workflows/Build%20and%20Push%20HomeChat%20Addon/badge.svg)](https://github.com/kebabmane/homechat-addon/actions)

## 📈 Usage Analytics

View container download stats:
- [GitHub Container Registry](https://github.com/users/kebabmane/packages/container/package/addon-homechat)