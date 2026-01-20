# Dashy - Quick Reference Guide

## What is Dashy? 🎯

Dashy is a **self-hosted dashboard** that helps you organize and access all your web services from one place. Think of it as a customizable homepage for your homelab, development environment, or personal web services.

```
┌─────────────────────────────────────────────────────────┐
│                    YOUR DASHY DASHBOARD                  │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐              │
│  │  GitHub  │  │   Plex   │  │ Pi-hole  │              │
│  └──────────┘  └──────────┘  └──────────┘              │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐              │
│  │ Portainer│  │ Nextcloud│  │  Grafana │              │
│  └──────────┘  └──────────┘  └──────────┘              │
└─────────────────────────────────────────────────────────┘
```

## 🚀 Quick Start (30 seconds)

### Using Docker (Recommended)
```bash
docker run -p 8080:8080 lissy93/dashy
```
Open http://localhost:8080

### Using Docker Compose
```yaml
version: '3.8'
services:
  dashy:
    image: lissy93/dashy
    ports:
      - 8080:8080
    volumes:
      - ./my-config.yml:/app/user-data/conf.yml
```

### From Source
```bash
git clone https://github.com/Lissy93/dashy.git
cd dashy
yarn install
yarn build
yarn start
```

## 📋 Core Features (Top 10)

| Feature | What it does |
|---------|--------------|
| 🎨 **Themes** | 20+ built-in themes, custom CSS support |
| 🔍 **Search** | Instant search with keyboard shortcuts |
| 🚦 **Status Checks** | Real-time monitoring of service availability |
| 📊 **Widgets** | Display live data from services (40+ widgets) |
| 🔐 **Authentication** | Built-in auth + SSO support (Keycloak) |
| 📱 **PWA** | Install as standalone app on any device |
| 🌍 **i18n** | 25+ languages supported |
| 📄 **Multi-Page** | Organize services across multiple pages |
| ☁️ **Cloud Sync** | Encrypted backup and restore |
| ⚡ **Fast** | Lightweight, <3MB bundle size |

## 🎯 Common Use Cases

### 1. Homelab Dashboard
```yaml
sections:
  - name: Infrastructure
    items:
      - title: Proxmox
        url: https://proxmox.local:8006
      - title: TrueNAS
        url: https://truenas.local
      
  - name: Services
    items:
      - title: Pi-hole
        url: http://pihole.local/admin
      - title: Portainer
        url: https://portainer.local:9000
```

### 2. Development Dashboard
Access all your dev tools from one place:
- GitHub/GitLab repositories
- CI/CD pipelines
- Documentation sites
- Development databases
- API testing tools

### 3. Media Center Hub
Organize your media services:
- Plex/Jellyfin/Emby
- Sonarr/Radarr/Lidarr
- Transmission/qBittorrent
- Tautulli/Overseerr

## 🏗️ Architecture at a Glance

```
Frontend (Vue.js)
    ↓
Express.js Server
    ↓
conf.yml Configuration
```

### Tech Stack
- **Frontend**: Vue.js 2.7, Vuex, Vue Router
- **Backend**: Node.js, Express.js
- **Config**: YAML-based
- **Build**: Webpack, Vue CLI
- **Container**: Docker (Alpine Linux)

### Key Directories
```
dashy/
├── src/              # Vue.js frontend code
│   ├── components/   # UI components
│   ├── views/        # Main pages
│   └── utils/        # Helper functions
├── services/         # Backend API handlers
├── user-data/        # Your configuration
│   └── conf.yml      # Main config file
└── server.js         # Express server
```

## ⚙️ Configuration Basics

### Minimal Config
```yaml
pageInfo:
  title: My Dashboard
  
sections:
  - name: Bookmarks
    items:
      - title: Google
        url: https://google.com
      - title: GitHub
        url: https://github.com
```

### Adding Features
```yaml
appConfig:
  theme: colorful          # Choose a theme
  statusCheck: true        # Enable status monitoring
  language: en             # Set language
  
sections:
  - name: Services
    icon: fas fa-server
    items:
      - title: My App
        icon: favicon
        url: https://example.com
        statusCheck: true    # Monitor this service
        hotkey: 1            # Press '1' to open
```

## 🎨 Customization Quick Reference

### Change Theme
```yaml
appConfig:
  theme: matrix  # or: material, minimal, nord, bee, etc.
```

### Add Icons
```yaml
items:
  - title: GitHub
    icon: fab fa-github        # Font Awesome
  - title: Custom
    icon: https://my-icon.png  # URL
  - title: Local
    icon: /icons/my-icon.svg   # Local file
```

### Enable Status Checks
```yaml
appConfig:
  statusCheck: true
  statusCheckInterval: 60  # Check every 60 seconds
```

### Add Search
```yaml
appConfig:
  webSearch:
    searchEngine: duckduckgo
    openingMethod: newtab
```

## 🔒 Security Setup

### Basic Authentication
```yaml
appConfig:
  auth:
    users:
      - user: admin
        hash: [SHA-256-hash-of-password]
        type: admin
```

Generate hash:
```bash
echo -n 'your-password' | sha256sum
```

