# MCP Server Integrations Guide

> **Comprehensive guide for Claude Code MCP servers, custom agents, and specialized skills**
>
> Last Updated: October 31, 2025

---

## 📋 Overview

This repository contains:
1. **MCP Server Installation Guide** - Complete setup guide for all available MCP servers
2. **Custom Sub Agents** - Specialized autonomous agents for complex tasks
3. **Custom Skills** - Focused skills for specific domain expertise
4. **Usage Guides** - Detailed documentation with examples and best practices

---

## 📁 Repository Structure

```
mcp-server-integrations-guide/
├── README.md                              # This file
├── QUICK-REFERENCE.md                     # Quick reference card (print this!)
├── MCP-Servers-Installation-Guide.md      # Complete MCP setup guide
├── MCP-Integration-Skill-Usage-Guide.md   # MCP Integration skill guide
├── GA4-GTM-Expert-Usage-Guide.md          # Complete GA4/GTM usage guide
├── prompt.md                              # Agent creation instructions
│
├── .claude/
│   ├── agents/                            # Custom sub agents
│   │   └── ga4-gtm-expert.md              # GA4/GTM implementation expert
│   │
│   └── skills/                            # Custom skills
│       ├── mcp-integration.md             # MCP server integration skill
│       └── ga4-gtm.md                     # GA4/GTM quick skill
```

---

## 🚀 Quick Start

### 1. Install Claude Code CLI
```bash
# Verify installation
claude --version
```

### 2. Set Up Essential MCP Servers
```bash
# Check current installations
claude mcp list

# If not installed, add core servers
claude mcp add --transport http context7 https://mcp.context7.com/mcp
claude mcp add --transport stdio playwright -- npx -y @executeautomation/playwright-mcp-server
claude mcp add --transport stdio chrome-devtools -- npx -y chrome-devtools-mcp --isolated
```

### 3. Verify Agent & Skill Installation
```bash
# Check if files exist
ls -la .claude/agents/ga4-gtm-expert.md
ls -la .claude/skills/ga4-gtm.md
```

---

## 📚 Documentation

### 📋 [Quick Reference Card](QUICK-REFERENCE.md) ⭐
**Print this!** Ultra-concise cheat sheet for daily use with common commands, patterns, and troubleshooting.

### Core Guides

#### [MCP Servers Installation Guide](MCP-Servers-Installation-Guide.md)
Complete reference for installing and configuring all available MCP servers:
- ✅ Currently installed servers (context7, playwright, chrome-devtools, etc.)
- 📦 Popular MCP servers (filesystem, github, postgres, etc.)
- 🎯 Use case recommendations
- ⚡ Token optimization strategies
- 🔧 Troubleshooting tips

#### [MCP Integration Skill Usage Guide](MCP-Integration-Skill-Usage-Guide.md)
Comprehensive guide for using the MCP Integration skill:
- 🔌 Installation workflows and examples
- 🐛 Troubleshooting decision trees
- 📊 Server recommendations by use case
- 🔒 Security and credential management
- ⚡ Token optimization strategies
- 💻 Platform-specific guidance (macOS, Windows, Linux)

#### [GA4/GTM Expert Usage Guide](GA4-GTM-Expert-Usage-Guide.md)
Comprehensive guide for using the GA4/GTM sub agent and skill:
- 🎯 When to use sub agent vs skill
- 📝 Detailed usage examples
- 🔌 MCP requirements and setup
- 💡 Advanced workflows
- ✅ Best practices

---

## 🤖 Available Agents & Skills

### MCP Integration Expert

**Skill**: `.claude/skills/mcp-integration.md`
- MCP server installation and configuration
- Troubleshooting connection issues
- Server recommendations by use case
- Token optimization strategies
- Security and credential management
- Platform-specific setup (macOS, Windows, Linux)

**Usage Example**:
```plaintext
# Installing new MCP servers
Use the mcp-integration skill to install the postgres MCP server

# Troubleshooting
Use the mcp-integration skill to debug why chrome-devtools is not connecting

# Optimization
Use the mcp-integration skill to recommend MCPs for web development workflow
```

**Full Documentation**: [MCP Integration Skill Usage Guide](MCP-Integration-Skill-Usage-Guide.md)

---

### Google Analytics 4 & GTM Expert

**Sub Agent**: `.claude/agents/ga4-gtm-expert.md`
- Complex GA4/GTM implementations
- UA to GA4 migrations
- Server-side GTM architecture
- Data pipeline design
- Complete roadmap planning

