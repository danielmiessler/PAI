# PAI System Documentation

Welcome to the Personal AI Infrastructure (PAI) documentation. PAI is a comprehensive system for integrating AI assistants into your personal workflow with advanced context management, automation, and extensibility.

## 📚 Documentation Index

### Getting Started
- [Quick Start Guide](./quick-start.md) - Get up and running in minutes
- [Installation Guide](./installation.md) - Detailed installation instructions
- [Configuration Guide](./configuration.md) - System configuration options

### Core Concepts
- [System Architecture](./architecture.md) - Overview of PAI components
- [UFC Context System](./ufc-context-system.md) - Universal Flexible Context management
- [Hook System](./hook-system.md) - Event-driven automation
- [Agent System](./agent-system.md) - Specialized AI agents

### Components
- [Voice Server](../voice-server/README.md) - Voice notification system
- [Context Management](./context-management.md) - Dynamic context loading
- [Command System](./command-system.md) - Custom commands and scripts

### Development
- [API Reference](./api-reference.md) - HTTP APIs and interfaces
- [Security Guide](./security.md) - Security best practices
- [Contributing](./contributing.md) - How to contribute to PAI

## 🚀 What is PAI?

PAI (Personal AI Infrastructure) is a powerful framework that enhances AI assistants with:

- **Dynamic Context Loading**: Automatically loads relevant context based on conversation intent
- **Universal Flexible Context (UFC)**: Intelligent context management system
- **Hook System**: Event-driven automation for tool calls
- **Voice Notifications**: AI-powered voice feedback
- **Multi-Agent Architecture**: Specialized agents for different tasks
- **Security First**: Built with security best practices

## 🎯 Key Features

### 1. Context Intelligence
- Semantic understanding of user intent
- Automatic context loading
- Project-specific knowledge bases
- Dynamic agent selection

### 2. Automation
- Pre and post-execution hooks
- Custom command integration
- Workflow automation
- Event-driven responses

### 3. Voice Integration
- ElevenLabs AI voices
- macOS fallback support
- Multiple voice personalities
- Real-time notifications

### 4. Security
- Input validation and sanitization
- Rate limiting
- CORS protection
- No hardcoded secrets

## 🏗️ System Components

```
PAI/
├── .claude/                 # Claude-specific configuration
│   ├── context/            # UFC context files
│   ├── hooks/              # Event hooks
│   ├── commands/           # Custom commands
│   └── voice-server/       # Voice notification server
├── Documentation/          # System documentation
├── Projects/               # Project-specific contexts
└── Library/               # System libraries and logs
```

## 🔧 Environment Variables

PAI uses environment variables for configuration:

- `PAI_HOME`: Base directory for PAI installation
- `CLAUDE_CONFIG_DIR`: Claude configuration directory
- `ELEVENLABS_API_KEY`: API key for voice synthesis
- `PORT`: Voice server port (default: 8888)

## 📖 Quick Links

- [System Requirements](#system-requirements)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage Examples](#usage-examples)
- [Troubleshooting](#troubleshooting)

## System Requirements

- macOS 11+ (primary support)
- Bun runtime
- Claude Desktop or API access
- Optional: ElevenLabs API key
- Optional: SwiftBar for menu indicators

## Installation

```bash
# Clone PAI repository
git clone https://github.com/yourusername/PAI.git
cd PAI

# Set PAI_HOME
export PAI_HOME="$(pwd)"

# Install voice server (optional)
cd .claude/voice-server
./install.sh

# Configure environment
cp .env.example ~/.env
# Edit ~/.env with your settings
```

## Configuration

PAI is configured through:
1. Environment variables in `~/.env`
2. Context files in `.claude/context/`
3. Hook scripts in `.claude/hooks/`
4. Project-specific configurations

## Usage Examples

### Basic Context Loading
```bash
# Context automatically loads based on conversation
"Help me with my website" → Loads website context
"Research AI trends" → Loads research agent
```

### Voice Notifications
```bash
# Send voice notification
curl -X POST http://localhost:8888/notify \
  -d '{"message": "Task completed"}'
```

### Hook System
```yaml
# .claude/hooks/user-prompt-submit.sh
# Automatically loads context before processing prompts
```

## Troubleshooting

Common issues and solutions:

| Issue | Solution |
|-------|----------|
| Context not loading | Check `${PAI_HOME}/.claude/context/` |
| Voice not working | Verify ElevenLabs API key in `~/.env` |
| Hooks not triggering | Ensure hook scripts are executable |
| Port conflicts | Change PORT in `~/.env` |

## Contributing

PAI is open for contributions. See [Contributing Guide](./contributing.md) for:
- Code style guidelines
- Pull request process
- Issue reporting
- Feature requests

## Support

- GitHub Issues: Report bugs and request features
- Documentation: This directory contains all documentation
- Community: Join discussions in the repository

## License

PAI is part of the Personal AI Infrastructure project.

---

*Last updated: [Current Date]*
*Version: 1.0.0*