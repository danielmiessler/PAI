# PAI Quick Start Guide

Get your Personal AI Infrastructure up and running in minutes!

## Prerequisites

- **macOS** 11+ (primary platform)
- **AI Assistant** (Claude, GPT, Gemini, etc.)
- **Bun runtime** (for voice server)
- **Git** (for version control)

## Installation

### 1. Clone or Create PAI Directory

```bash
# Option A: Clone from repository
git clone https://github.com/yourusername/PAI.git
cd PAI

# Option B: Create new PAI installation
mkdir -p ~/PAI
cd ~/PAI
```

### 2. Set Environment Variables

```bash
# Add to your shell profile (~/.zshrc or ~/.bashrc)
export PAI_DIR="$HOME/PAI/PAI_DIRECTORY"  # PAI infrastructure directory
export PATH="$HOME/bin:$PATH"

# Reload shell
source ~/.zshrc  # or ~/.bashrc
```

### 3. Create Directory Structure

```bash
# Create essential directories
mkdir -p "${PAI_DIR}/context"
mkdir -p "${PAI_DIR}/hooks"
mkdir -p "${PAI_DIR}/commands"
mkdir -p "$HOME/Projects"
mkdir -p "$HOME/Library/Logs"
mkdir -p "$HOME/Documentation"
```

### 4. Configure Environment File

Create `${PAI_DIR}/.env` with your settings:

```bash
# Essential Configuration
PAI_DIR=$HOME/PAI/PAI_DIRECTORY
PAI_HOME=$HOME

# Optional: Voice Server
PORT=8888

# Optional: Digital Assistant Customization
DA="YourAssistantName"    # Defaults to "Assistant"
DA_COLOR="purple"         # Choose: purple, blue, green, cyan, magenta, yellow, red, orange

# Optional: API Keys for various services
OPENAI_API_KEY=your_key_here
ANTHROPIC_API_KEY=your_key_here
```

## Core Setup

### 1. Create Main Context File

Create `${PAI_DIR}/context/CLAUDE.md`:

```markdown
# PAI System Context

## System Information
- PAI_DIR: ${PAI_DIR}
- Platform: macOS
- User: ${USER}

## Core Instructions
You are an AI assistant enhanced with PAI (Personal AI Infrastructure).

## Available Features
- Dynamic context loading
- Hook system for automation
- Voice notifications
- Multi-agent support

## Project Contexts
[Your project-specific information here]
```

### 2. Setup UFC Hook System

Create the main hook file `${PAI_DIR}/hooks/user-prompt-submit-hook`:

```bash
#!/bin/bash
# UFC Dynamic Context Loader

PROMPT="$1"
PAI_DIR="${PAI_DIR:-$HOME/PAI/PAI_DIRECTORY}"

# Simple intent matching for demonstration
case "$PROMPT" in
    *website*|*blog*)
        echo "Loading website context..."
        cat "${PAI_DIR}/context/projects/website/CLAUDE.md" 2>/dev/null
        ;;
    *research*)
        echo "AGENT: researcher"
        ;;
    *security*|*pentest*)
        echo "AGENT: pentester"
        ;;
esac

exit 0
```

Make it executable:
```bash
chmod +x "${PAI_DIR}/hooks/user-prompt-submit-hook"
```

### 3. Install Voice Server (Optional)

For voice notifications, you'll need to:
1. Download macOS Premium/Enhanced voices (System Settings → Voice)
2. Start the voice server

```bash
# Navigate to voice server
cd "${PAI_DIR}/voice-server"

# Start the server (runs in background)
bun server.ts &

# Test voice server
curl -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "PAI system initialized", "voice_name": "Jamie (Premium)"}'
```

See [Voice Setup Guide](./VOICE-SETUP-GUIDE.md) for detailed instructions.

## Basic Usage

### 1. Context Management

Create project-specific contexts:

```bash
# Create a project context
mkdir -p "${PAI_DIR}/context/projects/myproject"
cat > "${PAI_DIR}/context/projects/myproject/CLAUDE.md" << EOF
# My Project Context

## Project Details
- Name: My Project
- Path: ${HOME}/Projects/myproject
- Type: Web Application

## Technical Stack
- Frontend: React
- Backend: Node.js
- Database: PostgreSQL

## Current Tasks
- [ ] Implement user authentication
- [ ] Add dashboard features
EOF
```

### 2. Hook Examples

#### Tool Validation Hook

Create `${PAI_DIR}/hooks/tool-use-hook`:

```bash
#!/bin/bash
# Validate tool usage

TOOL="$1"
PARAMS="$2"

# Log tool usage
echo "[$(date)] Tool: $TOOL" >> "${HOME}/Library/Logs/tools.log"

# Validate dangerous operations
if [[ "$TOOL" == "Bash" ]] && [[ "$PARAMS" =~ "rm -rf" ]]; then
    echo "BLOCKED: Dangerous command"
    exit 1
fi

exit 0
```

#### Notification Hook

Create `${PAI_DIR}/hooks/post-execution-hook`:

```bash
#!/bin/bash
# Send completion notifications

COMMAND="$1"
STATUS="$2"

if [ "$STATUS" -eq 0 ]; then
    curl -X POST http://localhost:8888/notify \
        -d '{"message": "Task completed successfully"}' \
        2>/dev/null
fi

exit 0
```

### 3. Custom Commands

Create custom command `${PAI_DIR}/commands/status.sh`:

```bash
#!/bin/bash
# Show PAI system status

echo "PAI System Status"
echo "================="
echo "PAI_DIR: ${PAI_DIR}"
echo "Contexts: $(find ${PAI_DIR}/context -name "*.md" | wc -l)"
echo "Hooks: $(find ${PAI_DIR}/hooks -type f | wc -l)"
echo "Projects: $(ls -1 ${HOME}/Projects 2>/dev/null | wc -l)"

# Check voice server
if curl -s http://localhost:8888/health > /dev/null 2>&1; then
    echo "Voice Server: ✅ Running"
else
    echo "Voice Server: ❌ Stopped"
fi
```

## Testing Your Installation

### 1. Test Context Loading

In Claude, try:
```
"Help me with my website"
# Should load website context

"Research AI trends"
# Should launch researcher agent
```

### 2. Test Voice Server

```bash
# Send test notification
curl -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Hello from PAI"}'
```

### 3. Test Hooks

```bash
# Test hook directly
${PAI_DIR}/hooks/user-prompt-submit-hook "test website"

# Check output
echo $?  # Should be 0
```

## Common Tasks

### Adding a New Project Context

```bash
# 1. Create project directory
mkdir -p "${HOME}/Projects/newproject"

# 2. Create context file
cat > "${PAI_DIR}/context/projects/newproject/CLAUDE.md" << EOF
# New Project Context
[Project specific information]
EOF

# 3. Add to hook system (optional)
# Edit user-prompt-submit-hook to include new project triggers
```

### Creating Agent-Specific Contexts

```bash
# Research agent context
cat > "${PAI_DIR}/context/agents/researcher.md" << EOF
# Researcher Agent Context
Focus on finding accurate, recent information
Cite sources when possible
EOF
```

### Setting Up Automation

```bash
# Create automation hook
cat > "${PAI_DIR}/hooks/automation-hook" << EOF
#!/bin/bash
# Automated tasks
if [[ "\$1" =~ "daily report" ]]; then
    generate_daily_report
fi
EOF
chmod +x "${PAI_DIR}/hooks/automation-hook"
```

## Troubleshooting

### Context Not Loading

```bash
# Check hook permissions
ls -la "${PAI_DIR}/hooks/"

# Test hook manually
"${PAI_DIR}/hooks/user-prompt-submit-hook" "test prompt"

# Check PAI_DIR is set
echo $PAI_DIR
```

### Voice Server Issues

```bash
# Check if running
lsof -i :8888

# View logs
tail -f "${HOME}/Library/Logs/pai-voice-server.log"

# Restart service
cd "${PAI_DIR}/voice-server"
./restart.sh
```

### Hook Not Executing

```bash
# Check if executable
chmod +x "${PAI_DIR}/hooks/"*

# Enable debug mode
export HOOK_DEBUG=true

# Check logs
tail -f "${HOME}/Library/Logs/hooks.log"
```

## Next Steps

1. **Explore Documentation**
   - [System Architecture](./architecture.md)
   - [UFC Context System](./ufc-context-system.md)
   - [Hook System](./hook-system.md)

2. **Customize Your Setup**
   - Add project-specific contexts
   - Create custom hooks
   - Configure voice personalities

3. **Advanced Features**
   - Set up multiple agents
   - Create command shortcuts
   - Integrate with external services

## Quick Reference

### Essential Commands

```bash
# Check system status
"${PAI_DIR}/commands/status.sh"

# Reload context
source ~/.zshrc

# Test voice
curl -X POST http://localhost:8888/notify -d '{"message":"test"}'

# View logs
tail -f "${HOME}/Library/Logs/"*.log
```

### File Locations

| Component | Location |
|-----------|----------|
| Main Context | `${PAI_DIR}/context/CLAUDE.md` |
| Hooks | `${PAI_DIR}/hooks/` |
| Commands | `${PAI_DIR}/commands/` |
| Projects | `${HOME}/Projects/` |
| Logs | `${HOME}/Library/Logs/` |
| Voice Server | `${PAI_DIR}/voice-server/` |

### Environment Variables

| Variable | Purpose | Default |
|----------|---------|---------|
| `PAI_DIR` | PAI configuration directory | `$HOME/PAI/PAI_DIRECTORY` |
| `PAI_HOME` | Your home directory | `$HOME` |
| `PORT` | Voice server port | 8888 |
| `DA` | Digital Assistant name | "Assistant" |
| `DA_COLOR` | Display color | "purple" |
| `HOOK_DEBUG` | Enable hook debugging | false |

## Getting Help

- Check the [Documentation](./README.md)
- Review [Troubleshooting Guide](#troubleshooting)
- File issues on GitHub
- Check logs in `${HOME}/Library/Logs/`

---

*Welcome to PAI! Your personal AI infrastructure is ready to enhance your workflow.*