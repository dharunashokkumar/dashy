# Dashy - Complete Architecture and Overview

## Table of Contents
- [What is Dashy?](#what-is-dashy)
- [Key Features](#key-features)
- [Use Cases](#use-cases)
- [Technology Stack](#technology-stack)
- [Architecture Overview](#architecture-overview)
- [Directory Structure](#directory-structure)
- [Component Architecture](#component-architecture)
- [Configuration System](#configuration-system)
- [Deployment Options](#deployment-options)
- [API Endpoints](#api-endpoints)
- [Data Flow](#data-flow)
- [Security Features](#security-features)

---

## What is Dashy?

**Dashy** is a self-hosted, highly customizable homepage for your homelab or server dashboard. It's designed to help you organize all your self-hosted services, web applications, and tools in a single, accessible, and visually appealing interface.

### Core Purpose
- **Centralized Access Point**: Single dashboard to access all your self-hosted applications
- **Customizable Interface**: Fully configurable via YAML with live editing capabilities
- **Self-Hosted Privacy**: Runs entirely on your own infrastructure with no external dependencies
- **Multi-Platform Support**: Works on Docker, bare metal, or cloud platforms

### Project Information
- **Author**: Alicia Sykes
- **License**: MIT
- **Version**: 3.1.1
- **Language**: JavaScript/Vue.js
- **Repository**: [github.com/Lissy93/dashy](https://github.com/Lissy93/dashy)

---

## Key Features

### 1. **Multi-Page Dashboard Support**
- Create unlimited sub-pages for different categories
- Load configurations from local or remote YAML files
- Easy navigation between different dashboard views

### 2. **Real-Time Status Monitoring**
- Monitor uptime and health of your applications
- Display response times and status codes
- Configurable polling intervals
- Visual traffic-light indicators

### 3. **Dynamic Widgets**
- Display live data from your self-hosted services
- Pre-built widgets for common services (Pi-hole, Portainer, etc.)
- System information widgets (CPU, RAM, network stats)
- RSS feed integration
- Weather, crypto, and more

### 4. **Advanced Search & Navigation**
- Instant search by name, domain, or tags
- Keyboard shortcuts (0-9 for quick access)
- Web search integration with custom search engines
- Search bangs for quick access to specific sites

### 5. **Theming & Customization**
- 20+ built-in color themes
- Visual theme editor with live preview
- Custom CSS support
- Support for custom backgrounds and layouts
- Material Design icons, Font Awesome, and more

### 6. **Authentication & Security**
- Built-in basic authentication
- Keycloak SSO integration
- Multi-user support with different privilege levels
- Read-only guest access
- Header-based authentication support

### 7. **Multiple View Modes**
- **Default View**: Traditional dashboard with sections and items
- **Workspace View**: Multi-tasking view with embedded iframes
- **Minimal View**: Clean startpage for browsers

### 8. **Cloud Backup & Sync**
- End-to-end encrypted cloud backup
- Restore configurations across instances
- No server-side storage of unencrypted data

### 9. **Internationalization**
- Support for 25+ languages
- Auto-detection of user's locale
- Easy language switching through UI

### 10. **Progressive Web App (PWA)**
- Installable as a standalone app
- Basic offline functionality
- Service worker support

---

## Use Cases

### 1. **Homelab Dashboard**
Perfect for managing your homelab infrastructure:
- Quick access to services (Proxmox, TrueNAS, Pi-hole)
- Monitor server health and status
- Centralized documentation links
- System monitoring widgets

### 2. **Development Environment**
Organize development tools and resources:
- Git repositories (GitHub, GitLab)
- CI/CD pipelines (Jenkins, GitHub Actions)
- Documentation portals
- API testing tools

### 3. **Media Center Hub**
Central access point for media services:
- Plex, Jellyfin, Emby
- Sonarr, Radarr, Lidarr
- Download managers
- Media organization tools

### 4. **Business/Team Dashboard**
Team-wide access to business applications:
- Project management tools
- Communication platforms
- Cloud storage
- Analytics dashboards

### 5. **Personal Startpage**
Replace your browser's new tab page:
- Frequently visited sites
- Web search integration
- Quick bookmarks
- RSS feeds and news

### 6. **Network Management**
IT administration and network monitoring:
- Router/firewall interfaces
- Network monitoring tools
- Documentation wikis
- Device management portals

---

## Technology Stack

### Frontend
- **Framework**: Vue.js 2.7.0
- **State Management**: Vuex 3.6.2
- **Routing**: Vue Router 3.5.3
- **Styling**: SCSS/Sass
- **Icons**: 
  - Font Awesome
  - Simple Icons
  - Material Icons
  - Custom SVG support

### Backend
- **Runtime**: Node.js (16.0.0 or higher)
- **Server**: Express.js 4.17.2
- **API**: RESTful endpoints
- **Configuration**: js-yaml 4.1.0

### Build Tools
- **Build System**: Vue CLI 4.5.19 with Webpack
- **Package Manager**: Yarn (preferred) or NPM
- **Transpiler**: Babel
- **Linting**: ESLint with Airbnb style guide

### Additional Libraries
- **Authentication**: 
  - Keycloak-js 20.0.3
  - OIDC-client-ts 3.0.1
  - Express-basic-auth 1.2.1
- **HTTP Client**: Axios 1.12.0
- **Charts**: Frappe Charts 1.6.2
- **Configuration**: AJV 8.10.0 (JSON Schema validation)
- **Encryption**: Crypto-js 4.2.0

### Deployment
- **Containerization**: Docker + Docker Compose
- **Cloud Platforms**: 
  - Netlify
  - Vercel
  - Heroku
  - Railway
  - Google Cloud Run
- **Bare Metal**: Node.js server

---

## Architecture Overview

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        USER BROWSER                          │
│  ┌─────────────────────────────────────────────────────┐    │
│  │              Vue.js Single Page App                  │    │
│  │  ┌─────────┐  ┌──────────┐  ┌─────────────────┐    │    │
│  │  │  Views  │  │Components│  │  Vuex Store      │    │    │
│  │  └─────────┘  └──────────┘  └─────────────────┘    │    │
│  └─────────────────────────────────────────────────────┘    │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       │ HTTP/HTTPS
                       │
┌──────────────────────▼──────────────────────────────────────┐
│                   EXPRESS.JS SERVER                          │
│  ┌────────────────────────────────────────────────────┐     │
│  │              REST API Endpoints                     │     │
│  │  • /status-check  • /config-save  • /rebuild       │     │
│  │  • /system-info   • /cors-proxy   • /get-user      │     │
│  └────────────────────────────────────────────────────┘     │
│  ┌────────────────────────────────────────────────────┐     │
│  │            Middleware & Services                    │     │
│  │  • Authentication   • Config Validation             │     │
│  │  • SSL/TLS         • Static File Serving           │     │
│  └────────────────────────────────────────────────────┘     │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       │ File I/O
                       │
┌──────────────────────▼──────────────────────────────────────┐
│                   FILE SYSTEM                                │
│  ┌─────────────────┐  ┌─────────────────┐                   │
│  │  user-data/     │  │     dist/       │                   │
│  │  └─ conf.yml    │  │  (Built assets) │                   │
│  └─────────────────┘  └─────────────────┘                   │
└─────────────────────────────────────────────────────────────┘
```

### Application Flow

1. **Build Phase** (Development/Deployment):
   ```
   Source Code → Webpack/Vue CLI → Compiled Assets → dist/
   ```

2. **Runtime Phase**:
   ```
   User Request → Express Server → Static Files / API → Response
   ```

3. **Configuration Flow**:
   ```
   conf.yml → YAML Parser → Validation → Vue Store → UI Rendering
   ```

### Request Flow

```
1. Browser Request
   └─→ Express Server
       ├─→ Authentication Middleware (if enabled)
       ├─→ Route Handler
       │   ├─→ Static Files (HTML/CSS/JS)
       │   ├─→ API Endpoints
       │   └─→ Config Files (.yml)
       └─→ Response to Browser
```

---

## Directory Structure

### Root Directory Layout
```
dashy/
├── .devcontainer/          # VS Code dev container configuration
├── .github/                # GitHub workflows, issue templates
├── .vscode/                # VS Code workspace settings
├── docker/                 # Docker-specific configuration files
├── docs/                   # Complete documentation
├── public/                 # Static assets (copied to dist/)
├── services/               # Backend service modules
├── src/                    # Frontend source code
├── user-data/              # User configuration and custom files
├── Dockerfile              # Container build instructions
├── docker-compose.yml      # Docker Compose configuration
├── package.json            # Node.js dependencies and scripts
├── server.js               # Express.js server entry point
├── vue.config.js           # Vue CLI and Webpack configuration
├── tsconfig.json           # TypeScript configuration
└── yarn.lock               # Dependency lock file
```

### Services Directory (`/services/`)
Backend utilities and API handlers:
```
services/
├── config-validator.js     # Validates conf.yml against schema
├── cors-proxy.js           # Proxy for CORS-restricted APIs
├── get-user.js             # User authentication lookup
├── healthcheck.js          # Application health monitoring
├── print-message.js        # Startup message formatting
├── rebuild-app.js          # Triggers production rebuild
├── save-config.js          # Saves configuration to disk
├── ssl-server.js           # HTTPS/SSL support
├── status-check.js         # Service availability checking
├── system-info.js          # System metrics (CPU, RAM, etc.)
└── update-checker.js       # Checks for new Dashy versions
```

### Source Directory (`/src/`)
Frontend application code:
```
src/
├── App.vue                 # Root Vue component
├── main.js                 # Application entry point
├── router.js               # Vue Router configuration
├── store.js                # Vuex state management
├── assets/                 # Static assets
│   ├── fonts/              # Custom fonts
│   ├── locales/            # i18n translation files
│   └── interface-icons/    # SVG icons
├── components/             # Vue components (detailed below)
├── mixins/                 # Reusable component logic
├── styles/                 # Global SCSS stylesheets
├── utils/                  # Helper functions and utilities
└── views/                  # Main page components
```

---

## Component Architecture

### Component Hierarchy

```
App.vue
├── Router
    ├── Home.vue
    │   ├── Header
    │   │   ├── PageTitle
    │   │   ├── Nav
    │   │   └── Settings
    │   │       ├── SearchBar
    │   │       ├── ConfigLauncher
    │   │       ├── ThemeSelector
    │   │       └── LanguageSwitcher
    │   ├── ItemGroup (Section)
    │   │   └── Item (multiple)
    │   │       ├── ItemIcon
    │   │       ├── StatusIndicator
    │   │       └── ItemContextMenu
    │   └── Footer
    ├── Minimal.vue
    │   ├── MinimalHeading
    │   ├── MinimalSearch
    │   └── MinimalSection
    ├── Workspace.vue
    │   ├── SideBar
    │   │   └── SideBarSection
    │   │       └── SideBarItem
    │   └── WebContent
    └── Login.vue
```

### Key Component Groups

#### 1. **Page Structure** (`/components/PageStrcture/`)
- `Header.vue`: Top navigation bar
- `Footer.vue`: Bottom footer with links
- `Nav.vue`: Main navigation menu
- `PageTitle.vue`: Dashboard title and subtitle
- `LoadingScreen.vue`: Initial loading animation

#### 2. **Link Items** (`/components/LinkItems/`)
- `ItemGroup.vue`: Container for section items
- `Item.vue`: Individual application link
- `ItemIcon.vue`: Icon rendering (various formats)
- `StatusIndicator.vue`: Real-time status checking
- `ItemContextMenu.vue`: Right-click menu
- `IframeModal.vue`: Embedded app viewer

#### 3. **Settings** (`/components/Settings/`)
- `SettingsContainer.vue`: Main settings panel
- `SearchBar.vue`: Global search functionality
- `ThemeSelector.vue`: Theme switching
- `LanguageSwitcher.vue`: Language selection
- `ConfigLauncher.vue`: Opens config editor
- `CustomThemeMaker.vue`: Visual theme builder

#### 4. **Configuration** (`/components/Configuration/`)
- `ConfigContainer.vue`: Main config modal
- `JsonEditor.vue`: Raw config editing
- `AppInfoModal.vue`: Application information
- `CloudBackupRestore.vue`: Backup management
- `CustomCss.vue`: Custom CSS editor
- `EditSiteMeta.vue`: Metadata editor

#### 5. **Interactive Editor** (`/components/InteractiveEditor/`)
- `EditSection.vue`: Section editing form
- `EditItem.vue`: Item editing form
- `EditAppConfig.vue`: App config editing
- `EditPageInfo.vue`: Page info editing
- `EditModeSaveMenu.vue`: Save/cancel controls
- `MoveItemTo.vue`: Item moving/copying

#### 6. **Widgets** (`/components/Widgets/`)
Over 40+ specialized widgets for different services:
- System monitoring (Glances, Netdata)
- Network services (Pi-hole, AdGuard)
- Media (Sonarr, Radarr, Plex)
- Infrastructure (Proxmox, Portainer)
- Generic (Clock, Weather, RSS, Crypto)

#### 7. **Workspace View** (`/components/Workspace/`)
- `SideBar.vue`: Application sidebar
- `SideBarSection.vue`: Collapsible sections
- `SideBarItem.vue`: Sidebar app items
- `WebContent.vue`: Main iframe container
- `WidgetView.vue`: Widget display area

#### 8. **Minimal View** (`/components/MinimalView/`)
- `MinimalHeading.vue`: Simple page header
- `MinimalSearch.vue`: Streamlined search
- `MinimalSection.vue`: Tabbed sections

---

## Configuration System

### Configuration Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     conf.yml                             │
│  ┌────────────┐  ┌───────────┐  ┌──────────────┐       │
│  │ pageInfo   │  │ appConfig │  │  sections[]  │       │
│  └────────────┘  └───────────┘  └──────────────┘       │
└────────────┬────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────┐
│              YAML Parser (js-yaml)                       │
└────────────┬────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────┐
│           Schema Validator (AJV)                         │
│           (ConfigSchema.js)                              │
└────────────┬────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────┐
│              Vuex Store                                  │
│  • config    • modalOpen   • navigateConfToTab          │
└────────────┬────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────┐
│           Vue Components                                 │
│           (Props & Computed Properties)                  │
└─────────────────────────────────────────────────────────┘
```

### Configuration Structure

```yaml
# pageInfo - Basic page metadata
pageInfo:
  title: My Dashboard
  description: Self-hosted services
  navLinks:
    - title: GitHub
      path: https://github.com
  logo: /logo.png
  footerText: My custom footer

# appConfig - Application settings
appConfig:
  theme: colorful
  layout: auto
  iconSize: medium
  language: en
  startingView: default
  defaultOpeningMethod: newtab
  statusCheck: true
  statusCheckInterval: 300
  webSearch:
    searchEngine: duckduckgo
    openingMethod: newtab
  auth:
    users:
      - user: admin
        hash: [SHA-256 hash]
        type: admin
  
# sections - Dashboard sections and items
sections:
  - name: Development
    icon: fas fa-code
    displayData:
      collapsed: false
      rows: 2
    items:
      - title: GitHub
        description: Code repositories
        icon: fab fa-github
        url: https://github.com
        target: newtab
        tags: [code, git]
        statusCheck: true
        
# pages - Multi-page support
pages:
  - name: Media
    path: media.yml
  - name: Network
    path: network.yml
```

### Configuration Methods

1. **Direct YAML Editing**
   - Edit `user-data/conf.yml` directly
   - Full control over all options
   - Requires app rebuild

2. **UI JSON Editor**
   - Access via Config menu
   - Built-in validation
   - Live schema checking

3. **Visual Interactive Editor**
   - Click any element to edit
   - Live preview of changes
   - Saves to disk or browser

4. **Programmatic API**
   - POST to `/config-save` endpoint
   - Automated configuration
   - CI/CD integration

---

## Deployment Options

### 1. Docker (Recommended)

```bash
# Simple deployment
docker run -d \
  -p 8080:8080 \
  -v ~/dashy-config.yml:/app/user-data/conf.yml \
  -v ~/dashy-icons:/app/public/item-icons \
  --name dashy \
  --restart=always \
  lissy93/dashy:latest
```

**Docker Compose:**
```yaml
version: '3.8'
services:
  dashy:
    image: lissy93/dashy:latest
    container_name: dashy
    ports:
      - 8080:8080
    volumes:
      - ./conf.yml:/app/user-data/conf.yml
      - ./icons:/app/public/item-icons
    environment:
      - NODE_ENV=production
      - UID=1000
      - GID=1000
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "node", "/app/services/healthcheck"]
      interval: 5m
      timeout: 5s
      start_period: 30s
```

### 2. Bare Metal

```bash
# Prerequisites: Node.js 16+ and Yarn
git clone https://github.com/Lissy93/dashy.git
cd dashy
yarn install
yarn build
yarn start

# With PM2 (recommended for production)
yarn pm2-start
```

### 3. Cloud Platforms

**One-Click Deployments:**
- **Netlify**: Static hosting with CDN
- **Vercel**: Edge network deployment
- **Heroku**: Container-based hosting
- **Railway**: Modern cloud platform
- **Google Cloud Run**: Serverless containers

### 4. Kubernetes

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: dashy
spec:
  replicas: 2
  selector:
    matchLabels:
      app: dashy
  template:
    metadata:
      labels:
        app: dashy
    spec:
      containers:
      - name: dashy
        image: lissy93/dashy:latest
        ports:
        - containerPort: 8080
        volumeMounts:
        - name: config
          mountPath: /app/user-data
      volumes:
      - name: config
        configMap:
          name: dashy-config
```

---

## API Endpoints

### Backend REST API

| Endpoint | Method | Purpose | Authentication |
|----------|--------|---------|----------------|
| `/status-check/:url` | GET | Check if a service is online | Optional |
| `/config-save` | POST | Save configuration to disk | Required |
| `/rebuild` | GET | Trigger app rebuild | Required |
| `/system-info` | GET | Get system metrics | Optional |
| `/cors-proxy` | GET | Proxy CORS-blocked requests | Optional |
| `/get-user` | GET | Get current user info | Optional |
| `/*.yml` | GET | Serve config files | Optional |

### Status Check Endpoint

**Request:**
```
GET /status-check/https://example.com
```

**Response:**
```json
{
  "statusCode": 200,
  "statusText": "OK",
  "responseTime": 145,
  "online": true,
  "successStatus": true
}
```

### Config Save Endpoint

**Request:**
```
POST /config-save
Content-Type: application/json

{
  "config": {
    "pageInfo": {...},
    "sections": [...]
  }
}
```

**Response:**
```json
{
  "success": true,
  "message": "Config saved successfully"
}
```

### System Info Endpoint

**Request:**
```
GET /system-info
```

**Response:**
```json
{
  "cpu": {
    "percent": 23.5,
    "cores": 8
  },
  "memory": {
    "total": 16384,
    "used": 8192,
    "free": 8192
  },
  "disk": {...},
  "network": {...}
}
```

---

## Data Flow

### 1. Application Startup Flow

```
1. server.js executes
   ├─→ Load environment variables
   ├─→ Initialize Express app
   ├─→ Run update checker
   ├─→ Validate config file
   ├─→ Setup middleware
   │   ├─→ SSL redirect
   │   ├─→ JSON parser
   │   ├─→ Authentication
   │   └─→ Static file serving
   ├─→ Register API routes
   ├─→ Start HTTP server
   └─→ Start HTTPS server (if configured)

2. Browser loads index.html
   ├─→ Load Vue.js bundle
   ├─→ Initialize Vue app (main.js)
   ├─→ Setup Vue Router
   ├─→ Initialize Vuex store
   ├─→ Fetch config file
   ├─→ Apply theme
   ├─→ Render components
   └─→ Register service worker (PWA)
```

### 2. Config Loading Flow

```
User Changes Config
   ├─→ UI Edit Mode
   │   ├─→ Edit component opens
   │   ├─→ User makes changes
   │   ├─→ Validation runs
   │   ├─→ Preview updates (live)
   │   └─→ Save decision
   │       ├─→ Save Locally (localStorage)
   │       └─→ Save to Disk (POST /config-save)
   │
   └─→ Direct YAML Edit
       ├─→ Edit conf.yml
       ├─→ Run: yarn validate-config
       ├─→ Run: yarn build
       └─→ Restart server
```

### 3. Status Check Flow

```
Page Load / Interval Timer
   ├─→ For each item with statusCheck: true
   │   ├─→ GET /status-check/:url
   │   ├─→ Server makes HTTP request
   │   ├─→ Measure response time
   │   ├─→ Return status data
   │   └─→ Update UI indicator
   │       ├─→ Green: Online (200-299)
   │       ├─→ Yellow: Warning (300-399)
   │       ├─→ Red: Error (400+)
   │       └─→ Gray: Timeout/Unknown
   │
   └─→ Schedule next check (if interval set)
```

### 4. Widget Data Flow

```
Widget Component Mounts
   ├─→ Read widget config
   ├─→ Determine data source
   │   ├─→ Local API (via /cors-proxy)
   │   ├─→ Remote API (direct)
   │   └─→ System Info (via /system-info)
   ├─→ Fetch data
   ├─→ Transform data
   ├─→ Update component state
   ├─→ Render visualization
   └─→ Schedule refresh (if updateInterval set)
```

### 5. Authentication Flow

```
User Access Request
   ├─→ Check if auth enabled
   │   ├─→ No Auth
   │   │   └─→ Serve content
   │   │
   │   ├─→ Basic Auth
   │   │   ├─→ Check credentials
   │   │   ├─→ Verify against users array
   │   │   └─→ Grant/Deny access
   │   │
   │   └─→ Keycloak SSO
   │       ├─→ Redirect to Keycloak
   │       ├─→ User authenticates
   │       ├─→ Receive token
   │       ├─→ Validate token
   │       └─→ Load user-specific config
   │
   └─→ Apply access controls
       ├─→ Hide restricted sections
       ├─→ Show allowed items
       └─→ Enable/disable features
```

---

## Security Features

### 1. Authentication Methods

**Basic Authentication:**
- SHA-256 hashed passwords
- Multi-user support
- Role-based access (admin/user/guest)
- Token-based API access

**Keycloak SSO:**
- Industry-standard OpenID Connect
- Centralized user management
- Multi-factor authentication support
- Fine-grained access control

**Header Authentication:**
- Proxy-based authentication
- Integration with reverse proxies
- Custom header validation

### 2. Configuration Security

- **Schema Validation**: All configs validated against JSON schema
- **Input Sanitization**: XSS prevention in user inputs
- **YAML Safe Loading**: Prevents code injection
- **File Access Control**: Limited to user-data directory

### 3. Network Security

- **CORS Proxy**: Controlled access to external APIs
- **SSL/TLS Support**: HTTPS encryption
- **Content Security Policy**: XSS protection headers
- **Subresource Integrity**: Verified resource loading

### 4. Data Privacy

- **End-to-End Encryption**: Cloud backups encrypted client-side
- **No Telemetry**: Zero tracking or analytics
- **Local Storage**: All data stays on your server
- **Privacy-First**: GDPR compliant by design

### 5. Container Security

- **Non-Root User**: Runs as unprivileged user
- **Health Checks**: Automatic container monitoring
- **Read-Only Filesystem**: Where possible
- **Minimal Base Image**: Alpine Linux for reduced attack surface

---

## Performance Characteristics

### Build Performance
- **Build Time**: 1-3 minutes (depending on platform)
- **Bundle Size**: ~2.5 MB (gzipped)
- **Cold Start**: <5 seconds
- **Hot Reload**: <1 second (dev mode)

### Runtime Performance
- **Memory Usage**: 100-300 MB
- **CPU Usage**: <5% idle, <20% active
- **Concurrent Users**: 50+ (single instance)
- **Response Time**: <100ms (static content)

### Optimization Features
- **Code Splitting**: Lazy-loaded routes
- **Tree Shaking**: Unused code removal
- **Asset Caching**: Browser and CDN caching
- **Image Optimization**: On-demand icon loading
- **Service Worker**: Offline functionality

---

## Development Workflow

### Local Development Setup
```bash
# 1. Clone repository
git clone https://github.com/Lissy93/dashy.git
cd dashy

# 2. Install dependencies
yarn install

# 3. Start dev server (hot reload enabled)
yarn dev

# 4. Access at http://localhost:8080
```

### Available Commands
```bash
yarn dev              # Start development server
yarn build            # Build for production
yarn start            # Start production server
yarn lint             # Run code linting
yarn validate-config  # Validate conf.yml
yarn health-check     # Check app health
yarn pm2-start        # Start with PM2
```

### Code Style
- **Linting**: ESLint with Airbnb/Vue.js styleguide
- **Formatting**: 2-space indentation, single quotes
- **Pre-commit Hooks**: Automatic linting
- **Component Style**: Vue Single File Components (.vue)

---

## Extensibility

### Adding Custom Widgets
```javascript
// src/components/Widgets/MyCustomWidget.vue
<template>
  <div class="my-widget">
    <p>{{ data }}</p>
  </div>
</template>

<script>
import WidgetMixin from '@/mixins/WidgetMixin';

export default {
  mixins: [WidgetMixin],
  data() {
    return {
      data: null,
    };
  },
  methods: {
    fetchData() {
      this.makeRequest(this.endpoint)
        .then(this.processData);
    },
  },
};
</script>
```

### Custom Themes
```scss
// src/styles/user-defined-themes.scss
.theme-my-custom {
  --primary: #ff6b6b;
  --background: #1a1a1a;
  --item-background: #2d2d2d;
  --item-text: #ffffff;
}
```

### Custom Icons
```yaml
sections:
  - name: My Section
    icon: /local-icons/my-icon.png  # Local icon
    items:
      - title: My App
        icon: https://example.com/icon.png  # Remote icon
```

---

## Monitoring and Observability

### Health Checks
```bash
# Manual health check
yarn health-check

# Docker health check (automatic)
HEALTHCHECK --interval=5m --timeout=5s \
  CMD node /app/services/healthcheck
```

### Logging
- **Server Logs**: Console output (stdout/stderr)
- **Access Logs**: Express.js logging
- **Error Tracking**: Optional Sentry integration
- **Browser Console**: Development mode debugging

### Metrics
- **Status Indicators**: Per-service uptime
- **System Info Widget**: CPU, RAM, disk usage
- **Response Times**: Via status checks
- **Build Performance**: Webpack stats

---

## Common Patterns and Best Practices

### Configuration Management
1. **Keep backups**: Use cloud backup or version control
2. **Use anchors**: Reuse YAML blocks with `&anchor` and `*alias`
3. **Validate frequently**: Run `yarn validate-config`
4. **Start simple**: Begin with minimal config, expand gradually

### Performance Optimization
1. **Disable unused features**: Hide components in appConfig
2. **Optimize images**: Resize icons to appropriate size
3. **Limit status checks**: Only enable for critical services
4. **Use local icons**: Faster than fetching from web

### Security Hardening
1. **Enable authentication**: Even on private networks
2. **Use HTTPS**: Always in production
3. **Regular updates**: Keep Dashy and dependencies current
4. **Limit access**: Use firewall rules or VPN

### Maintenance
1. **Monitor health**: Regular health checks
2. **Check logs**: Review for errors or warnings
3. **Update configs**: Keep documentation current
4. **Test changes**: Validate before production deployment

---

## Troubleshooting Guide

### Common Issues

**Config not loading:**
- Check YAML syntax: `yarn validate-config`
- Verify file path: `/app/user-data/conf.yml`
- Check file permissions

**Status checks failing:**
- Verify URL accessibility from server
- Check CORS settings
- Increase timeout values

**Icons not displaying:**
- Verify icon format (Font Awesome, URL, local)
- Check network connectivity
- Review browser console for errors

**Build failures:**
- Clear cache: `rm -rf node_modules && yarn install`
- Check Node.js version (16+)
- Verify disk space available

**Authentication issues:**
- Verify password hash (SHA-256)
- Check auth configuration syntax
- Review server logs for details

---

## Resources and Links

### Official Documentation
- **GitHub Repository**: https://github.com/Lissy93/dashy
- **Documentation**: https://dashy.to/docs
- **Live Demo**: https://demo.dashy.to

### Community
- **Discussions**: https://github.com/Lissy93/dashy/discussions
- **Issues**: https://github.com/Lissy93/dashy/issues
- **Showcase**: https://github.com/Lissy93/dashy/blob/master/docs/showcase.md

### Related Projects
- **Homer**: https://github.com/bastienwirtz/homer
- **Heimdall**: https://github.com/linuxserver/Heimdall
- **Organizr**: https://organizr.app/

---

## Conclusion

Dashy is a comprehensive, feature-rich dashboard solution for organizing and accessing your self-hosted services. Its architecture is built on modern web technologies (Vue.js, Express.js, Node.js) with a focus on:

- **Flexibility**: Extensive configuration options
- **Performance**: Fast loading and responsive UI
- **Security**: Multiple authentication methods
- **Privacy**: Self-hosted with no external dependencies
- **Extensibility**: Easy to customize and extend

Whether you're managing a homelab, development environment, or business infrastructure, Dashy provides the tools and flexibility needed to create the perfect dashboard for your needs.

---

**Last Updated**: December 2024  
**Dashy Version**: 3.1.1  
**License**: MIT
