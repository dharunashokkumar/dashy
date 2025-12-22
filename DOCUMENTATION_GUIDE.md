# 📚 Dashy Documentation Guide

Welcome! This repository contains comprehensive documentation about **Dashy** - a self-hosted dashboard for organizing your web services.

## 🎯 What You'll Find Here

This repository provides complete information about Dashy's purpose, features, and architecture. Choose the documentation that best fits your needs:

### 📖 Documentation Files

| File | Best For | Content |
|------|----------|---------|
| **[QUICK_REFERENCE.md](./QUICK_REFERENCE.md)** | Getting started quickly | 30-second setup, essential features, quick examples |
| **[ARCHITECTURE.md](./ARCHITECTURE.md)** | Understanding the system | Complete technical details, architecture, data flows |
| **[README.md](./README.md)** | Feature overview | Main project information, features, links |
| **[docs/](./docs/)** | Specific topics | Detailed guides on configuration, deployment, widgets, etc. |

## 🚀 Start Here

### New to Dashy? 
👉 Start with **[QUICK_REFERENCE.md](./QUICK_REFERENCE.md)**
- Get Dashy running in 30 seconds
- Understand core features
- See practical examples

### Need Technical Details?
👉 Read **[ARCHITECTURE.md](./ARCHITECTURE.md)**
- Full technology stack
- Architecture diagrams
- Component structure
- API documentation
- Data flow explanations

### Want Specific Guides?
👉 Browse **[docs/](./docs/)**
- Configuration options
- Widget setup
- Theme customization
- Authentication setup
- Deployment guides

## 📋 Quick Overview

### What is Dashy?

Dashy is a **self-hosted dashboard application** that provides:
- 🎯 Single place to access all your services
- 🎨 Highly customizable interface
- 🔍 Instant search and shortcuts
- 🚦 Real-time service monitoring
- 📊 Dynamic widgets for live data
- 🔐 Built-in authentication
- 🌍 Multi-language support (25+ languages)
- ☁️ Cloud backup & sync

### Key Features Summary

1. **Multi-Page Dashboards** - Organize services across unlimited pages
2. **Status Monitoring** - Real-time health checks for your services
3. **40+ Widgets** - Display live data from self-hosted apps
4. **Advanced Search** - Find services instantly with keyboard shortcuts
5. **20+ Themes** - Built-in themes + custom CSS support
6. **Multiple Views** - Default, Workspace, and Minimal layouts
7. **Authentication** - Basic auth + SSO (Keycloak)
8. **PWA Support** - Install as standalone app
9. **Cloud Sync** - Encrypted backup and restore
10. **Highly Configurable** - YAML-based configuration

### Technology Stack

- **Frontend**: Vue.js 2.7, Vuex, Vue Router
- **Backend**: Node.js, Express.js
- **Configuration**: YAML
- **Deployment**: Docker, Bare Metal, Cloud (Netlify, Vercel, etc.)
- **License**: MIT

## 🏗️ Architecture Summary

```
User Browser (Vue.js SPA)
        ↓
Express.js Server
        ↓
Configuration (conf.yml)
        ↓
Your Services
```

### Directory Structure
```
dashy/
├── ARCHITECTURE.md       # Complete technical documentation
├── QUICK_REFERENCE.md    # Quick start guide
├── README.md             # Main project readme
├── src/                  # Vue.js frontend source
│   ├── components/       # UI components
│   ├── views/            # Main pages
│   └── utils/            # Helper functions
├── services/             # Backend API handlers
├── user-data/            # Your configuration files
│   └── conf.yml          # Main config
├── docs/                 # Detailed documentation
└── server.js             # Express server entry point
```

## 🎓 Learning Path

### 1️⃣ First Time Setup (5 minutes)
```bash
# Quick start with Docker
docker run -p 8080:8080 lissy93/dashy

# Open http://localhost:8080
```

