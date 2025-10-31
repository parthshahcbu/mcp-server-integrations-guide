# MCP Servers Installation Guide for Claude Code

> **Last Updated:** October 31, 2025
> **Platform Support:** macOS & Windows
> **Installation Scope:** User (Global)

---

## Table of Contents

1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Quick Reference - Installed Servers](#quick-reference---installed-servers)
4. [Installation Guide](#installation-guide)
   - [Currently Installed Servers](#currently-installed-servers)
   - [Popular MCP Servers](#popular-mcp-servers)
5. [Token Optimization Guide](#token-optimization-guide)
6. [MCP Server Recommendations](#mcp-server-recommendations)
7. [Configuration Tips](#configuration-tips)
8. [Troubleshooting](#troubleshooting)

---

## Introduction

Model Context Protocol (MCP) servers extend Claude Code's capabilities by providing specialized tools and integrations. This guide covers installation, configuration, and best practices for the most useful MCP servers.

---

## Prerequisites

### macOS
- **Node.js** (v18 or higher): `brew install node`
- **npm** (comes with Node.js)
- **Claude Code CLI** installed

### Windows
- **Node.js** (v18 or higher): Download from [nodejs.org](https://nodejs.org)
- **npm** (comes with Node.js)
- **Claude Code CLI** installed

### Verify Installation
```bash
node --version
npm --version
claude --version
```

---

## Quick Reference - Installed Servers

Currently installed and connected MCP servers:

| Server | Status | Purpose |
|--------|--------|---------|
| context7 | ✓ Connected | Up-to-date library documentation |
| playwright | ✓ Connected | Browser automation and testing |
| microsoft-learn | ✓ Connected | Microsoft documentation access |
| firecrawl | ✓ Connected | Web scraping and content extraction |
| chrome-devtools | ✓ Connected | Chrome browser control and inspection |

Check status: `claude mcp list`

---

## Installation Guide

### Currently Installed Servers

#### 1. Context7
**Purpose:** Access up-to-date documentation and code examples for any library

**Installation:**
```bash
# Context7 uses HTTP transport (no installation needed)
claude mcp add --transport http context7 https://mcp.context7.com/mcp
```

**Usage:** Automatically provides documentation when you ask about libraries or frameworks.

---

#### 2. Playwright
**Purpose:** Browser automation, web scraping, and end-to-end testing

**Installation:**

**macOS:**
```bash
# Add MCP server
claude mcp add --transport stdio playwright -- npx -y @executeautomation/playwright-mcp-server

# Install Playwright browsers (required)
npx playwright install
```

**Windows (PowerShell):**
```powershell
# Add MCP server
claude mcp add --transport stdio playwright -- npx -y @executeautomation/playwright-mcp-server

# Install Playwright browsers (required)
npx playwright install
```

**Key Features:**
- Navigate websites and take screenshots
- Fill forms and click elements
- Execute JavaScript in browser
- Retrieve console logs
- HTTP requests (GET, POST, PUT, DELETE)

---

#### 3. Microsoft Learn
**Purpose:** Access Microsoft's official documentation and technical content

**Installation:**
```bash
# Uses HTTP transport (remote endpoint)
claude mcp add --transport http microsoft-learn https://learn.microsoft.com/api/mcp
```

**Usage:** Ask questions about Microsoft technologies (.NET, Azure, TypeScript, etc.)

---

#### 4. Firecrawl
**Purpose:** Advanced web scraping with JavaScript rendering and structured data extraction

**Installation:**

**Prerequisites:** Get API key from [firecrawl.dev](https://www.firecrawl.dev/app/api-keys)

**macOS & Windows:**
```bash
# Replace YOUR_API_KEY with your actual Firecrawl API key
claude mcp add --transport stdio firecrawl --env FIRECRAWL_API_KEY=YOUR_API_KEY -- npx -y firecrawl-mcp
```

**Key Features:**
- JavaScript rendering
- Batch processing
- Search capabilities
- Content filtering
- Automatic retries

---

#### 5. Chrome DevTools
**Purpose:** Control and inspect live Chrome browser with full DevTools access

**Installation:**

**macOS:**
```bash
# Isolated mode (recommended - auto-manages Chrome)
claude mcp add --transport stdio chrome-devtools -- npx -y chrome-devtools-mcp --isolated
```

**Windows (PowerShell):**
```powershell
# Isolated mode (recommended - auto-manages Chrome)
claude mcp add --transport stdio chrome-devtools -- npx -y chrome-devtools-mcp --isolated
```

**Alternative - Manual Chrome Setup:**
If you need to use your existing Chrome profile:

**macOS:**
```bash
# Launch Chrome with remote debugging
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222

# In another terminal, add MCP server
claude mcp add --transport stdio chrome-devtools -- npx -y chrome-devtools-mcp
```

**Windows (Command Prompt):**
```cmd
# Launch Chrome with remote debugging
"C:\Program Files\Google\Chrome\Application\chrome.exe" --remote-debugging-port=9222

# In another terminal, add MCP server
claude mcp add --transport stdio chrome-devtools -- npx -y chrome-devtools-mcp
```

---

### Popular MCP Servers

#### 6. Filesystem
**Purpose:** Secure file operations with configurable access controls

**Installation:**
```bash
# Basic installation
claude mcp add --transport stdio filesystem -- npx -y @modelcontextprotocol/server-filesystem /path/to/allowed/directory

# Example: Allow access to home directory
claude mcp add --transport stdio filesystem -- npx -y @modelcontextprotocol/server-filesystem ~
```

**Security Note:** Only grant access to directories you trust Claude to modify.

---

#### 7. GitHub
**Purpose:** Complete GitHub integration for repository management and code review

**Installation:**

**Prerequisites:** GitHub Personal Access Token
1. Go to GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Generate new token with `repo` scope

**macOS & Windows:**
```bash
# Replace YOUR_GITHUB_TOKEN with your actual token
claude mcp add --transport stdio github --env GITHUB_TOKEN=YOUR_GITHUB_TOKEN -- npx -y @modelcontextprotocol/server-github
```

**Key Features:**
- Repository management
- Issue tracking
- Pull request automation
- Code review
- Changelog generation

---

#### 8. Git
**Purpose:** Read, search, and manipulate Git repositories

**Installation:**
```bash
# Allow access to specific repository
claude mcp add --transport stdio git -- npx -y @modelcontextprotocol/server-git /path/to/repo

# Example: Current directory
claude mcp add --transport stdio git -- npx -y @modelcontextprotocol/server-git .
```

**Key Features:**
- View commit history
- Search code across commits
- Analyze repository structure
- Track file changes

---

#### 9. PostgreSQL
**Purpose:** PostgreSQL database integration with schema inspection and queries

**Installation:**

**Prerequisites:** PostgreSQL connection string

**macOS & Windows:**
```bash
# Replace with your actual connection string
claude mcp add --transport stdio postgres --env POSTGRES_CONNECTION_STRING="postgresql://user:password@localhost:5432/dbname" -- npx -y @modelcontextprotocol/server-postgres
```

**Key Features:**
- Schema inspection
- Query execution
- Database analysis
- Data modeling

---

#### 10. Memory
**Purpose:** Knowledge graph-based persistent memory system for long-term context

**Installation:**
```bash
claude mcp add --transport stdio memory -- npx -y @modelcontextprotocol/server-memory
```

**Key Features:**
- Persistent knowledge storage
- Context retention across sessions
- Relationship mapping
- Information retrieval

---

#### 11. Brave Search
**Purpose:** Web search capabilities using Brave Search API

**Installation:**

**Prerequisites:** Brave Search API key from [brave.com/search/api](https://brave.com/search/api)

**macOS & Windows:**
```bash
# Replace YOUR_API_KEY with your Brave Search API key
claude mcp add --transport stdio brave-search --env BRAVE_API_KEY=YOUR_API_KEY -- npx -y @modelcontextprotocol/server-brave-search
```

---

#### 12. Slack
**Purpose:** Slack workspace integration for channel management and messaging

**Installation:**

**Prerequisites:** Slack Bot Token
1. Go to [api.slack.com/apps](https://api.slack.com/apps)
2. Create new app
3. Add bot token scopes (channels:read, chat:write, etc.)

**macOS & Windows:**
```bash
# Replace YOUR_BOT_TOKEN with your Slack bot token
claude mcp add --transport stdio slack --env SLACK_BOT_TOKEN=YOUR_BOT_TOKEN -- npx -y @modelcontextprotocol/server-slack
```

---

#### 13. Google Drive
**Purpose:** Google Drive integration for file access and management

**Installation:**

**Prerequisites:** Google OAuth credentials
1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Enable Google Drive API
3. Create OAuth 2.0 credentials

**macOS & Windows:**
```bash
# Follow interactive setup
npx -y @modelcontextprotocol/server-gdrive init

# Add to Claude Code
claude mcp add --transport stdio gdrive -- npx -y @modelcontextprotocol/server-gdrive
```

---

#### 14. Sequential Thinking
**Purpose:** Dynamic problem-solving through structured thought sequences

**Installation:**
```bash
claude mcp add --transport stdio sequential-thinking -- npx -y @modelcontextprotocol/server-sequential-thinking
```

**Key Features:**
- Multi-step reasoning
- Thought process visibility
- Complex problem decomposition

---

#### 15. Fetch
**Purpose:** Web content fetching and conversion optimized for LLM usage

**Installation:**
```bash
claude mcp add --transport stdio fetch -- npx -y @modelcontextprotocol/server-fetch
```

**Key Features:**
- HTML to Markdown conversion
- Content extraction
- Link following
- Efficient content formatting

---

## Token Optimization Guide

### Best Practices for Reducing Token Usage

#### 1. **Use MCP Servers Instead of Direct File Operations**
- ✅ **Do:** Use Filesystem MCP server for file access
- ❌ **Don't:** Read entire files with `cat` or `Read` tool when MCP can filter

**Token Savings:** 30-50% when working with large files

---

#### 2. **Leverage Specialized Servers**
- ✅ **Do:** Use Context7 for documentation instead of web searches
- ✅ **Do:** Use GitHub MCP server instead of manual API calls
- ❌ **Don't:** Use WebFetch when a specialized server exists

**Token Savings:** 40-60% by using optimized data formats

---

#### 3. **Configure Appropriate Scopes**
- ✅ **Do:** Limit filesystem access to specific directories
- ✅ **Do:** Use Git server only for relevant repositories
- ❌ **Don't:** Grant broad access that returns unnecessary data

**Token Savings:** 20-40% by reducing context scope

---

#### 4. **Use Memory Server for Long Sessions**
- ✅ **Do:** Store important context in Memory server
- ✅ **Do:** Reference stored knowledge instead of repeating context
- ❌ **Don't:** Re-explain the same information each session

**Token Savings:** 50-70% in multi-session projects

---

#### 5. **Batch Operations Efficiently**
- ✅ **Do:** Use Firecrawl's batch processing for multiple pages
- ✅ **Do:** Combine related operations in single requests
- ❌ **Don't:** Make individual requests for each item

**Token Savings:** 30-50% through operation batching

---

#### 6. **Optimize Search Queries**
- ✅ **Do:** Use specific search patterns with Brave Search
- ✅ **Do:** Filter results at the source (MCP server level)
- ❌ **Don't:** Fetch all results and filter client-side

**Token Savings:** 40-60% with targeted queries

---

## MCP Server Recommendations

### By Use Case

#### **Web Development**
1. **Playwright** - Browser automation and testing
2. **Chrome DevTools** - Live browser inspection
3. **Firecrawl** - Web scraping and content extraction
4. **Fetch** - Simple content fetching

**Why:** Comprehensive browser control and content extraction capabilities.

---

#### **Documentation & Learning**
1. **Context7** - Library documentation (always up-to-date)
2. **Microsoft Learn** - Microsoft ecosystem documentation
3. **Brave Search** - Web search for current information
4. **Fetch** - Documentation page fetching

**Why:** Reduces hallucinations with authoritative sources.

---

#### **Data Engineering**
1. **PostgreSQL** - Database operations
2. **Filesystem** - File access and manipulation
3. **Sequential Thinking** - Complex data transformations
4. **Memory** - Context persistence

**Why:** Direct database access and structured data handling.

---

#### **DevOps & Repository Management**
1. **GitHub** - Repository and PR management
2. **Git** - Local repository analysis
3. **Slack** - Team notifications
4. **Filesystem** - File operations

**Why:** Complete development workflow automation.

---

#### **Research & Analysis**
1. **Brave Search** - Web search
2. **Firecrawl** - Advanced web scraping
3. **Memory** - Knowledge graph storage
4. **Sequential Thinking** - Complex reasoning

**Why:** Comprehensive information gathering and analysis.

---

#### **AI/ML Development**
1. **Filesystem** - Dataset access
2. **PostgreSQL** - Data storage
3. **GitHub** - Code versioning
4. **Sequential Thinking** - Algorithm design

**Why:** Data access, versioning, and structured problem-solving.

---

## Configuration Tips

### 1. **Organize by Scope**

**User Scope (Recommended):**
- Servers you use across all projects
- Examples: Context7, Microsoft Learn, Brave Search, GitHub

```bash
# Add to user scope (default)
claude mcp add --scope user --transport stdio server-name -- npx -y package-name
```

**Project Scope:**
- Project-specific servers
- Examples: Database servers, specific Git repos

```bash
# Add to project scope
claude mcp add --scope project --transport stdio server-name -- npx -y package-name
```

---

### 2. **Environment Variable Management**

**Secure Storage:**
- Store API keys in environment variables
- Never commit API keys to version control
- Use `.env` files with `.gitignore`

**Example `.env` file:**
```bash
FIRECRAWL_API_KEY=fc-xxx
GITHUB_TOKEN=ghp_xxx
BRAVE_API_KEY=BSA-xxx
SLACK_BOT_TOKEN=xoxb-xxx
```

---

### 3. **Performance Optimization**

**Remove Unused Servers:**
```bash
# Check installed servers
claude mcp list

# Remove unused server
claude mcp remove server-name
```

**Why:** Each server adds initialization overhead. Keep only what you need.

---

### 4. **Transport Type Selection**

| Transport | When to Use | Examples |
|-----------|-------------|----------|
| **HTTP** | Remote services, no local installation | Context7, Microsoft Learn |
| **stdio** | Local processing, NPM packages | Playwright, Filesystem |
| **SSE** | Real-time updates, streaming data | Chat services, live feeds |

---

### 5. **Monitoring & Health Checks**

**Regular Health Checks:**
```bash
# Check all server statuses
claude mcp list

# Get detailed info for specific server
claude mcp get server-name
```

**Best Practice:** Run weekly to ensure all servers are functioning.

---

### 6. **Update Management**

**Keep Servers Updated:**
```bash
# NPX automatically uses latest version with -y flag
# To force update, clear npm cache:
npm cache clean --force

# Restart Claude Code to reconnect servers
```

---

## Troubleshooting

### Common Issues

#### ❌ Server Failed to Connect

**Symptoms:** `✗ Failed to connect` in `claude mcp list`

**Solutions:**
1. **Check package name:**
   ```bash
   npm search package-name
   ```

2. **Verify Node.js version:**
   ```bash
   node --version  # Should be v18+
   ```

3. **Clear npm cache:**
   ```bash
   npm cache clean --force
   ```

4. **Remove and re-add server:**
   ```bash
   claude mcp remove server-name
   claude mcp add --transport stdio server-name -- npx -y package-name
   ```

---

#### ❌ API Key Not Working

**Symptoms:** Server connects but operations fail

**Solutions:**
1. **Verify API key:**
   - Check key hasn't expired
   - Verify key has correct permissions
   - Regenerate key if needed

2. **Check environment variable format:**
   ```bash
   # Correct format
   claude mcp add --transport stdio server -e API_KEY=value -- npx -y package

   # Check saved configuration
   claude mcp get server-name
   ```

---

#### ❌ Chrome DevTools Issues

**Symptoms:** Chrome DevTools not connecting

**Solutions:**

**For Isolated Mode:**
```bash
# Ensure Chrome is not already running
# Remove and re-add with --isolated flag
claude mcp remove chrome-devtools
claude mcp add --transport stdio chrome-devtools -- npx -y chrome-devtools-mcp --isolated
```

**For Manual Mode:**
```bash
# macOS - Launch Chrome with debugging
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222

# Windows - Launch Chrome with debugging
"C:\Program Files\Google\Chrome\Application\chrome.exe" --remote-debugging-port=9222

# Verify port 9222 is listening
netstat -an | grep 9222  # macOS/Linux
netstat -an | findstr 9222  # Windows
```

---

#### ❌ Permission Denied Errors

**Symptoms:** Filesystem or Git operations fail

**Solutions:**

**macOS:**
```bash
# Grant full disk access to Terminal/iTerm
# System Settings → Privacy & Security → Full Disk Access

# Use specific directories instead of system folders
claude mcp add --transport stdio filesystem -- npx -y @modelcontextprotocol/server-filesystem ~/Documents
```

**Windows:**
```powershell
# Run PowerShell as Administrator
# Right-click → "Run as administrator"

# Use specific directories
claude mcp add --transport stdio filesystem -- npx -y @modelcontextprotocol/server-filesystem C:\Users\YourName\Projects
```

---

#### ❌ Token/Rate Limits

**Symptoms:** Operations fail with quota errors

**Solutions:**
1. **Check API quotas** in respective service dashboards
2. **Upgrade plan** if needed
3. **Implement caching** using Memory server
4. **Use alternative servers** (e.g., Fetch instead of Firecrawl for simple scraping)

---

### Getting Help

**Documentation:**
- Claude Code Docs: [docs.claude.com/claude-code](https://docs.claude.com/claude-code)
- MCP Protocol: [modelcontextprotocol.io](https://modelcontextprotocol.io)
- GitHub Issues: [github.com/anthropics/claude-code/issues](https://github.com/anthropics/claude-code/issues)

**Community:**
- Official Discord: Claude Code community channels
- GitHub Discussions: Share configurations and solutions

---

## Additional Helpful Suggestions

### 1. **Create a Configuration Backup**

```bash
# macOS
cp ~/.claude.json ~/.claude.json.backup

# Windows
copy %USERPROFILE%\.claude.json %USERPROFILE%\.claude.json.backup
```

### 2. **Use Aliases for Common Commands**

**macOS/Linux (.bashrc or .zshrc):**
```bash
alias mcp-list='claude mcp list'
alias mcp-add='claude mcp add'
alias mcp-remove='claude mcp remove'
```

**Windows (PowerShell Profile):**
```powershell
function mcp-list { claude mcp list }
function mcp-add { claude mcp add $args }
function mcp-remove { claude mcp remove $args }
```

### 3. **Setup Script for New Machines**

Create a setup script to quickly configure your preferred MCP servers:

**macOS/Linux (setup-mcp.sh):**
```bash
#!/bin/bash

echo "Installing MCP servers..."

# Core servers
claude mcp add --transport http context7 https://mcp.context7.com/mcp
claude mcp add --transport http microsoft-learn https://learn.microsoft.com/api/mcp
claude mcp add --transport stdio playwright -- npx -y @executeautomation/playwright-mcp-server
claude mcp add --transport stdio chrome-devtools -- npx -y chrome-devtools-mcp --isolated

# With API keys (set these as environment variables first)
if [ ! -z "$FIRECRAWL_API_KEY" ]; then
    claude mcp add --transport stdio firecrawl -e FIRECRAWL_API_KEY=$FIRECRAWL_API_KEY -- npx -y firecrawl-mcp
fi

if [ ! -z "$GITHUB_TOKEN" ]; then
    claude mcp add --transport stdio github -e GITHUB_TOKEN=$GITHUB_TOKEN -- npx -y @modelcontextprotocol/server-github
fi

echo "MCP servers installed! Run 'claude mcp list' to verify."
```

**Windows (setup-mcp.ps1):**
```powershell
Write-Host "Installing MCP servers..."

# Core servers
claude mcp add --transport http context7 https://mcp.context7.com/mcp
claude mcp add --transport http microsoft-learn https://learn.microsoft.com/api/mcp
claude mcp add --transport stdio playwright -- npx -y @executeautomation/playwright-mcp-server
claude mcp add --transport stdio chrome-devtools -- npx -y chrome-devtools-mcp --isolated

# With API keys (set these as environment variables first)
if ($env:FIRECRAWL_API_KEY) {
    claude mcp add --transport stdio firecrawl -e FIRECRAWL_API_KEY=$env:FIRECRAWL_API_KEY -- npx -y firecrawl-mcp
}

if ($env:GITHUB_TOKEN) {
    claude mcp add --transport stdio github -e GITHUB_TOKEN=$env:GITHUB_TOKEN -- npx -y @modelcontextprotocol/server-github
}

Write-Host "MCP servers installed! Run 'claude mcp list' to verify."
```

### 4. **Environment-Specific Configurations**

**Development:**
- Add Memory server for context retention
- Add Sequential Thinking for complex problems
- Add Git server for local repos

**Production:**
- Add GitHub server for deployment automation
- Add Slack server for notifications
- Add PostgreSQL for data operations

**Research:**
- Add Brave Search for web research
- Add Firecrawl for advanced scraping
- Add Fetch for simple content extraction

---

## Quick Start Checklist

- [ ] Install Node.js and npm
- [ ] Verify Claude Code CLI is working
- [ ] Install core servers (Context7, Microsoft Learn)
- [ ] Install browser automation (Playwright, Chrome DevTools)
- [ ] Configure API keys for Firecrawl
- [ ] Install filesystem/database servers as needed
- [ ] Create configuration backup
- [ ] Set up setup script for future machines
- [ ] Test token optimization practices
- [ ] Join Claude Code community for updates

---

**Happy Coding with Claude Code!**

For updates to this guide, check the [official Claude Code documentation](https://docs.claude.com/claude-code).
