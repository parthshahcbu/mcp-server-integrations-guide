# Google Analytics 4 & Google Tag Manager Expert - Usage Guide

> **Advanced Implementation Guide for GA4/GTM Sub Agent & Skill**
>
> Last Updated: October 31, 2025
> Target Audience: Advanced Analytics Professionals & Developers

---

## Table of Contents

1. [Overview](#overview)
2. [Quick Start](#quick-start)
3. [Sub Agent vs Skill - When to Use Which](#sub-agent-vs-skill---when-to-use-which)
4. [MCP Server Requirements](#mcp-server-requirements)
5. [Usage Examples](#usage-examples)
6. [Common Use Cases](#common-use-cases)
7. [Best Practices](#best-practices)
8. [Advanced Workflows](#advanced-workflows)
9. [Troubleshooting](#troubleshooting)

---

## Overview

The GA4/GTM Expert system consists of two components:

### 1. Sub Agent (`.claude/agents/ga4-gtm-expert.md`)
- **Type**: Autonomous agent for complex, multi-step tasks
- **Best For**: Large implementations, migrations, architecture design
- **Invocation**: Via Task tool or direct agent invocation
- **Capabilities**: Full autonomous operation with planning and execution

### 2. Skill (`.claude/skills/ga4-gtm.md`)
- **Type**: Specialized skill for quick, focused tasks
- **Best For**: Specific implementations, debugging, documentation
- **Invocation**: Via Skill tool
- **Capabilities**: Targeted expertise on demand

---

## Quick Start

### Prerequisites

Ensure you have the following MCPs installed (see [MCP Setup](#mcp-server-requirements)):
- ✅ **context7** (required) - For GA4/GTM documentation
- ✅ **chrome-devtools** (recommended) - For debugging
- ✅ **playwright** (recommended) - For testing
- ⚪ **filesystem** (optional) - For GTM container management
- ⚪ **git/github** (optional) - For version control

### Installation Verification

```bash
# Check if the files exist
ls -la .claude/agents/ga4-gtm-expert.md
ls -la .claude/skills/ga4-gtm.md

# Verify MCP servers
claude mcp list
```

---

## Sub Agent vs Skill - When to Use Which

### Use the Sub Agent When:

✅ **Complex Multi-Step Projects**
- Complete GA4 implementation from scratch
- Full UA to GA4 migration
- Enterprise-wide GTM architecture redesign
- Multi-platform tracking strategy (web + mobile + server-side)

✅ **Planning & Roadmapping**
- Creating implementation roadmaps
- Designing event taxonomy for large organizations
- Planning data pipeline architectures
- Stakeholder presentations and documentation

✅ **Autonomous Execution Needed**
- You need the agent to work independently
- Multiple related tasks that require decision-making
- Complex debugging that requires exploration

**Example Invocation:**
```plaintext
You: I need to plan and execute a complete GA4 migration from Universal Analytics for our e-commerce site. We have 50+ custom events, 3 domains, and need server-side GTM.

Claude: I'll use the Task tool to invoke the ga4-gtm-expert sub agent...
```

### Use the Skill When:

✅ **Specific, Focused Tasks**
- Implementing a single custom event
- Debugging a specific tag firing issue
- Creating dataLayer documentation
- Writing GTM variables/triggers

✅ **Quick Assistance**
- Code review for tracking implementation
- Generating test plans
- Answering specific technical questions
- Creating code snippets

✅ **Interactive Guidance**
- You want step-by-step guidance
- You need to provide input during the process
- Quick consultations

**Example Invocation:**
```plaintext
You: /ga4-gtm (if set up as slash command)
OR
You: Use the ga4-gtm skill to help me implement a custom checkout event

Claude: I'll invoke the ga4-gtm skill to help...
```

---

## MCP Server Requirements

### Required MCPs

#### 1. Context7 (Already Installed ✅)
**Purpose**: Retrieve latest GA4/GTM documentation

**Usage**: Automatic - the agent/skill will use this to fetch current best practices

**Verification**:
```bash
claude mcp list | grep context7
```

### Highly Recommended MCPs

#### 2. Chrome DevTools (Already Installed ✅)
**Purpose**: Debug GTM containers, inspect dataLayer, validate tag firing

**Usage**: For debugging and testing implementations

**Why Essential for GA4/GTM**:
- Inspect `window.dataLayer` in real-time
- Monitor `gtag()` calls
- Validate Measurement Protocol requests
- Debug consent mode implementation

**Example Usage with Agent**:
```plaintext
You: Debug why my purchase event isn't firing in GTM

Agent: I'll use Chrome DevTools MCP to inspect your dataLayer and tag firing...
```

#### 3. Playwright (Already Installed ✅)
**Purpose**: Automated testing of tracking implementations

**Usage**: End-to-end testing of event tracking

**Why Essential for GA4/GTM**:
- Automated QA for tracking implementations
- Cross-browser testing
- User journey simulation
- Screenshot validation

**Example Usage with Agent**:
```plaintext
You: Create an automated test for our checkout funnel tracking

Agent: I'll use Playwright to create a test that validates all checkout events...
```

#### 4. Firecrawl (Already Installed ✅)
**Purpose**: Scrape competitor tracking implementations, analyze GTM setups

**Usage**: Research and competitive analysis

**Example Usage**:
```plaintext
You: Analyze how competitor.com implements their e-commerce tracking

Agent: I'll use Firecrawl to extract their GTM implementation...
```

### Optional But Useful MCPs

#### 5. Filesystem
**Purpose**: Manage GTM container export files, save documentation

**Installation**:
```bash
# Allow access to your project directory
claude mcp add --transport stdio filesystem -- npx -y @modelcontextprotocol/server-filesystem ~/Documents/GA4-Projects
```

**Why Useful**:
- Version control GTM container exports (JSON)
- Store dataLayer specifications
- Manage event taxonomy documents

#### 6. GitHub
**Purpose**: Version control for GTM configurations and tracking code

**Installation**:
```bash
# Replace YOUR_GITHUB_TOKEN
claude mcp add --transport stdio github --env GITHUB_TOKEN=YOUR_GITHUB_TOKEN -- npx -y @modelcontextprotocol/server-github
```

**Why Useful**:
- Track changes to GTM containers
- Collaborate on tracking implementations
- Automated deployment workflows

#### 7. Memory
**Purpose**: Store event taxonomies and configuration specs across sessions

**Installation**:
```bash
claude mcp add --transport stdio memory -- npx -y @modelcontextprotocol/server-memory
```

**Why Useful**:
- Remember your event taxonomy
- Recall GTM container structures
- Maintain context across multiple sessions

#### 8. PostgreSQL
**Purpose**: Analyze GA4 BigQuery export data

**Installation**:
```bash
# Replace with your connection string
claude mcp add --transport stdio postgres --env POSTGRES_CONNECTION_STRING="postgresql://user:password@localhost:5432/ga4_data" -- npx -y @modelcontextprotocol/server-postgres
```

**Why Useful**:
- Query GA4 BigQuery exports
- Build custom reports
- Data validation and quality checks

#### 9. Fetch
**Purpose**: Retrieve Google documentation and resources

**Installation**:
```bash
claude mcp add --transport stdio fetch -- npx -y @modelcontextprotocol/server-fetch
```

**Why Useful**:
- Fetch latest Google documentation
- Access GTM template gallery
- Retrieve measurement protocol specs

---

## Usage Examples

### Example 1: Implementing Custom E-commerce Tracking

#### Using the Skill (Quick Implementation)

```plaintext
You: I need to implement a custom "add_to_wishlist" event with product details

Claude (with ga4-gtm skill): I'll help you implement the add_to_wishlist event. Here's the implementation:

[Provides complete dataLayer code, GTM configuration, and testing steps]
```

**What the Skill Does**:
1. Uses context7 to get latest GA4 e-commerce spec
2. Generates dataLayer push code
3. Provides GTM tag configuration
4. Creates testing checklist

#### Using the Sub Agent (Complete Implementation)

```plaintext
You: Plan and implement a complete enhanced e-commerce tracking system including all funnel events, product impressions, and checkout tracking

Claude: I'll invoke the ga4-gtm-expert sub agent to handle this comprehensive implementation...

Sub Agent:
1. Analyzes your current implementation (if requested)
2. Designs complete event taxonomy
3. Creates dataLayer specification document
4. Implements all tracking code
5. Configures GTM container
6. Creates testing plan
7. Generates stakeholder documentation
```

**What the Sub Agent Does**:
1. **Planning Phase**: Creates implementation roadmap
2. **Design Phase**: Designs event taxonomy and dataLayer architecture
3. **Implementation Phase**: Writes all code and GTM configurations
4. **Testing Phase**: Uses Playwright to create automated tests
5. **Documentation Phase**: Creates developer docs and stakeholder reports

---

### Example 2: Debugging Tag Firing Issues

#### Using the Skill

```plaintext
You: My purchase event fires on preview but not in production

Claude (with ga4-gtm skill): Let me help debug this. I'll guide you through:

1. Check GTM trigger conditions
2. Validate dataLayer timing
3. Inspect consent mode settings
4. Review tag firing sequence

[Provides step-by-step debugging checklist]
```

#### Using the Sub Agent with Chrome DevTools

```plaintext
You: Debug my entire checkout funnel - multiple events aren't firing correctly

Claude: I'll invoke the ga4-gtm-expert sub agent with Chrome DevTools access...

Sub Agent:
1. Uses Chrome DevTools MCP to inspect live dataLayer
2. Validates tag firing sequence
3. Checks network requests to GA4
4. Identifies timing issues
5. Provides fix recommendations with code
6. Creates testing plan to prevent regression
```

---

### Example 3: UA to GA4 Migration

#### Complex Migration (Use Sub Agent)

```plaintext
You: We need to migrate from Universal Analytics to GA4. We have:
- 50+ custom events
- 3 cross-domain sites
- Custom dimensions and metrics
- E-commerce tracking
- Custom JavaScript tracking

Claude: This is a complex migration. I'll invoke the ga4-gtm-expert sub agent...

Sub Agent will:
1. **Audit Phase**:
   - Analyze current UA implementation
   - Map UA events to GA4 events
   - Identify gaps and opportunities

2. **Strategy Phase**:
   - Design GA4 event taxonomy
   - Plan parallel tracking setup (UA + GA4)
   - Create migration timeline

3. **Implementation Phase**:
   - Configure GA4 property
   - Implement GA4 tracking code
   - Set up custom dimensions/metrics
   - Configure e-commerce tracking

4. **Testing Phase**:
   - Parallel tracking validation
   - Data comparison reports
   - Automated testing suite

5. **Documentation Phase**:
   - Migration documentation
   - Training materials
   - Stakeholder reports
```

---

### Example 4: Creating DataLayer Documentation

#### Using the Skill (Single Page/Event)

```plaintext
You: Create dataLayer documentation for our product detail page

Claude (with ga4-gtm skill): I'll create comprehensive dataLayer documentation:

[Generates markdown documentation with:
- Event specifications
- Code examples
- Testing requirements
- Implementation notes]
```

#### Using the Sub Agent (Complete System)

```plaintext
You: Create complete dataLayer documentation for our entire e-commerce site

Sub Agent will:
1. Analyze all pages and user journeys
2. Design comprehensive event taxonomy
3. Create detailed dataLayer specification
4. Generate developer implementation guide
5. Create QA testing procedures
6. Generate stakeholder summary
```

---

### Example 5: Server-Side GTM Implementation

```plaintext
You: Set up server-side Google Tag Manager with first-party data collection

Claude: I'll invoke the ga4-gtm-expert sub agent for this complex implementation...

Sub Agent will:
1. **Architecture Design**:
   - Design server-side GTM architecture
   - Plan cloud infrastructure (Cloud Run/App Engine)
   - Define data enrichment strategy

2. **Implementation**:
   - Set up server-side GTM container
   - Configure web container to send to server
   - Implement server-side tags
   - Set up custom transformations

3. **Testing**:
   - Validate request routing
   - Test data enrichment
   - Performance testing

4. **Documentation**:
   - Architecture diagrams
   - Deployment guides
   - Monitoring setup
```

---

### Example 6: BigQuery Data Pipeline

```plaintext
You: Create a data pipeline that combines GA4 BigQuery exports with our CRM data and visualizes in Looker Studio

Claude: This requires the ga4-gtm-expert sub agent with PostgreSQL MCP...

Sub Agent will:
1. **GA4 Setup**:
   - Configure BigQuery export
   - Optimize schema design
   - Set up data streaming

2. **Pipeline Design**:
   - Design ETL/ELT process
   - Plan data warehouse schema
   - Create data transformation logic

3. **Implementation**:
   - Write SQL queries for data processing
   - Set up scheduled jobs
   - Implement data quality checks

4. **Visualization**:
   - Design Looker Studio dashboards
   - Create calculated fields
   - Set up data blending

5. **Documentation**:
   - Data pipeline documentation
   - Looker Studio user guides
   - Maintenance procedures
```

---

## Common Use Cases

### Use Case Matrix

| Task | Use Skill | Use Sub Agent | Key MCPs Needed |
|------|-----------|---------------|-----------------|
| Implement single custom event | ✅ | ⚪ | context7 |
| Debug tag firing issue | ✅ | ⚪ | chrome-devtools |
| Create event taxonomy | ⚪ | ✅ | context7, memory |
| Complete GA4 setup | ⚪ | ✅ | context7, filesystem |
| UA to GA4 migration | ⚪ | ✅ | context7, memory, git |
| DataLayer docs (single page) | ✅ | ⚪ | context7, filesystem |
| DataLayer docs (entire site) | ⚪ | ✅ | context7, filesystem, memory |
| E-commerce tracking | ✅ | ⚪ | context7 |
| Server-side GTM setup | ⚪ | ✅ | context7, filesystem |
| Consent mode implementation | ✅ | ⚪ | context7, chrome-devtools |
| BigQuery pipeline | ⚪ | ✅ | context7, postgres |
| Looker Studio dashboard | ⚪ | ✅ | context7 |
| GTM container audit | ⚪ | ✅ | chrome-devtools, filesystem |
| Testing implementation | ✅ | ⚪ | playwright |
| Automated test suite | ⚪ | ✅ | playwright, filesystem |

---

## Best Practices

### 1. Be Specific in Your Requests

❌ **Vague**:
```plaintext
Help me with GA4
```

✅ **Specific**:
```plaintext
Help me implement purchase event tracking for a Shopify store with dynamic product arrays and custom parameters for product categories
```

### 2. Provide Context

✅ **Good Request**:
```plaintext
I need to implement scroll tracking. We're using:
- React 18 with Next.js 14
- GTM web container
- Consent Mode v2 (Google CMP)
- Want to track 25%, 50%, 75%, 100% scroll depth

Current issue: Events firing multiple times on scroll
```

### 3. Specify Your Environment

Include:
- Platform (web, mobile, server-side)
- Framework (React, Vue, Angular, vanilla JS)
- GTM container type
- Consent mode setup
- Privacy requirements (GDPR, CCPA)

### 4. Use MCPs Effectively

When asking for debugging:
```plaintext
Use Chrome DevTools to inspect my dataLayer on the checkout page and validate the purchase event
```

When asking for testing:
```plaintext
Use Playwright to create an automated test for the add-to-cart event that validates the items array structure
```

### 5. Request Documentation

Always ask for documentation alongside implementation:
```plaintext
Implement enhanced e-commerce tracking and create developer documentation with code examples and testing procedures
```

### 6. Leverage Memory MCP

For ongoing projects:
```plaintext
Store our event taxonomy in Memory so we can reference it in future sessions

Later session:
Retrieve our event taxonomy from Memory and add mobile app events to it
```

---

## Advanced Workflows

### Workflow 1: Complete GA4 Implementation (Enterprise)

```plaintext
Phase 1 - Discovery (Sub Agent):
You: Analyze our current tracking setup and create a GA4 implementation roadmap

Phase 2 - Event Design (Sub Agent):
You: Design a comprehensive event taxonomy following Google's recommended events and add our custom business events

Phase 3 - DataLayer Spec (Sub Agent):
You: Create complete dataLayer specification documentation for our development team

Phase 4 - Implementation (Iterative with Skill):
You (using Skill): Implement product_view event
You (using Skill): Implement add_to_cart event
You (using Skill): Implement checkout events
[Continue for each event]

Phase 5 - Testing (Sub Agent):
You: Create automated test suite using Playwright for all tracking events

Phase 6 - Validation (Skill + Chrome DevTools):
You: Validate all events are firing correctly using Chrome DevTools

Phase 7 - Documentation (Sub Agent):
You: Create stakeholder presentation showing implementation status and data quality metrics
```

### Workflow 2: Debugging Production Issues

```plaintext
Step 1 - Initial Analysis (Skill):
You: My conversion events dropped 50% yesterday. Help me identify potential causes.

Step 2 - Live Debugging (Sub Agent + Chrome DevTools):
You: Use Chrome DevTools to inspect the live site and identify why conversion events aren't firing

Step 3 - Fix Implementation (Skill):
You: Implement the fix for [specific issue found]

Step 4 - Testing (Skill + Playwright):
You: Create a test to prevent this issue from happening again

Step 5 - Monitoring (Skill):
You: Help me set up alerts in GA4 for event volume drops
```

### Workflow 3: Server-Side GTM + Data Pipeline

```plaintext
Phase 1 - Architecture (Sub Agent):
You: Design server-side GTM architecture on Google Cloud Run with first-party data collection

Phase 2 - Server Container (Sub Agent):
You: Implement server-side GTM container with data enrichment from our CRM API

Phase 3 - Web Container Update (Skill):
You: Update web GTM container to send data to server container

Phase 4 - BigQuery Setup (Sub Agent):
You: Configure GA4 BigQuery export and design optimal schema

Phase 5 - Data Pipeline (Sub Agent + PostgreSQL):
You: Create data pipeline that combines GA4 BigQuery data with CRM data in our warehouse

Phase 6 - Visualization (Sub Agent):
You: Design Looker Studio dashboard with blended data sources

Phase 7 - Documentation (Sub Agent):
You: Create complete technical documentation for the entire data pipeline
```

---

## Troubleshooting

### Agent/Skill Not Working?

#### Check 1: Files Exist
```bash
ls -la .claude/agents/ga4-gtm-expert.md
ls -la .claude/skills/ga4-gtm.md
```

#### Check 2: MCP Servers Connected
```bash
claude mcp list
```

Should show:
- ✓ context7
- ✓ chrome-devtools (optional but recommended)
- ✓ playwright (optional but recommended)

#### Check 3: Invoke Correctly

**For Skill**:
```plaintext
Use the ga4-gtm skill to [your request]
```

**For Sub Agent**:
```plaintext
Use the Task tool to invoke ga4-gtm-expert sub agent to [your request]
```

Or let Claude decide which to use by providing a clear, specific request.

### Common Issues

#### Issue: "Agent doesn't have latest GA4 features"

**Solution**: context7 MCP automatically fetches latest documentation. Ensure it's connected:
```bash
claude mcp list | grep context7
```

#### Issue: "Can't debug dataLayer in browser"

**Solution**: Install Chrome DevTools MCP:
```bash
claude mcp add --transport stdio chrome-devtools -- npx -y chrome-devtools-mcp --isolated
```

#### Issue: "Can't save GTM container exports"

**Solution**: Install Filesystem MCP:
```bash
claude mcp add --transport stdio filesystem -- npx -y @modelcontextprotocol/server-filesystem ~/Documents/GTM-Configs
```

#### Issue: "Loses context between sessions"

**Solution**: Install Memory MCP:
```bash
claude mcp add --transport stdio memory -- npx -y @modelcontextprotocol/server-memory
```

---

## Quick Command Reference

### Invoke the Skill
```plaintext
# Direct invocation
Use the ga4-gtm skill to implement purchase event tracking

# Let Claude decide
I need to implement a custom event for video tracking
```

### Invoke the Sub Agent
```plaintext
# Explicit invocation
Use the Task tool to invoke the ga4-gtm-expert sub agent to plan and execute our GA4 migration

# Let Claude decide
We need a complete GA4 implementation with server-side GTM, BigQuery exports, and Looker Studio dashboards
```

### Common Requests

**Implementation**:
```plaintext
Implement [event name] tracking for [platform] using [framework]
```

**Debugging**:
```plaintext
Debug [specific issue] using Chrome DevTools
```

**Documentation**:
```plaintext
Create dataLayer documentation for [page/section]
```

**Testing**:
```plaintext
Create Playwright test for [event/funnel]
```

**Migration**:
```plaintext
Migrate from UA to GA4 for [site description]
```

**Architecture**:
```plaintext
Design [server-side GTM/data pipeline] architecture for [use case]
```

---

## MCP Setup Quick Reference

### Essential Setup (5 minutes)
```bash
# Already installed - verify:
claude mcp list
```

Should have:
- ✓ context7
- ✓ chrome-devtools
- ✓ playwright

### Recommended Setup (10 minutes)
```bash
# Add filesystem for GTM container management
claude mcp add --transport stdio filesystem -- npx -y @modelcontextprotocol/server-filesystem ~/Documents/GA4-Projects

# Add memory for session persistence
claude mcp add --transport stdio memory -- npx -y @modelcontextprotocol/server-memory

# Add fetch for Google docs
claude mcp add --transport stdio fetch -- npx -y @modelcontextprotocol/server-fetch
```

### Advanced Setup (20 minutes)
```bash
# Add GitHub for version control
claude mcp add --transport stdio github --env GITHUB_TOKEN=YOUR_TOKEN -- npx -y @modelcontextprotocol/server-github

# Add PostgreSQL for BigQuery analysis
claude mcp add --transport stdio postgres --env POSTGRES_CONNECTION_STRING="postgresql://user:pass@localhost:5432/ga4" -- npx -y @modelcontextprotocol/server-postgres
```

---

## Examples by Platform

### Web (Standard JavaScript)
```plaintext
Implement GA4 pageview tracking with custom dimensions for our marketing site
```

### React/Next.js SPA
```plaintext
Implement virtual pageview tracking for Next.js 14 app router with dynamic route parameters
```

### Server-Side GTM
```plaintext
Design and implement server-side GTM architecture on Cloud Run for enhanced privacy and performance
```

### Mobile Apps (Firebase)
```plaintext
Implement GA4 SDK tracking for iOS app with custom events and user properties
```

---

## Token Optimization Tips

### Use MCPs Efficiently
✅ **Do**: "Use context7 to get latest GA4 e-commerce spec"
❌ **Don't**: "Search the web for GA4 documentation"

### Batch Related Requests
✅ **Do**: "Implement all checkout funnel events (begin_checkout, add_payment_info, add_shipping_info, purchase)"
❌ **Don't**: Make separate requests for each event

### Use Memory for Repeated Context
✅ **Do**: "Store our event taxonomy in Memory"
Then later: "Use our stored event taxonomy to add mobile events"
❌ **Don't**: Re-explain your event taxonomy each session

---

## Additional Resources

### Google Official Documentation
- GA4 Documentation: https://support.google.com/analytics/topic/9143232
- GTM Documentation: https://support.google.com/tagmanager
- Measurement Protocol: https://developers.google.com/analytics/devguides/collection/protocol/ga4

### Community Resources
- GTM Template Gallery: https://tagmanager.google.com/gallery/
- Simo Ahava's Blog: https://www.simoahava.com/
- Analytics Mania: https://www.analyticsmania.com/

### Tools
- GA4 DebugView: In GA4 Admin → DebugView
- Tag Assistant: Chrome extension
- Google Analytics Debugger: Chrome extension

---

## Support & Feedback

### Getting Help

If you encounter issues:
1. Check this guide's [Troubleshooting](#troubleshooting) section
2. Verify MCP connections: `claude mcp list`
3. Review the [MCP Installation Guide](MCP-Servers-Installation-Guide.md)
4. Check [Claude Code documentation](https://docs.claude.com/claude-code)

### Contributing

Found an issue or have suggestions? Update the agent/skill files:
- `.claude/agents/ga4-gtm-expert.md`
- `.claude/skills/ga4-gtm.md`

---

## Quick Start Checklist

- [ ] Verify sub agent file exists (`.claude/agents/ga4-gtm-expert.md`)
- [ ] Verify skill file exists (`.claude/skills/ga4-gtm.md`)
- [ ] Verify context7 MCP connected
- [ ] Install Chrome DevTools MCP (recommended)
- [ ] Install Playwright MCP (recommended)
- [ ] Install filesystem MCP (for GTM exports)
- [ ] Install memory MCP (for session persistence)
- [ ] Test skill with simple request
- [ ] Test sub agent with complex request

---

**Happy Tracking! 🎯📊**

For the latest Google Analytics 4 and GTM features, the agent/skill will automatically use context7 to fetch current documentation.
