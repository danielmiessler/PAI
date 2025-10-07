# Contributing to PAI

Thank you for your interest in contributing to PAI (Personal AI Infrastructure)! This document provides guidelines for contributing to the project.

## 🎯 Mission

PAI's core mission is to **augment humans with AI capabilities so they can survive and thrive in a world full of AI**. We're building an open-source, personal AI platform that's accessible to everyone on Earth—not just the tech elite.

## 📋 How to Contribute

### Reporting Issues

Before creating an issue, please:
1. Check if a similar issue already exists
2. Use the issue templates if available
3. Provide clear, detailed information including:
   - Steps to reproduce (for bugs)
   - Expected vs actual behavior
   - Your environment (OS, PAI version, etc.)
   - Relevant logs or error messages

### Suggesting Enhancements

We welcome feature suggestions! Please:
1. Search existing issues to avoid duplicates
2. Clearly describe the use case and benefit
3. Consider if the feature aligns with PAI's mission of universal accessibility
4. Provide examples of how it would work

### Documentation Improvements

Documentation is critical for accessibility. You can help by:
- Fixing typos and clarifying unclear sections
- Adding examples and use cases
- Updating outdated information
- Improving organization and navigation
- Translating documentation (future goal)

**Important:** When editing documentation:
- Use `${PAI_DIR}` for path references, not hardcoded paths
- Keep the main README concise and link to detailed docs in `/PAI_DIRECTORY/documentation/`
- Update both locations if content is duplicated (or better, eliminate duplication)

### Code Contributions

#### Before You Start

1. **Fork the repository** and create a feature branch
2. **Check existing PRs** to avoid duplicate work
3. **Discuss major changes** in an issue first
4. **Follow the coding style** of the existing codebase

#### Development Guidelines

**Path Portability:**
- Always use `${PAI_DIR}` environment variable for PAI directory references
- Never hardcode absolute paths like `/Users/username/` or `~/.claude/`
- Test your changes with PAI_DIR set to different locations

**Platform Compatibility:**
- Primary platform is macOS, but consider cross-platform compatibility
- Document any platform-specific requirements
- Test on different shell environments (zsh, bash) when relevant

**Code Quality:**
- Write clear, self-documenting code
- Add comments for complex logic
- Include error handling and validation
- Test your changes thoroughly

**Security:**
- Never commit API keys, tokens, or sensitive data
- Use environment variables for configuration
- Follow the security guidelines in SECURITY.md
- Be mindful of command injection and path traversal risks in hooks

#### TypeScript/JavaScript (for hooks, servers, etc.)
- Use TypeScript when possible
- Follow existing formatting conventions
- Handle errors gracefully
- Validate inputs

#### Shell Scripts (for hooks, commands)
- Use `#!/bin/bash` or `#!/bin/zsh` shebang
- Include error handling (`set -e` when appropriate)
- Use shellcheck for validation
- Document any non-obvious bash features

#### Documentation Files
- Use Markdown format
- Follow existing structure and formatting
- Include code examples with syntax highlighting
- Keep line length reasonable (80-100 chars when possible)

### Pull Request Process

1. **Update documentation** if you're changing functionality
2. **Test thoroughly** in your local PAI installation
3. **Follow commit message conventions:**
   - Use clear, descriptive commit messages
   - Reference issue numbers (e.g., "Fix #23: Update documentation paths")
   - Use imperative mood ("Add feature" not "Added feature")

4. **PR Description should include:**
   - What changes you made and why
   - How to test the changes
   - Any breaking changes or migration notes
   - Screenshots/demos if relevant

5. **Be responsive** to review feedback
6. **Keep PRs focused** - one feature/fix per PR when possible

## 🏗️ Project Structure

Understanding the structure helps you contribute effectively:

```
PAI/
├── README.md                    # Main entry point (keep concise!)
├── PAI_DIRECTORY/              # Core PAI system
│   ├── documentation/          # Detailed documentation (source of truth)
│   ├── context/               # UFC context files
│   ├── hooks/                 # Event hooks
│   ├── commands/              # Custom commands
│   └── voice-server/          # Voice notification server
└── SECURITY.md                # Security guidelines
```

**Documentation Philosophy:**
- Main README: High-level overview with links to detailed docs
- `/PAI_DIRECTORY/documentation/`: Comprehensive, detailed documentation
- Avoid duplication between main README and detailed docs
- When in doubt, link to detailed docs rather than duplicating

## 🎨 Code of Conduct

### Our Standards

- **Be respectful and inclusive** - PAI is for everyone
- **Be constructive** in feedback and discussions
- **Focus on the mission** - upgrading humans with AI
- **Help newcomers** - we want PAI to be accessible to all skill levels
- **Assume good intentions** - we're all here to help

### Unacceptable Behavior

- Harassment, discrimination, or exclusionary behavior
- Trolling, insulting comments, or personal attacks
- Publishing others' private information
- Other conduct inappropriate in a professional setting

## 🔄 Development Workflow

1. **Fork** the repository
2. **Create a branch** from `main`: `git checkout -b feature/your-feature-name`
3. **Make your changes** following the guidelines above
4. **Test thoroughly** in a local PAI installation
5. **Commit** with clear messages
6. **Push** to your fork
7. **Create a Pull Request** to the main repository

## 🧪 Testing Your Changes

Before submitting a PR:

1. **Install PAI** in a test environment
2. **Set PAI_DIR** to your test location
3. **Test all affected functionality:**
   - If you changed hooks, test them with various prompts
   - If you changed commands, run them
   - If you changed documentation, verify all links work
   - If you changed paths, test with PAI_DIR in different locations

4. **Test edge cases** and error conditions
5. **Verify no secrets** are in your commits

## 📝 Documentation Standards

When writing documentation:

- **Be clear and concise** - avoid jargon when possible
- **Provide examples** - show, don't just tell
- **Use consistent formatting:**
  - Commands in code blocks with bash syntax
  - File paths in code formatting: `${PAI_DIR}/context/`
  - Emphasis with **bold** or *italic* as appropriate

- **Structure with headers** for easy navigation
- **Include troubleshooting** for common issues
- **Link to related docs** to help users find more information

## 🌟 Areas We Need Help

Current priorities:
- **Documentation improvements** (this issue!)
- **Cross-platform support** (Linux, Windows)
- **Example contexts and commands** for different professions
- **Testing and bug fixes**
- **Performance optimization**
- **Accessibility improvements**

## 📞 Getting Help

- **GitHub Issues:** For bugs and feature requests
- **GitHub Discussions:** For questions and general discussion
- **Documentation:** Check `/PAI_DIRECTORY/documentation/` first

## 🙏 Recognition

Contributors will be:
- Listed in release notes
- Credited in relevant documentation
- Part of the mission to bring AI to everyone on Earth

## License

By contributing to PAI, you agree that your contributions will be licensed under the MIT License.

---

Thank you for helping make AI accessible to everyone! 🚀