📖 Follow: [QUICK_REFERENCE.md § Quick Start](./QUICK_REFERENCE.md#-quick-start-30-seconds)

### 2️⃣ Basic Configuration (10 minutes)
- Learn YAML configuration basics
- Add your first services
- Choose a theme

📖 Follow: [QUICK_REFERENCE.md § Configuration Basics](./QUICK_REFERENCE.md#️-configuration-basics)

### 3️⃣ Explore Features (30 minutes)
- Try different view modes
- Add status checks
- Setup search and shortcuts
- Explore widgets

📖 Follow: [docs/configuring.md](./docs/configuring.md)

### 4️⃣ Customize & Secure (30 minutes)
- Apply custom themes
- Add authentication
- Configure multi-page setup
- Setup cloud backup

📖 Follow: [docs/](./docs/)

### 5️⃣ Advanced Usage (60 minutes)
- Understand the architecture
- Explore component structure
- Learn data flows
- Review API endpoints

📖 Follow: [ARCHITECTURE.md](./ARCHITECTURE.md)

## 🔍 Finding What You Need

### By Topic

**Setup & Deployment**
- Quick Start → [QUICK_REFERENCE.md](./QUICK_REFERENCE.md#-quick-start-30-seconds)
- Docker Setup → [QUICK_REFERENCE.md](./QUICK_REFERENCE.md#-docker-tips)
- Full Deployment Guide → [docs/deployment.md](./docs/deployment.md)
- Deployment Architecture → [ARCHITECTURE.md](./ARCHITECTURE.md#deployment-options)

**Configuration**
- Basic Config → [QUICK_REFERENCE.md](./QUICK_REFERENCE.md#️-configuration-basics)
- Complete Options → [docs/configuring.md](./docs/configuring.md)
- Config System → [ARCHITECTURE.md](./ARCHITECTURE.md#configuration-system)

**Features**
- Feature Overview → [README.md](./README.md#features-)
- Feature Details → [ARCHITECTURE.md](./ARCHITECTURE.md#key-features)
- Widgets → [docs/widgets.md](./docs/widgets.md)
- Theming → [docs/theming.md](./docs/theming.md)

**Architecture & Development**
- Tech Stack → [ARCHITECTURE.md](./ARCHITECTURE.md#technology-stack)
- Architecture → [ARCHITECTURE.md](./ARCHITECTURE.md#architecture-overview)
- Component Structure → [ARCHITECTURE.md](./ARCHITECTURE.md#component-architecture)
- Development → [docs/developing.md](./docs/developing.md)

**Troubleshooting**
- Quick Fixes → [QUICK_REFERENCE.md](./QUICK_REFERENCE.md#-quick-troubleshooting)
- Full Guide → [docs/troubleshooting.md](./docs/troubleshooting.md)

## 💡 Common Questions

### "How do I get started?"
→ See [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) - You'll be up and running in 30 seconds

### "What can Dashy do?"
→ See [README.md § Features](./README.md#features-) or [ARCHITECTURE.md § Key Features](./ARCHITECTURE.md#key-features)

### "How does it work?"
→ See [ARCHITECTURE.md § Architecture Overview](./ARCHITECTURE.md#architecture-overview)

### "How do I configure it?"
→ See [QUICK_REFERENCE.md § Configuration](./QUICK_REFERENCE.md#️-configuration-basics) for basics, [docs/configuring.md](./docs/configuring.md) for complete options

### "Can I use it for [specific use case]?"
→ See [ARCHITECTURE.md § Use Cases](./ARCHITECTURE.md#use-cases)

### "Is it secure?"
→ See [ARCHITECTURE.md § Security Features](./ARCHITECTURE.md#security-features)

### "How do I customize it?"
→ See [QUICK_REFERENCE.md § Customization](./QUICK_REFERENCE.md#-customization-quick-reference) or [docs/theming.md](./docs/theming.md)

## 🔗 External Resources

- **Live Demo**: https://demo.dashy.to
- **Official Site**: https://dashy.to
- **GitHub**: https://github.com/Lissy93/dashy
- **Docker Hub**: https://hub.docker.com/r/lissy93/dashy
- **Discussions**: https://github.com/Lissy93/dashy/discussions

## 📊 Documentation Statistics

- **Total Documentation**: 1,500+ lines
- **Main Documents**: 3 files
- **Detailed Guides**: 20+ files in docs/
- **Code Examples**: 50+ throughout documentation
- **Architecture Diagrams**: 10+ in ARCHITECTURE.md

## 🎯 Documentation Goals

This documentation aims to:
- ✅ Help you understand what Dashy is
- ✅ Get you started quickly
- ✅ Explain all features comprehensively
- ✅ Provide complete technical details
- ✅ Support different learning styles
- ✅ Answer common questions
- ✅ Enable self-service problem-solving

## 🤝 Contributing to Documentation

Found something missing or unclear?
- Open an issue: https://github.com/Lissy93/dashy/issues
- Start a discussion: https://github.com/Lissy93/dashy/discussions
- Submit a PR with improvements

## 📝 License

This documentation is part of the Dashy project.

- **License**: MIT
- **Copyright**: © 2021-2024 Alicia Sykes
- **More Info**: See [LICENSE](./LICENSE)

---

## 🚀 Ready to Start?

1. **Quick Start** → [QUICK_REFERENCE.md](./QUICK_REFERENCE.md)
2. **Full Details** → [ARCHITECTURE.md](./ARCHITECTURE.md)
3. **Main README** → [README.md](./README.md)

**Need Help?**
- 💬 [GitHub Discussions](https://github.com/Lissy93/dashy/discussions)
- 🐛 [Report Issues](https://github.com/Lissy93/dashy/issues)
- 📚 [Browse Docs](./docs/)

---

**Documentation Version**: 1.0  
**Last Updated**: December 2024  
**Dashy Version**: 3.1.1