### Environment Variables
```bash
# Basic auth via env vars
BASIC_AUTH_USERNAME=admin
BASIC_AUTH_PASSWORD=secret

# Or enable config-based auth
ENABLE_HTTP_AUTH=true
```

## 📊 Widget Examples

### System Info
```yaml
widgets:
  - type: gl-current-cpu
    options:
      hostname: http://192.168.1.1:61208
```

### Weather
```yaml
widgets:
  - type: weather
    options:
      apiKey: your-api-key
      city: London
```

### RSS Feed
```yaml
widgets:
  - type: rss-feed
    options:
      feedUrl: https://news.ycombinator.com/rss
      limit: 10
```

## 🐳 Docker Tips

### Persist Configuration
```bash
docker run -d \
  -p 8080:8080 \
  -v ~/dashy-config.yml:/app/user-data/conf.yml \
  -v ~/dashy-icons:/app/public/item-icons \
  --name dashy \
  lissy93/dashy
```

### Update Container
```bash
docker pull lissy93/dashy:latest
docker stop dashy
docker rm dashy
# Run with same volumes
```

### View Logs
```bash
docker logs dashy
docker logs -f dashy  # Follow logs
```

## 🔧 Useful Commands

```bash
# Validate configuration
yarn validate-config

# Rebuild after config changes
yarn build

# Start production server
yarn start

# Development mode (hot reload)
yarn dev

# Check application health
yarn health-check
```

## 🌐 Accessing Dashy

### Local Access
- Default: `http://localhost:8080`
- Docker: `http://localhost:[YOUR-PORT]`

### Remote Access
1. **Reverse Proxy** (recommended)
   - Nginx, Caddy, Traefik
   - Add SSL certificate
   - Use domain name

2. **Port Forward**
   - Forward port on router
   - Use DDNS for changing IP

3. **VPN/Tunnel**
   - WireGuard, Tailscale
   - Cloudflare Tunnel

## 📱 Making it a PWA

1. Open Dashy in browser
2. Click browser menu
3. Select "Install App" or "Add to Home Screen"
4. Launch as standalone app

## 🎓 Learning Resources

- **Full Docs**: https://dashy.to/docs
- **Configuration**: See `./docs/configuring.md`
- **Widgets**: See `./docs/widgets.md`
- **Theming**: See `./docs/theming.md`
- **Architecture**: See `./ARCHITECTURE.md`

## 🆘 Quick Troubleshooting

### Config Not Loading
```bash
# Validate config
yarn validate-config

# Check file location
ls -la user-data/conf.yml

# View syntax errors
docker logs dashy | grep -i error
```

### Icons Not Showing
- Check icon syntax (Font Awesome format)
- Verify image URLs are accessible
- Clear browser cache

### Status Checks Failing
- Ensure service is accessible from Dashy
- Check firewall rules
- Increase timeout in config

### Can't Save Config
- Check file permissions
- Ensure not running read-only
- Check disk space

## 🔗 Important Links

- **Demo**: https://demo.dashy.to
- **GitHub**: https://github.com/Lissy93/dashy
- **Docs**: https://dashy.to/docs
- **Discussions**: https://github.com/Lissy93/dashy/discussions
- **Docker Hub**: https://hub.docker.com/r/lissy93/dashy

## 💡 Pro Tips

1. **Start Simple**: Begin with basic config, add features gradually
2. **Use Anchors**: Reuse YAML blocks with `&anchor` and `*alias`
3. **Backup Config**: Use cloud sync or keep in version control
4. **Test Changes**: Use dev mode to preview before building
5. **Check Logs**: Monitor logs when troubleshooting
6. **Update Regularly**: Keep Dashy and dependencies current
7. **Join Community**: Ask questions in GitHub Discussions

## 📊 Performance Tips

- **Optimize Icons**: Use appropriately sized images
- **Limit Widgets**: Only enable widgets you use
- **Status Check Intervals**: Don't check too frequently
- **Disable Unused Features**: Hide components in appConfig
- **Use Local Assets**: Faster than fetching from web

## 🎯 Next Steps

1. ✅ **Install Dashy** - Get it running (5 minutes)
2. ✅ **Basic Config** - Add your first services (10 minutes)
3. 📚 **Explore Features** - Try themes, widgets, search
4. 🎨 **Customize** - Make it yours with themes and layouts
5. 🔒 **Secure** - Add authentication if needed
6. 📱 **Install PWA** - Use as standalone app
7. 🚀 **Advanced** - Multi-page, widgets, custom CSS

---

**Need More Details?**
- See [ARCHITECTURE.md](./ARCHITECTURE.md) for complete technical documentation
- See [README.md](./README.md) for full feature list
- See [docs/](./docs/) for detailed guides

**Have Questions?**
- Check [Discussions](https://github.com/Lissy93/dashy/discussions)
- Review [Issues](https://github.com/Lissy93/dashy/issues)
- Read [Troubleshooting Guide](./docs/troubleshooting.md)

---

**Quick Reference Version**: 1.0  
**Last Updated**: December 2024  
**Dashy Version**: 3.1.1
