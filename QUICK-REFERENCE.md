# Quick Reference Card - GA4/GTM Expert & MCPs

> **Ultra-concise reference for daily use**
> Print or bookmark for quick access

---

## 🎯 GA4/GTM Agent/Skill Selection

| Task Type | Use This | Example |
|-----------|----------|---------|
| Single event | **Skill** | "Implement add_to_cart event" |
| Debug issue | **Skill** | "Debug why purchase event not firing" |
| Full migration | **Agent** | "Migrate UA to GA4" |
| Architecture | **Agent** | "Design server-side GTM" |
| Documentation | **Either** | "Create dataLayer spec" |
| Roadmap | **Agent** | "Plan GA4 implementation" |

---

## 💬 Invocation Patterns

### Quick Tasks (Skill)
```plaintext
Use the ga4-gtm skill to [task]

Examples:
- Use the ga4-gtm skill to implement purchase event
- Use the ga4-gtm skill to debug tag firing issues
- Use the ga4-gtm skill to create event documentation
```

### Complex Projects (Agent)
```plaintext
Use the Task tool to invoke ga4-gtm-expert to [complex task]

Examples:
- Plan and execute complete GA4 migration
- Design and implement server-side GTM architecture
- Create comprehensive event taxonomy and implementation
```

### Let Claude Decide
```plaintext
Just describe your need clearly:
- "I need to implement checkout tracking"
- "Debug my GTM container"
- "Migrate from UA to GA4"
```

---

## 🔌 Essential MCP Commands

### Check Status
```bash
# List all servers
claude mcp list

# Check specific server
claude mcp list | grep context7
```

### Core MCPs for GA4/GTM
```bash
# Already installed - verify:
claude mcp list | grep -E "context7|chrome|playwright"
```

### Recommended Additions
```bash
# Filesystem (for GTM exports)
claude mcp add --transport stdio filesystem -- npx -y @modelcontextprotocol/server-filesystem ~/Documents/GA4

# Memory (for session persistence)
claude mcp add --transport stdio memory -- npx -y @modelcontextprotocol/server-memory

# Fetch (for Google docs)
claude mcp add --transport stdio fetch -- npx -y @modelcontextprotocol/server-fetch
```

### Quick Reinstall
```bash
# Remove and re-add
claude mcp remove server-name
claude mcp add --transport stdio server-name -- npx -y package-name
```

---

## 🎯 Common GA4/GTM Requests

### Implementation
```plaintext
Implement [event_name] tracking for [platform]
└─ Example: Implement purchase event for Next.js app

Create [event_type] tracking with [parameters]
└─ Example: Create video_play tracking with video_title and duration

Set up [feature] in GA4
└─ Example: Set up enhanced measurement and custom dimensions
```

### Debugging
```plaintext
Debug why [issue] using Chrome DevTools
└─ Example: Debug why checkout events fire twice

Validate [implementation] in GTM Preview
└─ Example: Validate e-commerce tracking in GTM Preview

Inspect dataLayer for [page/event]
└─ Example: Inspect dataLayer for product detail page
```

### Documentation
```plaintext
Create dataLayer documentation for [scope]
└─ Example: Create dataLayer docs for checkout funnel

Document [implementation] with code examples
└─ Example: Document server-side GTM setup with examples

Generate testing checklist for [feature]
└─ Example: Generate testing checklist for conversion tracking
```

### Testing
```plaintext
Create Playwright test for [event/funnel]
└─ Example: Create Playwright test for purchase funnel

Automate testing of [tracking]
└─ Example: Automate testing of product_view events
```

### Migration
```plaintext
Migrate [source] to [target]
└─ Example: Migrate Universal Analytics to GA4

Plan migration strategy for [site]
└─ Example: Plan migration for multi-domain e-commerce site
```

---

## 🔧 Debugging Workflows

### Tag Not Firing
```plaintext
1. "Debug [event] tag firing using Chrome DevTools"
2. Check: dataLayer push timing
3. Check: GTM trigger conditions
4. Check: Consent mode settings
5. Check: Tag firing sequence
```

### DataLayer Issues
```plaintext
1. "Inspect dataLayer structure on [page]"
2. Validate: Event naming
3. Validate: Parameter format
4. Validate: Data types
5. Test: In GTM Preview mode
```

### Conversion Tracking
```plaintext
1. "Validate conversion event in GA4 DebugView"
2. Check: Event parameters
3. Check: Conversion marking
4. Check: Attribution settings
5. Verify: In Real-Time report
```

---

## 📋 File Locations