**Skill**: `.claude/skills/ga4-gtm.md`
- Quick event implementation
- Tag debugging
- DataLayer documentation
- GTM configuration
- Testing procedures

**Usage Example**:
```plaintext
# Using the skill (quick task)
Use the ga4-gtm skill to implement a custom purchase event

# Using the sub agent (complex project)
Plan and execute a complete GA4 migration including server-side GTM and BigQuery data pipeline
```

**Full Documentation**: [GA4/GTM Expert Usage Guide](GA4-GTM-Expert-Usage-Guide.md)

---

## 🔌 MCP Server Recommendations

### Currently Installed (Verified ✅)

| Server | Purpose | Status |
|--------|---------|--------|
| **context7** | Up-to-date library documentation | ✓ Connected |
| **playwright** | Browser automation & testing | ✓ Connected |
| **microsoft-learn** | Microsoft documentation | ✓ Connected |
| **firecrawl** | Web scraping & extraction | ✓ Connected |
| **chrome-devtools** | Chrome browser control | ✓ Connected |

### Recommended Additions

#### For GA4/GTM Work
```bash
# Essential for analytics work
claude mcp add --transport stdio filesystem -- npx -y @modelcontextprotocol/server-filesystem ~/Documents/GA4-Projects
claude mcp add --transport stdio memory -- npx -y @modelcontextprotocol/server-memory
claude mcp add --transport stdio fetch -- npx -y @modelcontextprotocol/server-fetch

# For BigQuery data analysis
claude mcp add --transport stdio postgres --env POSTGRES_CONNECTION_STRING="your-connection" -- npx -y @modelcontextprotocol/server-postgres
```

#### For Development Work
```bash
# GitHub integration
claude mcp add --transport stdio github --env GITHUB_TOKEN=YOUR_TOKEN -- npx -y @modelcontextprotocol/server-github

# Git repository analysis
claude mcp add --transport stdio git -- npx -y @modelcontextprotocol/server-git .
```

**See**: [MCP Servers Installation Guide](MCP-Servers-Installation-Guide.md) for complete installation instructions.

---

## 💡 Usage Examples

### Example 1: Implement GA4 Tracking
```plaintext
You: Use the ga4-gtm skill to implement enhanced e-commerce tracking with purchase events

Result:
- Complete dataLayer code
- GTM configuration steps
- Testing checklist
- Best practices
```

### Example 2: Debug Tag Issues
```plaintext
You: My checkout events aren't firing. Use Chrome DevTools to debug.

Result:
- Live dataLayer inspection
- Tag firing validation
- Network request analysis
- Fix recommendations
```

### Example 3: Complete Migration
```plaintext
You: Migrate our site from Universal Analytics to GA4 with server-side GTM

Result (via ga4-gtm-expert sub agent):
- Migration roadmap
- Event taxonomy design
- Implementation code
- Testing suite
- Documentation
```

### Example 4: Create Documentation
```plaintext
You: Create dataLayer specification for our e-commerce site

Result:
- Event specifications
- Code examples
- Developer implementation guide
- QA procedures
```

---

## 🎯 Use Case Matrix

| Your Goal | Use This | Required MCPs |
|-----------|----------|---------------|
| Install MCP server | mcp-integration skill | - |
| Debug MCP issues | mcp-integration skill | - |
| Configure MCPs | mcp-integration skill | - |
| MCP recommendations | mcp-integration skill | context7 |
| Implement single event | ga4-gtm skill | context7 |
| Debug tag firing | ga4-gtm skill | chrome-devtools |
| Complete GA4 setup | ga4-gtm-expert agent | context7, filesystem |
| UA to GA4 migration | ga4-gtm-expert agent | context7, memory |
| Server-side GTM | ga4-gtm-expert agent | context7, filesystem |
| BigQuery pipeline | ga4-gtm-expert agent | context7, postgres |
| Create docs | Either | context7, filesystem |
| Test implementation | ga4-gtm skill | playwright |

---

## 📖 Learning Resources

### Internal Documentation
- [MCP Servers Installation Guide](MCP-Servers-Installation-Guide.md) - MCP setup & config reference
- [MCP Integration Skill Usage Guide](MCP-Integration-Skill-Usage-Guide.md) - Using the MCP skill
- [GA4/GTM Expert Usage Guide](GA4-GTM-Expert-Usage-Guide.md) - Analytics implementation
- [QUICK-REFERENCE.md](QUICK-REFERENCE.md) - Quick commands cheat sheet
- [prompt.md](prompt.md) - Agent creation guidelines

