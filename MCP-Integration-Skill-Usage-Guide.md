# MCP Integration Skill - Complete Usage Guide

> **Expert assistance for Model Context Protocol server installation, configuration, and troubleshooting**
>
> Last Updated: October 31, 2025

---

## 📋 Table of Contents

1. [Overview](#overview)
2. [When to Use This Skill](#when-to-use-this-skill)
3. [Quick Start Examples](#quick-start-examples)
4. [Installation Workflows](#installation-workflows)
5. [Configuration Best Practices](#configuration-best-practices)
6. [Troubleshooting Guide](#troubleshooting-guide)
7. [Token Optimization](#token-optimization)
8. [Advanced Use Cases](#advanced-use-cases)
9. [Platform-Specific Guidance](#platform-specific-guidance)
10. [Security Best Practices](#security-best-practices)

---

## Overview

The **MCP Integration Skill** (`.claude/skills/mcp-integration.md`) is your expert assistant for all things related to Model Context Protocol (MCP) servers in Claude Code. It provides intelligent guidance for:

- 🔌 **Installation**: Step-by-step setup for any MCP server
- ⚙️ **Configuration**: Optimal settings for your use case
- 🐛 **Troubleshooting**: Quick diagnosis and fixes
- 📊 **Recommendations**: Best server choices for your workflow
- 🔒 **Security**: Credential and access management
- ⚡ **Optimization**: Token efficiency strategies

---

## When to Use This Skill

### ✅ Use the MCP Integration Skill for:

| Scenario | Example Request |
|----------|----------------|
| **Installing new servers** | "Use the mcp-integration skill to install the postgres MCP server" |
| **Debugging connections** | "Use the mcp-integration skill to debug why chrome-devtools won't connect" |
| **Getting recommendations** | "Use the mcp-integration skill to recommend MCPs for data engineering" |
| **Configuration help** | "Use the mcp-integration skill to set up filesystem MCP with proper security" |
| **Platform-specific setup** | "Use the mcp-integration skill to install playwright on Windows" |
| **Token optimization** | "Use the mcp-integration skill to optimize my MCP stack for lower token usage" |
| **Security guidance** | "Use the mcp-integration skill to securely manage my API keys" |

### ❌ Don't Use This Skill for:

- Using already-installed MCPs (just use them directly)
- GA4/GTM-specific work (use the ga4-gtm skill)
- General coding tasks (use Claude Code directly)
- Creating custom MCP servers (use documentation/agent)

---

## Quick Start Examples

### Example 1: Installing Your First MCP Server

**Request:**
```plaintext
Use the mcp-integration skill to install the memory MCP server
```

**What You Get:**
1. Platform detection (macOS, Windows, Linux)
2. Prerequisites check
3. Installation command with explanation
4. Verification steps
5. Basic usage examples
6. Common troubleshooting tips

**Sample Response:**
```bash
# For all platforms
claude mcp add --transport stdio memory -- npx -y @modelcontextprotocol/server-memory

# Verify installation
claude mcp list | grep memory

# Test it
# Now you can ask Claude to "store this information in memory" and it will persist
```

---

### Example 2: Debugging Connection Issues

**Request:**
```plaintext
Use the mcp-integration skill to debug why chrome-devtools is not connecting
```

**What You Get:**
1. Diagnostic checklist
2. Common causes analysis
3. Step-by-step fixes
4. Alternative solutions
5. Prevention tips

**Sample Response:**
```plaintext
Let's diagnose the chrome-devtools connection issue:

1. Check if Chrome is already running:
   - Close all Chrome instances
   - The MCP server needs exclusive debugging access

2. Reinstall with --isolated flag (recommended):
   claude mcp remove chrome-devtools
   claude mcp add --transport stdio chrome-devtools -- npx -y chrome-devtools-mcp --isolated

3. Verify the installation:
   claude mcp list | grep chrome-devtools

4. Alternative: Manual Chrome setup (if you need your profile):
   [Platform-specific commands provided]
```

---

### Example 3: Getting Server Recommendations

**Request:**
```plaintext
Use the mcp-integration skill to recommend MCPs for a web development workflow involving React, TypeScript, and PostgreSQL
```

**What You Get:**
1. Tailored server recommendations
2. Priority order
3. Installation commands
4. Use case explanations
5. Token optimization notes

**Sample Response:**
```plaintext
Recommended MCP Stack for React/TypeScript/PostgreSQL:

Essential (Install First):
1. context7 - Latest React/TypeScript docs
2. postgres - Database integration
3. filesystem - Project file access

Highly Recommended:
4. github - Code versioning
5. chrome-devtools - Browser debugging
6. playwright - E2E testing

Optional but Useful:
7. memory - Cross-session context
8. sequential-thinking - Complex problem solving

Installation commands:
[Platform-specific batch installation script provided]
```

---

### Example 4: Secure Configuration

**Request:**
```plaintext
Use the mcp-integration skill to set up the GitHub MCP server with secure credential management
```

**What You Get:**
1. Token generation guide
2. Secure storage methods
3. Installation with environment variables
4. Verification steps
5. Security best practices

**Sample Response:**
```plaintext
Secure GitHub MCP Setup:

1. Create Personal Access Token:
   - Go to GitHub Settings → Developer settings → Personal access tokens
   - Click "Generate new token (classic)"
   - Select scopes: repo, read:org, read:user
   - Copy token (you won't see it again!)

2. Store securely (choose one method):

   Method A - Environment variable (macOS/Linux):
   echo 'export GITHUB_TOKEN="ghp_your_token"' >> ~/.bashrc
   source ~/.bashrc

   Method B - Environment variable (Windows PowerShell):
   [System.Environment]::SetEnvironmentVariable('GITHUB_TOKEN', 'ghp_your_token', 'User')

   Method C - .env file (project-specific):
   echo 'GITHUB_TOKEN=ghp_your_token' >> .env
   Add .env to .gitignore

3. Install GitHub MCP:
   claude mcp add --transport stdio github --env GITHUB_TOKEN=$GITHUB_TOKEN -- npx -y @modelcontextprotocol/server-github

4. Verify:
   claude mcp list | grep github

Security reminders:
- Never commit tokens to git
- Rotate tokens regularly
- Use minimal required scopes
- Audit token usage periodically
```

---

## Installation Workflows

### Standard Installation Pattern

```plaintext
1. Identify your need
   ↓
2. Ask skill for recommendation
   ↓
3. Get platform-specific command
   ↓
4. Run installation
   ↓
5. Verify connection
   ↓
6. Test basic functionality
```

### Batch Installation for Teams

**Request:**
```plaintext
Use the mcp-integration skill to create a setup script for my team that installs context7, playwright, chrome-devtools, filesystem, and memory
```

**What You Get:**
- Complete bash/PowerShell script
- Error handling
- Verification steps
- Team distribution instructions
- Documentation template

---

## Configuration Best Practices

### User Scope vs Project Scope

**User Scope (Default - Recommended for most servers):**
```bash
# Available in all projects
claude mcp add --scope user --transport stdio server-name -- npx -y package-name
```

**Use user scope for:**
- Documentation servers (context7, microsoft-learn)
- General utilities (memory, sequential-thinking)
- Development tools (github, git)
- Browser automation (playwright, chrome-devtools)

**Project Scope:**
```bash
# Only available in current project
claude mcp add --scope project --transport stdio server-name -- npx -y package-name
```

**Use project scope for:**
- Project-specific databases
- Project-specific file access
- Temporary/experimental servers
- Client-specific integrations

### Environment Variable Management

**Best Practices:**
1. Use environment variables for all secrets
2. Never hard-code API keys
3. Document required variables
4. Use .env files with .gitignore
5. Provide .env.example for teams

---

## Troubleshooting Guide

### Common Issues & Solutions

#### Issue 1: "Server Failed to Connect"

**Request:**
```plaintext
Use the mcp-integration skill to fix a "server failed to connect" error for the playwright MCP
```

**Solutions Provided:**
- Verify Node.js version
- Clear npm cache
- Reinstall package
- Check for conflicting installations
- Platform-specific fixes

---

#### Issue 2: "API Key Not Working"

**Request:**
```plaintext
Use the mcp-integration skill to troubleshoot Firecrawl API key authentication issues
```

**Solutions Provided:**
- Verify key format
- Check key expiration
- Test key independently
- Recreate key if needed
- Proper environment variable syntax

---

#### Issue 3: "Permission Denied"

**Request:**
```plaintext
Use the mcp-integration skill to resolve filesystem MCP permission errors on macOS
```

**Solutions Provided:**
- Grant Full Disk Access to Terminal
- Use specific directories instead of root
- Check path existence
- Verify user permissions
- Alternative approaches

---

## Token Optimization

### Strategy 1: Use Specialized Servers

**Request:**
```plaintext
Use the mcp-integration skill to optimize my MCP stack for lower token usage
```

**Recommendations:**
- Replace WebFetch with context7 for documentation
- Use Memory for repeated context
- Configure appropriate scopes
- Batch operations
- Filter at source

**Token Savings:** 40-60%

---

### Strategy 2: Appropriate Scoping

**Guidance:**
- Limit filesystem access to specific directories
- Use targeted documentation servers
- Avoid broad permissions
- Configure server-specific filters

**Token Savings:** 20-40%

---

## Advanced Use Cases

### Creating Team Setup Scripts

**Request:**
```plaintext
Use the mcp-integration skill to create a comprehensive setup script for a data engineering team using Python, PostgreSQL, and Jupyter
```

**What You Get:**
- Full installation script
- Dependency checks
- Error handling
- Success verification
- Team documentation
- Troubleshooting guide

---

### Multi-Environment Configuration

**Request:**
```plaintext
Use the mcp-integration skill to set up different MCP configurations for development, staging, and production
```

**What You Get:**
- Environment-specific configs
- Scope management strategy
- Credential isolation
- Deployment procedures
- Migration guides

---

### Custom MCP Integration

**Request:**
```plaintext
Use the mcp-integration skill to help me integrate a custom internal MCP server
```

**What You Get:**
- Integration checklist
- Configuration examples
- Testing procedures
- Documentation template
- Troubleshooting framework

---

## Platform-Specific Guidance

### macOS

**Special Considerations:**
- Homebrew package management
- Terminal Full Disk Access
- Path configurations
- Native vs Rosetta (Apple Silicon)

**Request Example:**
```plaintext
Use the mcp-integration skill to set up all essential MCPs on macOS with Apple Silicon
```

---

### Windows

**Special Considerations:**
- PowerShell vs Command Prompt
- Path format (backslashes)
- Windows Defender exclusions
- WSL compatibility

**Request Example:**
```plaintext
Use the mcp-integration skill to install chrome-devtools on Windows 11
```

---

### Linux

**Special Considerations:**
- Distribution differences
- Package manager variations
- Permission management
- Systemd integration

**Request Example:**
```plaintext
Use the mcp-integration skill to set up PostgreSQL MCP on Ubuntu 22.04
```

---

## Security Best Practices

### 1. Credential Management

**Never:**
- ❌ Hard-code API keys
- ❌ Commit .env to git
- ❌ Share keys in plain text
- ❌ Use production keys in development

**Always:**
- ✅ Use environment variables
- ✅ Add .env to .gitignore
- ✅ Rotate keys regularly
- ✅ Use minimal required scopes
- ✅ Audit access logs

---

### 2. Filesystem Access

**Principle of Least Privilege:**
```bash
# ❌ Too broad
claude mcp add --transport stdio filesystem -- npx -y @modelcontextprotocol/server-filesystem /

# ✅ Specific and safe
claude mcp add --transport stdio filesystem -- npx -y @modelcontextprotocol/server-filesystem ~/Documents/Projects
```

---

### 3. Regular Audits

**Request:**
```plaintext
Use the mcp-integration skill to audit my current MCP security configuration
```

**Audit Checklist:**
- Review installed servers
- Check granted permissions
- Verify credential storage
- Assess scope appropriateness
- Identify unused servers
- Update outdated packages

---

## Real-World Workflows

### Workflow 1: Setting Up for Analytics Work

**Request:**
```plaintext
Use the mcp-integration skill to set up MCPs for GA4/GTM development and debugging
```

**What You Get:**
1. context7 (documentation)
2. chrome-devtools (debugging)
3. playwright (testing)
4. filesystem (GTM exports)
5. memory (event taxonomy storage)
6. postgres (BigQuery analysis - optional)

Plus:
- Installation commands
- Configuration guidance
- Usage examples
- Integration with ga4-gtm skill

---

### Workflow 2: Full-Stack Development Setup

**Request:**
```plaintext
Use the mcp-integration skill to configure MCPs for full-stack development with React, Node.js, and PostgreSQL
```

**Recommended Stack:**
- context7, github, git, postgres, filesystem, chrome-devtools, playwright, memory

---

### Workflow 3: Data Science & Analysis

**Request:**
```plaintext
Use the mcp-integration skill to set up MCPs for data science work with Python and Jupyter
```

**Recommended Stack:**
- context7, filesystem, postgres, memory, sequential-thinking, fetch

---

## Quick Reference Commands

### Check Installation Status
```bash
claude mcp list
claude mcp list | grep server-name
```

### Install Server
```bash
# Basic
claude mcp add --transport stdio server-name -- npx -y package-name

# With environment variable
claude mcp add --transport stdio server-name --env VAR=value -- npx -y package-name

# HTTP transport
claude mcp add --transport http server-name https://url
```

### Remove Server
```bash
claude mcp remove server-name
```

### Get Server Details
```bash
claude mcp get server-name
```

---

## Best Practices Summary

1. **Start Small**: Install core servers first (context7, filesystem)
2. **Test Incrementally**: Verify each server before adding more
3. **Document Everything**: Keep notes on configuration decisions
4. **Backup Config**: Save `.claude.json` regularly
5. **Monitor Health**: Weekly `claude mcp list` checks
6. **Stay Updated**: Clear npm cache and update servers monthly
7. **Secure by Default**: Use environment variables for all credentials
8. **Scope Appropriately**: User vs project scope thoughtfully
9. **Optimize Tokens**: Use specialized servers over generic ones
10. **Team Alignment**: Share setup scripts and configurations

---

## Getting Help

### Using the Skill

Just invoke it naturally:
```plaintext
Use the mcp-integration skill to [your task]
```

### Additional Resources

- [MCP Servers Installation Guide](MCP-Servers-Installation-Guide.md) - Complete reference
- [Quick Reference](QUICK-REFERENCE.md) - Commands cheat sheet
- [README](README.md) - Repository overview
- [Claude Code Docs](https://docs.claude.com/claude-code) - Official documentation
- [MCP Protocol](https://modelcontextprotocol.io) - Protocol specification

---

## Skill File Location

`.claude/skills/mcp-integration.md`

This skill is available in **user scope** by default, meaning it's accessible from any project where Claude Code is running.

---

## Integration with Other Skills

### Works Great With:

- **ga4-gtm skill**: Recommends MCPs for analytics work
- **ga4-gtm-expert agent**: Sets up required MCPs for complex implementations
- **Custom agents**: Configures MCP dependencies

### Example Combined Usage:

```plaintext
1. Use the mcp-integration skill to install chrome-devtools and playwright
2. Use the ga4-gtm skill to debug tag firing issues (uses chrome-devtools)
3. Use the ga4-gtm skill to create automated tests (uses playwright)
```

---

## Troubleshooting Decision Tree

```plaintext
Issue with MCP?
├─ Installation failure?
│  └─ Use skill: "debug installation of [server]"
├─ Connection problem?
│  └─ Use skill: "fix connection issue for [server]"
├─ API key error?
│  └─ Use skill: "troubleshoot [server] authentication"
├─ Permission denied?
│  └─ Use skill: "resolve permission error for [server]"
├─ Need recommendation?
│  └─ Use skill: "recommend MCPs for [use case]"
└─ Configuration help?
   └─ Use skill: "configure [server] for [requirement]"
```

---

## Success Metrics

After using this skill, you should:
- ✅ Have working MCP servers installed
- ✅ Understand why each server was chosen
- ✅ Know how to verify connections
- ✅ Have secure credential management
- ✅ Follow token optimization practices
- ✅ Be able to troubleshoot common issues
- ✅ Have documented your configuration

---

## Changelog

**v1.0 - October 31, 2025**
- Initial release of MCP Integration Skill
- Comprehensive installation guidance
- Platform-specific support (macOS, Windows, Linux)
- Security best practices
- Token optimization strategies
- Integration examples

---

## Contributing

Found an issue or have a suggestion? This skill is designed to help with MCP integration. For:
- MCP-specific issues → Use this skill
- GA4/GTM issues → Use ga4-gtm skill/agent
- General Claude Code issues → See [official docs](https://docs.claude.com/claude-code)

---

**Master your MCP setup with the MCP Integration Skill! 🔌**

For the latest updates, check the [main README](README.md).