```
.claude/
├── agents/
│   └── ga4-gtm-expert.md          # Complex implementations
└── skills/
    └── ga4-gtm.md                  # Quick tasks

Docs:
├── GA4-GTM-Expert-Usage-Guide.md   # Full usage guide
├── MCP-Servers-Installation-Guide.md # MCP setup
└── README.md                       # Overview
```

---

## 🚨 Troubleshooting Quick Fixes

### Agent/Skill Not Working
```bash
# 1. Check files
ls .claude/agents/ga4-gtm-expert.md
ls .claude/skills/ga4-gtm.md

# 2. Check MCPs
claude mcp list

# 3. Restart Claude Code
```

### Chrome DevTools Not Connecting
```bash
# Isolated mode (recommended)
claude mcp remove chrome-devtools
claude mcp add --transport stdio chrome-devtools -- npx -y chrome-devtools-mcp --isolated
```

### Context7 Not Found
```bash
# Re-add
claude mcp add --transport http context7 https://mcp.context7.com/mcp
```

### Memory Not Persisting
```bash
# Install memory MCP
claude mcp add --transport stdio memory -- npx -y @modelcontextprotocol/server-memory
```

---

## 💡 Pro Tips

### Token Optimization
```plaintext
✅ DO:
- "Use context7 for latest GA4 docs"
- Batch related events together
- Store taxonomy in Memory MCP

❌ DON'T:
- "Search web for GA4 info" (use context7)
- Make separate requests per event
- Re-explain context each time
```

### Best Request Format
```plaintext
Good: "Implement purchase event for Shopify store with dynamic product arrays and custom category parameter"

Bad: "Help with GA4"
```

### Using Memory
```plaintext
Session 1: "Store our event taxonomy in Memory"
Session 2: "Use stored taxonomy to add mobile events"
```

---

## 📊 Platform-Specific Patterns

### Web (Standard)
```plaintext
Implement [event] for vanilla JavaScript site
```

### React/Next.js
```plaintext
Implement [event] for Next.js 14 app router with virtual pageviews
```

### Server-Side GTM
```plaintext
Design server-side GTM on Cloud Run for [use case]
```

### Mobile
```plaintext
Implement [event] for iOS/Android using Firebase SDK
```

---

## 🎯 Common Event Implementations

| Event | Request Pattern |
|-------|----------------|
| **Pageview** | "Implement virtual pageview for SPA" |
| **Product View** | "Implement view_item with product details" |
| **Add to Cart** | "Implement add_to_cart with items array" |
| **Checkout** | "Implement checkout funnel events" |
| **Purchase** | "Implement purchase with transaction data" |
| **Video** | "Implement video_play tracking" |
| **Form** | "Implement form_submit tracking" |
| **Scroll** | "Implement scroll depth tracking" |

---

## 🔍 MCP Capabilities at a Glance

| MCP | What It Does | Use When |
|-----|--------------|----------|
| **context7** | Latest docs | Always (auto-used) |
| **chrome-devtools** | Browser debug | Debugging |
| **playwright** | Auto testing | Creating tests |
| **filesystem** | File ops | Saving GTM exports |
| **memory** | Persist data | Multi-session work |
| **postgres** | DB queries | BigQuery analysis |
| **fetch** | Web content | Google docs |

---

## 📞 Getting Help

```plaintext
1. Check: This quick reference
2. Read: GA4-GTM-Expert-Usage-Guide.md
3. Review: MCP-Servers-Installation-Guide.md
4. Visit: docs.claude.com/claude-code
```

---

## ⚡ One-Liners

```bash
# Check everything is ready
claude mcp list && ls .claude/agents/ && ls .claude/skills/

# Quick MCP install (filesystem + memory)
claude mcp add --transport stdio filesystem -- npx -y @modelcontextprotocol/server-filesystem ~/Documents/GA4 && claude mcp add --transport stdio memory -- npx -y @modelcontextprotocol/server-memory

# Backup config
cp ~/.claude.json ~/.claude.json.backup
```

---

## 🎓 Learning Path

1. ✅ Install MCPs (context7, chrome-devtools, playwright)
2. 📖 Read GA4-GTM-Expert-Usage-Guide.md intro
3. 🎯 Try simple event implementation (skill)
4. 🔧 Try debugging with Chrome DevTools
5. 🚀 Tackle complex migration (agent)
6. 💡 Add filesystem + memory MCPs
7. 📊 Try BigQuery pipeline (agent + postgres)

---

**Print this page and keep it handy! 📋**

[Back to README](README.md) | [Full Guide](GA4-GTM-Expert-Usage-Guide.md) | [MCP Guide](MCP-Servers-Installation-Guide.md)