### External Resources
- [Claude Code Documentation](https://docs.claude.com/claude-code)
- [Model Context Protocol](https://modelcontextprotocol.io)
- [GA4 Documentation](https://support.google.com/analytics/topic/9143232)
- [GTM Documentation](https://support.google.com/tagmanager)

---

## 🔧 Troubleshooting

### Common Issues

#### Agent/Skill Not Found
```bash
# Verify files exist
ls -la .claude/agents/
ls -la .claude/skills/
```

#### MCP Server Not Connected
```bash
# Check status
claude mcp list

# Reconnect if needed
claude mcp remove server-name
claude mcp add [server-config]
```

#### Chrome DevTools Not Working
```bash
# Use isolated mode (recommended)
claude mcp remove chrome-devtools
claude mcp add --transport stdio chrome-devtools -- npx -y chrome-devtools-mcp --isolated
```

**See**: [Troubleshooting Guide](MCP-Servers-Installation-Guide.md#troubleshooting) for complete solutions.

---

## 🚀 Next Steps

### For Analytics Professionals
1. ✅ Verify MCP servers: `claude mcp list`
2. 📖 Read [GA4/GTM Expert Usage Guide](GA4-GTM-Expert-Usage-Guide.md)
3. 🎯 Try implementing a simple custom event
4. 🔧 Install filesystem & memory MCPs for advanced features
5. 🚀 Start with complex migrations using the sub agent

### For Developers
1. ✅ Install recommended MCPs (filesystem, github, git)
2. 📖 Review [MCP Installation Guide](MCP-Servers-Installation-Guide.md)
3. 🤖 Explore creating custom agents/skills using [prompt.md](prompt.md)
4. 🔌 Contribute new agents/skills for other use cases

### For Teams
1. 📋 Create team-wide MCP setup script
2. 🔐 Set up shared API keys (Firecrawl, GitHub, etc.)
3. 📚 Document team-specific event taxonomies
4. 🤝 Share custom agents/skills across team

---

## 🤝 Contributing

### Adding New Agents/Skills

1. Follow guidelines in [prompt.md](prompt.md)
2. Create agent file in `.claude/agents/` or skill file in `.claude/skills/`
3. Create usage guide with examples
4. Update this README with new agent/skill info

### Improving Documentation

1. Test the guides and identify gaps
2. Add more examples and use cases
3. Update troubleshooting sections
4. Share best practices

---

## 📊 Token Optimization

### Best Practices

1. **Use Specialized MCPs**: context7 > WebFetch for documentation
2. **Leverage Memory**: Store frequently used context
3. **Batch Operations**: Combine related requests
4. **Use Targeted Agents**: ga4-gtm skill for quick tasks, agent for complex work

**See**: [Token Optimization Guide](MCP-Servers-Installation-Guide.md#token-optimization-guide) for detailed strategies.

---

## 📋 Quick Command Reference

### MCP Management
```bash
# List all servers
claude mcp list

# Add server
claude mcp add --transport stdio server-name -- npx -y package-name

# Remove server
claude mcp remove server-name

# Get server details
claude mcp get server-name
```

### Using Agents/Skills
```plaintext
# Invoke skill
Use the ga4-gtm skill to [task]

# Invoke sub agent
Use the Task tool to invoke ga4-gtm-expert to [complex task]

# Let Claude decide
[Provide clear, specific request and Claude will choose]
```

---

## 📞 Support

### Getting Help
- 📖 Check documentation in this repo
- 🔍 Review [troubleshooting guides](MCP-Servers-Installation-Guide.md#troubleshooting)
- 💬 Join [Claude Code community](https://docs.claude.com/claude-code)
- 🐛 Report issues at [GitHub](https://github.com/anthropics/claude-code/issues)

---

## 📝 License

This guide is provided as-is for use with Claude Code. Feel free to adapt and share.

---

## 🎯 Quick Start Checklist

- [ ] Claude Code CLI installed and verified
- [ ] Essential MCPs connected (context7, chrome-devtools, playwright)
- [ ] Agent & skill files exist in `.claude/` directories
- [ ] Read relevant usage guides
- [ ] Tested basic agent/skill invocation
- [ ] Installed recommended MCPs for your use case
- [ ] Created backup of `.claude.json` config
- [ ] Joined Claude Code community for updates

---

**Happy Building with Claude Code! 🚀**

For the latest updates and new agents/skills, check this repository regularly.
