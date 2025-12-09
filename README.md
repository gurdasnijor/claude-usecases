# Claude Use Cases & Skills

[![Run in Smithery](https://smithery.ai/badge/skills/therealchandlerbing)](https://smithery.ai/skills?ns=therealchandlerbing&utm_source=github&utm_medium=badge)


**Comprehensive AI skill library for specialized workflows** | 20+ Managed Skills | 15 Categories | Production-Ready

![status](https://img.shields.io/badge/status-production--ready-brightgreen)
![skills](https://img.shields.io/badge/skills-20%2B%20managed-blue)
![coverage](https://img.shields.io/badge/coverage-99%25%20financial-green)
![content](https://img.shields.io/badge/content-8700%2B%20lines-purple)

A comprehensive collection of use cases and skills that can be deployed with Claude for specialized workflows and automation. This repository provides structured, reusable skill files optimized for various business and technical use cases.

## Overview

This repository contains:
- **Skill Templates** - Standardized templates for creating new skills
- **360 Use Cases** - Customized workflows for 360-specific processes
- **Documentation** - Guides for creating and using skills
- **Examples** - Sample implementations to get started

## Repository Structure

```
claude-usecases/
├── .claude/
│   └── skills/                  # Managed Claude skills
│       ├── 360-client-portfolio-builder/   # Client venture portfolio page generator
│       ├── 360-executive-project-tracker/  # Multi-source project status tracking
│       ├── ai-ethics-advisor/              # AI ethics, bias assessment & responsible AI
│       ├── ceo-advisor/                    # Executive advisory board & decision support (v2.0)
│       ├── contract-redlining-tool/        # Automated contract review & redlining
│       ├── executive-impact-presentation-generator/  # Board-ready impact report generation
│       ├── executive-intelligence-dashboard/  # Executive intelligence briefing system
│       ├── fda-consultant-agent/           # FDA regulatory consulting
│       ├── intelligence-extractor/         # Partnership & funding intelligence extraction
│       ├── open-deep-research-team/        # Multi-agent comprehensive research system
│       ├── sales-automator/                # Intelligent sales automation & pipeline tracking
│       ├── skill-orchestrator/             # Universal workflow coordinator for multi-skill/agent operations
│       ├── 360-newsletter-generator/       # Board updates & investor briefings
│       ├── 360-proposal-builder/           # Executive proposal generation for innovation services
│       ├── design-director/                # Design elevation & visual polish
│       ├── financial-modeling-skills/      # Investment analysis & portfolio intelligence
│       ├── strategic-persona-builder/      # Multi-framework persona generation & validation
│       ├── workflow-debugging/             # Systematic workflow debugging & recovery
│       └── workflow-process-generator/     # Workflow visualization & process documentation
├── 360-board-meeting-prep/      # Board meeting intelligence system & packet generator
├── skills/                      # User-created skills
│   ├── 360-content-converter/   # Multi-platform content conversion
│   ├── 360-use-cases/           # 360-specific workflow skills (organizational directory)
│   └── 990-ez-preparation/      # IRS Form 990-EZ automated preparation (99% test coverage)
├── templates/                   # Production-ready HTML templates
│   └── impact-reports/          # Executive impact report templates (static & dynamic)
├── intelligence-dashboard/      # Live quality monitoring dashboard (Next.js app)
├── tests/                       # Comprehensive test suite (Python & TypeScript)
├── docs/                        # Documentation and guides
│   ├── pr-descriptions/         # Pull request templates and descriptions
│   └── summaries/               # Feature and implementation summaries
└── examples/                    # Example implementations
```

## Quick Start

### Using an Existing Skill

1. Browse the skills by category below
2. Click the README link to view complete documentation
3. Follow the quick start guide for each skill

### Creating a New Skill

1. Copy the template: `cp skills/templates/skill-template.md skills/your-skill-name.md`
2. Customize with your specific use case
3. Follow the guidelines in `docs/CREATING-SKILLS.md`

---

## Slash Commands

Quick shortcuts for invoking skills. Use these instead of typing full trigger phrases.

### Single-Skill Commands

| Category | Command | Skill | Description |
|----------|---------|-------|-------------|
| **Executive** | `/brief` | ceo-advisor | Daily CEO intelligence brief |
| | `/weekly-brief` | executive-intelligence-dashboard | Weekly 360 Impact Brief |
| | `/board-prep` | 360-board-meeting-prep | Board meeting packet generation |
| | `/impact-report` | executive-impact-presentation-generator | Board-ready impact reports |
| | `/newsletter` | 360-newsletter-generator | Executive briefs & newsletters |
| **Research** | `/research` | open-deep-research-team | Multi-agent deep research |
| | `/persona` | strategic-persona-builder | Stakeholder personas |
| **Sales/BD** | `/outreach` | sales-automator | Sales email sequences |
| | `/proposal` | 360-proposal-builder | Client proposals |
| | `/redline` | contract-redlining-tool | Contract review & redlining |
| | `/portfolio` | 360-client-portfolio-builder | Venture portfolio pages |
| **Financial** | `/finance` | financial-modeling-skills | Investment & SROI analysis |
| **Design** | `/elevate` | design-director | Professional design polish |
| **Data** | `/extract` | intelligence-extractor | Extract intelligence from content |
| | `/tracker` | 360-executive-project-tracker | Project status dashboards |
| **Healthcare** | `/fda` | fda-consultant-agent | FDA regulatory guidance |
| **AI Ethics** | `/ethics` | ai-ethics-advisor | Bias assessment & AI compliance |
| **Process** | `/sop` | workflow-process-generator | SOPs & process documentation |
| | `/debug` | workflow-debugging | Workflow debugging |
| | `/orchestrate` | skill-orchestrator | Multi-skill coordination |
| **Catalog** | `/skills` | — | Browse all available skills |

### Workflow Templates

Pre-built multi-skill sequences for common routines:

| Command | Workflow | Skills Chained | Time |
|---------|----------|----------------|------|
| `/morning` | Morning executive startup | ceo-advisor → intelligence-extractor → tracker | 20-40 min |
| `/weekly-review` | End-of-week review & planning | 4 skills | 45-75 min |
| `/meeting-wrap` | Post-meeting intelligence capture | 3 skills | 10-30 min |
| `/client-onboard` | New client engagement prep | research → persona → proposal → outreach | 60-120 min |
| `/partnership-eval` | Partnership due diligence | 5 skills | 90-120 min |
| `/deal-review` | Contract + financial evaluation | redline → finance → ceo-advisor | 60-90 min |
| `/venture-launch` | Complete launch package | 5 skills | 4-8 hours |
| `/quarterly-report` | Quarterly board materials | 4 skills | 3-4 hours |
| `/research-brief` | Research to executive presentation | 5 skills | 45 min - 3 hrs |
| `/compliance-audit` | Ethics + process documentation | 4 skills | 3-6 hours |

### Usage

Both methods work interchangeably:
```
/brief                                    # Slash command
"Generate my morning executive brief"     # Natural language
```

**Location:** `.claude/commands/`

---

## Available Skills

### Healthcare & Life Sciences Regulatory

#### FDA Consultant Agent
**Location:** `.claude/skills/fda-consultant-agent/`
**Purpose:** Expert FDA regulatory guidance for medical devices, pharmaceuticals, biologics, and combination products with 100% citation accuracy.

**Quick Links:** [README](.claude/skills/fda-consultant-agent/README.md) ⭐ | [Quick Start](.claude/skills/fda-consultant-agent/QUICK-START.md) | [Skill Spec](.claude/skills/fda-consultant-agent/SKILL.md)

**When to Use:**
- FDA pathway selection and product classification (510(k), PMA, IND, NDA, BLA)
- Quality system compliance (QSR, cGMP, ISO 13485)
- Clinical trial design and regulatory strategy
- Software as Medical Device (SaMD) and AI/ML regulatory frameworks

---

### AI Governance & Responsible AI

#### AI Ethics Advisor
**Location:** `.claude/skills/ai-ethics-advisor/`
**Purpose:** Comprehensive AI ethics and responsible AI development specialist for bias assessment, fairness evaluation, ethical AI implementation, community impact analysis, and regulatory compliance. Expert in AI safety, alignment, and equitable systems design.

**Quick Links:** [README](.claude/skills/ai-ethics-advisor/README.md) ⭐ | [Quick Start](.claude/skills/ai-ethics-advisor/QUICK-START.md) | [Skill Spec](.claude/skills/ai-ethics-advisor/SKILL.md) | [Assessment Templates](.claude/skills/ai-ethics-advisor/ASSESSMENT-TEMPLATES.md)

**When to Use:**
- Bias assessment and fairness evaluation for AI systems
- Ethical AI implementation guidance and frameworks
- Community impact analysis for AI deployments
- Regulatory compliance (EU AI Act, NIST AI RMF, sectoral requirements)
- High-risk AI systems affecting employment, lending, healthcare, or criminal justice
- Algorithmic audits and responsible AI development

---

### Research & Validation

#### Open Deep Research Team
**Location:** `.claude/skills/open-deep-research-team/`
**Purpose:** Sophisticated multi-agent AI research system conducting comprehensive, academic-quality research through orchestrated specialist agents. Combines academic, technical, and data-driven perspectives with rigorous quality assurance and comprehensive reporting.

**Quick Links:** [README](.claude/skills/open-deep-research-team/README.md) ⭐ | [Quick Start](.claude/skills/open-deep-research-team/QUICK-START.md) | [Implementation Guide](.claude/skills/open-deep-research-team/IMPLEMENTATION-GUIDE.md) | [Agent Prompts](.claude/skills/open-deep-research-team/prompts/)

**When to Use:**
- Conducting comprehensive research on complex topics requiring multiple perspectives
- Academic literature reviews and state-of-the-art analysis
- Technical evaluations with implementation details and code examples
- Market research and competitive intelligence with proper citations
- Business intelligence requiring academic rigor and data validation
- Research reports with executive summaries and actionable recommendations

#### Strategic Persona Builder
**Location:** `.claude/skills/strategic-persona-builder/`
**Purpose:** Generate evidence-backed stakeholder personas from research data using structured frameworks (Vianeo, Jobs-to-be-Done, empathy mapping). Supports partners, innovators, stakeholders, beneficiaries, and customers with dual outputs for strategy and platform entry.

**Quick Links:** [README](.claude/skills/strategic-persona-builder/README.md) ⭐ | [Quick Start](.claude/skills/strategic-persona-builder/QUICK-START.md) | [Skill Spec](.claude/skills/strategic-persona-builder/SKILL.md) | [Scoring Rubric](.claude/skills/strategic-persona-builder/references/scoring-rubric.md)

**When to Use:**
- Building personas for technology validation projects (Vianeo submissions)
- Product development with Jobs-to-be-Done analysis
- Team alignment with empathy mapping
- Partnership development and stakeholder documentation
- Research planning with hypothesis personas and validation questions

---

### Design & Visual Excellence

#### Design Director
**Location:** `.claude/skills/design-director/`
**Purpose:** Transform functional outputs (presentations, dashboards, HTML interfaces, reports) into professionally polished, design-elevated work through systematic application of proven techniques and world-class exemplars (Stripe, Linear, Apple).

**Quick Links:** [README](.claude/skills/design-director/README.md) ⭐ | [Quick Start](.claude/skills/design-director/QUICK-START.md) | [Skill Spec](.claude/skills/design-director/SKILL.md) | [Technique Catalog](.claude/skills/design-director/references/technique-catalog.md)

**When to Use:**
- Elevating dashboards, presentations, and reports to professional design quality
- Building web interfaces that match Stripe/Linear/Apple standards
- Ensuring visual consistency, WCAG AA accessibility, and hand-crafted appearance
- Making data-heavy outputs scannable and beautiful with exemplar-aligned quality

---

### Content Strategy & Multi-Platform Publishing

#### 360 Content Converter
**Location:** `skills/360-content-converter/`
**Purpose:** Transform one piece of content into multiple platform-optimized formats while maintaining brand consistency across 15+ platforms and 3 languages.

**Quick Links:** [README](skills/360-content-converter/README.md) ⭐ | [Prompt Templates](skills/360-content-converter/references/prompt-templates.md) | [Quality Checklist](skills/360-content-converter/references/quality-checklist.md)

**When to Use:**
- Repurposing content across multiple platforms (social, email, blog, presentations)
- Adapting content for different audiences and languages with cultural intelligence
- Building cohesive content ecosystems with strategic sequencing
- Creating design-ready specifications for visual content

---

### Data Intelligence & Quality Monitoring

#### Intelligence Extractor
**Location:** `.claude/skills/intelligence-extractor/`
**Purpose:** Extract structured partnership, funding, and stakeholder intelligence from meeting transcripts with real-time quality monitoring.

**Quick Links:** [README](.claude/skills/intelligence-extractor/README.md) ⭐ | [Skill Spec](.claude/skills/intelligence-extractor/SKILL.md) | [Template Selection Guide](.claude/skills/intelligence-extractor/templates/00-template-selection-guide.md)

**When to Use:**
- Extracting intelligence from partnership, funder, board, or stakeholder meetings
- Monitoring extraction quality and template performance with real-time analytics
- Cross-cultural meeting intelligence and community engagement documentation
- Building interconnected Partnership, Funding, and Stakeholder intelligence systems

#### Partnership Intelligence Dashboard
**Location:** `intelligence-dashboard/src/components/partnership/`
**Purpose:** Professional dashboard for navigating partnership conversations with data-driven intelligence from 40+ historical partnerships across 4 partner types.

**Quick Links:** [README](intelligence-dashboard/src/components/partnership/README.md) ⭐ | [Summary](PARTNERSHIP_DASHBOARD_SUMMARY.md) | [Dashboard Demo](intelligence-dashboard/README.md)

**When to Use:**
- Preparing for partnership conversations and qualifying potential partners
- Understanding decision-making timelines and cultural differences by partner type
- Building confidence in objection handling with proven response frameworks

---

### Executive Communication & Strategic Briefing

#### Executive Intelligence Dashboard
**Location:** `.claude/skills/executive-intelligence-dashboard/`
**Purpose:** Generate executive-grade weekly intelligence briefs by synthesizing Asana, Gmail, and Google Drive data into HTML dashboards.

**Quick Links:** [README](.claude/skills/executive-intelligence-dashboard/README.md) ⭐ | [Quick Start](.claude/skills/executive-intelligence-dashboard/QUICK-START.md) | [Skill Spec](.claude/skills/executive-intelligence-dashboard/SKILL.md)

**When to Use:**
- Generating weekly 360 Impact Brief for board meetings
- Preparing comprehensive partnership or operations reports with decision support
- Board meeting preparation and quarterly strategic planning sessions
- Creating stakeholder communications with strategic context

#### 360 Executive Brief / Newsletter Generator
**Location:** `.claude/skills/360-newsletter-generator/`
**Purpose:** Generate executive intelligence briefs (confidential) and stakeholder newsletters (shareable) with interactive Chart.js visualizations and modern dashboard design.

**Quick Links:** [README](.claude/skills/360-newsletter-generator/README.md) ⭐ | [Data Collection Guide](.claude/skills/360-newsletter-generator/references/data-collection-guide.md) | [Content Analysis Framework](.claude/skills/360-newsletter-generator/references/content-analysis-framework.md)

**When to Use:**
- Creating board updates and investor briefings with confidential data
- Generating weekly/monthly newsletters for stakeholders and partners
- Preparing pre-meeting briefings with talking points

#### 360 Board Meeting Prep Agent
**Location:** `360-board-meeting-prep/`
**Purpose:** Transform data from Asana, QuickBooks, Gmail, and Google Drive into professional board packets with automated quality checks.

**Quick Links:** [README](360-board-meeting-prep/README.md) ⭐ | [Main Orchestrator](360-board-meeting-prep/SKILL.md) | [Financial Dashboard](360-board-meeting-prep/references/financial-dashboard.md)

**When to Use:**
- Preparing quarterly or annual board meetings
- Generating comprehensive board documents with multi-source data synthesis
- Cross-validating financial and operational data
- Pre-drafting board motions and post-meeting action items

#### Executive Impact Presentation Generator
**Location:** `.claude/skills/executive-impact-presentation-generator/`
**Purpose:** Generate board-ready impact reports in dual formats (presentation deck and executive document) from a single content input, with brand customization, accessibility compliance, and print optimization.

**Quick Links:** [README](.claude/skills/executive-impact-presentation-generator/README.md) ⭐ | [Quick Start](.claude/skills/executive-impact-presentation-generator/QUICK-START.md) | [Skill Guide](.claude/skills/executive-impact-presentation-generator/SKILL.md)

**When to Use:**
- Quarterly board meetings requiring live presentations and comprehensive follow-up documents
- Annual impact reports for stakeholders, funders, and partners
- Grant reporting with professional polish and accessibility compliance
- Partnership pitches with impressive materials and leave-behind documents
- Quick regeneration of reports with updated metrics

---

### Process Documentation & Workflow Visualization

#### Workflow Process Generator
**Location:** `.claude/skills/workflow-process-generator/`
**Purpose:** Transform organizational knowledge into professional, compliance-ready workflow documentation including SOPs, process maps, runbooks, and operational playbooks with built-in quality assurance and change management frameworks.

**Quick Links:** [README](.claude/skills/workflow-process-generator/README.md) ⭐ | [Quick Start](.claude/skills/workflow-process-generator/QUICK-START.md) | [Skill Spec](.claude/skills/workflow-process-generator/SKILL.md) | [Implementation Guide](.claude/skills/workflow-process-generator/IMPLEMENTATION-GUIDE.md)

**When to Use:**
- Visualizing operational workflows for team onboarding
- Preparing board-ready workflow presentations
- Making processes delegation-ready and identifying bottlenecks
- Creating multi-language workflow documentation for international partnerships

---

### Workflow Coordination & Orchestration

#### Skill Orchestrator
**Location:** `.claude/skills/skill-orchestrator/`
**Purpose:** Universal workflow coordinator that intelligently routes requests and coordinates complex multi-skill and multi-agent operations.

**Quick Links:** [INDEX (Start Here)](.claude/skills/skill-orchestrator/INDEX.md) ⭐ | [README](.claude/skills/skill-orchestrator/README.md) | [Quick Start](.claude/skills/skill-orchestrator/QUICK-START.md)

**When to Use:**
- Multi-step workflows requiring coordination of multiple skills/agents
- Cross-domain operations (Asana + Gmail + Drive integration)
- Complex workflows requiring context preservation across steps
- GitHub agent coordination with payload validation

#### Workflow Debugging
**Location:** `.claude/skills/workflow-debugging/`
**Purpose:** Systematic debugging toolkit for workflow orchestration systems with automated error recovery and multi-region support.

**Quick Links:** [README](.claude/skills/workflow-debugging/README.md) ⭐ | [Skill Spec](.claude/skills/workflow-debugging/SKILL.md) | [Implementation Guide](.claude/skills/workflow-debugging/IMPLEMENTATION-GUIDE.md)

**When to Use:**
- Debugging multi-stage evaluation workflows and technology assessments
- Troubleshooting cross-system integration failures
- Resolving Asana integration issues (webhooks, duplicates, rate limiting)
- Managing multi-geography workflow errors (timezone, locale, permissions)

---

### Project Management & Executive Intelligence

#### 360 Executive Project Tracker
**Location:** `.claude/skills/360-executive-project-tracker/`
**Purpose:** Build professionally designed, multi-source project status trackers that consolidate Gmail, Google Calendar, Google Drive, and Asana into Excel dashboards and interactive HTML visualizations.

**Quick Links:** [README](.claude/skills/360-executive-project-tracker/docs/README.md) ⭐ | [Quick Start](.claude/skills/360-executive-project-tracker/docs/QUICK_START.md) | [Deliverables Summary](.claude/skills/360-executive-project-tracker/docs/DELIVERABLES_SUMMARY.md)

**When to Use:**
- Creating comprehensive project status trackers with automated updates
- Building executive dashboards for project visibility and blocker tracking
- Generating weekly status reports and tracking multi-project portfolios
- Monitoring team workload and capacity across workstreams

---

### Legal Intelligence & Risk Management

#### Contract Redlining Tool
**Location:** `.claude/skills/contract-redlining-tool/`
**Purpose:** Automated contract review and redlining that analyzes contracts against 360's standard positions and produces attorney-quality redlines with tracked changes, margin comments, and negotiation guidance.

**Quick Links:** [README](.claude/skills/contract-redlining-tool/README.md) ⭐ | [Implementation Guide](.claude/skills/contract-redlining-tool/IMPLEMENTATION-GUIDE.md) | [Examples](.claude/skills/contract-redlining-tool/EXAMPLES.md) | [Negotiation Playbook](.claude/skills/contract-redlining-tool/NEGOTIATION-PLAYBOOK.md)

**When to Use:**
- Reviewing contracts from partners, clients, or collaborators
- Identifying risks and misalignment with standard positions (IP, payment, scope, liability)
- Preparing negotiation strategy and talking points
- Training team on contract standards and protecting business interests

---

### Client Showcasing & Business Development

#### 360 Client Portfolio Builder
**Location:** `.claude/skills/360-client-portfolio-builder/`
**Purpose:** Create professional, editorially sophisticated portfolio HTML pages for 360 client ventures using Vianeo business validation sprint data. Production-quality single-page sites that build credibility with investors and partners.

**Quick Links:** [README](.claude/skills/360-client-portfolio-builder/README.md) ⭐ | [Quick Start](.claude/skills/360-client-portfolio-builder/QUICK-START.md) | [Design Standards](.claude/skills/360-client-portfolio-builder/references/design-standards.md) | [Deployment Guides](.claude/skills/360-client-portfolio-builder/deployment/)

**When to Use:**
- Creating showcase pages for current 360 client teams
- Presenting Vianeo sprint outputs to investors or partners
- Building portfolio section for 360 website
- Partnership development and fundraising preparation materials

---

### Strategic Leadership & Decision Support

#### CEO Advisor
**Location:** `.claude/skills/ceo-advisor/`
**Purpose:** Advanced executive intelligence system providing a complete AI-powered advisory board with five specialized experts (Intelligence, Relationship, Performance, Strategy, Financial) delivering integrated strategic guidance, stakeholder management, performance optimization, financial oversight, and real-time intelligence for CEO decision-making.

**Quick Links:** [README](.claude/skills/ceo-advisor/README.md) ⭐ | [Quick Start](.claude/skills/ceo-advisor/QUICK-START.md) | [Skill Spec](.claude/skills/ceo-advisor/SKILL.md) | [Implementation Guide](.claude/skills/ceo-advisor/IMPLEMENTATION-GUIDE.md)

**When to Use:**
- Daily intelligence briefs with critical issues, stakeholder attention, and strategic insights
- Board meeting preparation with individual member analysis and predicted questions
- Crisis response protocol with immediate action plans and communication strategy
- Strategic planning sessions with environmental scanning and scenario modeling
- Time and energy optimization with delegation recommendations and schedule analysis
- Stakeholder relationship tracking with engagement recommendations and trajectory predictions

---

### Sales & Business Development

#### Sales Automator
**Location:** `.claude/skills/sales-automator/`
**Purpose:** Intelligent sales automation with relationship intelligence, deal pipeline tracking, and competitive analysis. Transforms basic email automation into a context-aware conversion engine that researches prospects, tracks deals, and generates hyper-personalized outreach grounded in real intelligence.

**Quick Links:** [README](.claude/skills/sales-automator/README.md) ⭐ | [Quick Start](.claude/skills/sales-automator/docs/QUICK-START.md) | [Installation](.claude/skills/sales-automator/docs/INSTALLATION.md) | [Reference](.claude/skills/sales-automator/references/REFERENCE.md)

**When to Use:**
- Cold outreach campaigns (5-touch sequences with research-backed personalization)
- Warm lead follow-up (re-engage prospects with past conversation context)
- Stuck deal re-activation (identify and re-engage stalled opportunities)
- Proposal generation (comprehensive partnership proposals with case studies)
- Pipeline health monitoring (weekly reviews, forecasting, conversion tracking)
- Competitive positioning (research and position against alternatives)

#### 360 Proposal Builder
**Location:** `.claude/skills/360-proposal-builder/`
**Purpose:** Generate executive-grade proposals for 360 Social Impact Studios' innovation transformation services. Creates customized proposals with proper GenIP attribution, cultural considerations, and strategic positioning across Innovation Assessment, Business Design, and Leadership & Culture tracks.

**Quick Links:** [README](.claude/skills/360-proposal-builder/README.md) ⭐ | [Quick Start](.claude/skills/360-proposal-builder/QUICK-START.md) | [Skill Spec](.claude/skills/360-proposal-builder/SKILL.md)

**When to Use:**
- Creating customized proposals for innovation assessment, venture building, or leadership development
- Ensuring proper GenIP attribution and methodology crediting
- Adapting proposals for clients across global regions with cultural intelligence
- Generating service-specific pricing, deliverables, and strategic positioning

---

### Financial Analysis & Investment Intelligence

#### Financial Modeling Skills
**Location:** `.claude/skills/financial-modeling-skills/`
**Purpose:** Institutional-grade financial analysis toolkit for investment evaluation, portfolio management, and impact measurement.

**Quick Links:** [README](.claude/skills/financial-modeling-skills/README.md) ⭐ | [Investment Analysis](.claude/skills/financial-modeling-skills/investment-analysis/) | [Portfolio Intelligence](.claude/skills/financial-modeling-skills/portfolio-intelligence/)

**When to Use:**
- Investment evaluation and multi-scenario financial modeling
- Portfolio performance analytics and strategic allocation optimization
- Social return on investment (SROI) and impact-weighted accounting
- Technology transfer valuation and IP portfolio assessment

#### IRS Form 990-EZ Preparation
**Location:** `skills/990-ez-preparation/`
**Purpose:** Automated nonprofit tax compliance through intelligent data collection, multi-level validation, and complete filing package generation. Reduces preparation time from 40+ hours to under 10 hours.

**Quality:** ✅ **99% test coverage** (73 comprehensive tests covering all phases and edge cases)

**Quick Links:** [README](skills/990-ez-preparation/README.md) ⭐ | [Quick Start](skills/990-ez-preparation/docs/QUICK-START.md) | [Skill Spec](skills/990-ez-preparation/SKILL.md)

**When to Use:**
- Preparing annual IRS Form 990-EZ for small nonprofits (receipts < $200K, assets < $500K)
- Automated eligibility verification and compliance checking
- Multi-level validation (mathematical, regulatory, narrative, strategic)
- Complete filing package generation with Schedules A, B, and O
- Board-ready presentation with validation reports and pre-filing checklists

---

## Documentation

### Guides & References
- [Creating Skills Guide](docs/CREATING-SKILLS.md) - Comprehensive guide for creating new skills
- [Skill Template](skills/templates/skill-template.md) - Template for new skills
- [Testing Infrastructure](docs/TESTING.md) - Python and TypeScript testing setup
- [Merge Instructions](docs/MERGE_INSTRUCTIONS.md) - Guidelines for merging contributions

### Project Documentation
- [PR Descriptions](docs/pr-descriptions/) - Pull request templates and descriptions for all major features
- [Implementation Summaries](docs/summaries/) - Detailed summaries of key implementations and features

## Contributing

When adding new skills:
1. Use the provided template
2. Follow naming conventions (lowercase-with-hyphens)
3. Place skills in appropriate category folders
4. Update this README with links to new skills
5. Test thoroughly before committing

## Use Cases

This repository supports:
- Workflow automation and standardized processes
- Knowledge management and task templates
- Custom Claude behaviors and repeatable analysis patterns

## Getting Started

The best way to get started is to:
1. Browse skills by category above and click README links
2. Review the documentation in `docs/CREATING-SKILLS.md`
3. Examine the skill template in `skills/templates/`
4. Create your first skill using the template

---

## AI-Assisted Execution

This system is optimized for AI assistance with Claude. Each skill can be invoked through natural language prompts or by directly referencing the skill name. Below are organized examples by category.

### How to Invoke Skills

**Method 1: Natural Language** - Simply describe your task and Claude will route to the appropriate skill
**Method 2: Direct Invocation** - Reference the skill name explicitly (e.g., "Use the ceo-advisor skill to...")

---

### Healthcare & Life Sciences Regulatory

**Skill:** `fda-consultant-agent`

```
"Determine the FDA regulatory pathway for our AI-powered diagnostic device"

"Analyze 510(k) submission requirements for a Class II medical device"

"Review our Quality Management System against FDA QSR requirements"

"Evaluate our SaMD against the IMDRF risk classification framework"

"Provide FDA guidance for our combination drug-device product"
```

---

### AI Governance & Responsible AI

**Skill:** `ai-ethics-advisor`

```
"Conduct a bias assessment on our hiring algorithm"

"Evaluate our AI system for EU AI Act compliance"

"Perform a community impact analysis for our predictive policing tool"

"Run an ethical audit on our lending decision model"

"Assess fairness metrics for our healthcare triage system"

"Generate a responsible AI development checklist for our project"
```

---

### Research & Validation

**Skill:** `open-deep-research-team`

```
"Conduct comprehensive research on emerging battery technologies for EVs"

"Generate an academic-quality literature review on CRISPR therapeutics"

"Research competitive landscape for enterprise AI governance tools"

"Compile a technical evaluation of federated learning architectures"

"Create a market analysis report with proper academic citations"
```

**Skill:** `strategic-persona-builder`

```
"Build a Vianeo-formatted partner persona from these interview transcripts"

"Generate stakeholder personas using Jobs-to-be-Done framework"

"Create beneficiary personas with empathy mapping for our healthcare app"

"Develop hypothesis personas for our validation research planning"

"Generate dual-format personas for both strategy and platform entry"
```

---

### Design & Visual Excellence

**Skill:** `design-director`

```
"Elevate this dashboard to Stripe-quality design standards"

"Apply Linear-style visual polish to my executive presentation"

"Transform this functional HTML report into professional design quality"

"Ensure WCAG AA accessibility compliance for this interface"

"Add Apple-inspired typography and visual hierarchy to this document"
```

---

### Content Strategy & Multi-Platform Publishing

**Skill:** `360-content-converter`

```
"Convert this blog post into platform-optimized content for LinkedIn, Twitter, and email"

"Repurpose this case study for 15 different platforms in English and Spanish"

"Create a cohesive content ecosystem from this single research report"

"Generate design-ready specifications for social media graphics from this content"
```

---

### Data Intelligence & Quality Monitoring

**Skill:** `intelligence-extractor`

```
"Extract partnership intelligence from this meeting transcript"

"Parse funding insights from these investor call notes"

"Generate structured stakeholder intelligence from board meeting minutes"

"Process this Zapier webhook payload for intelligence extraction"

"Create cross-cultural meeting intelligence report from this session"
```

---

### Executive Communication & Strategic Briefing

**Skill:** `executive-intelligence-dashboard`

```
"Generate the weekly 360 Impact Brief from Asana, Gmail, and Drive data"

"Create a comprehensive partnership report with decision support"

"Prepare a quarterly strategic planning brief for the board"

"Build an executive HTML dashboard synthesizing all project data"
```

**Skill:** `360-newsletter-generator`

```
"Generate an executive intelligence brief for board members"

"Create a stakeholder newsletter with Chart.js visualizations"

"Prepare a pre-meeting briefing with key talking points"

"Build a monthly investor update with confidential metrics"
```

**Skill:** `360-board-meeting-prep`

```
"Prepare the quarterly board meeting packet from all data sources"

"Generate board documents with automated quality checks"

"Cross-validate financial and operational data for board presentation"

"Pre-draft board motions and action items for the upcoming meeting"
```

**Skill:** `executive-impact-presentation-generator`

```
"Generate board-ready impact reports in both presentation and document formats"

"Create an annual impact report with brand customization"

"Produce grant reporting materials with accessibility compliance"

"Build partnership pitch materials with leave-behind documents"
```

---

### Process Documentation & Workflow Visualization

**Skill:** `workflow-process-generator`

```
"Document our onboarding workflow with Mermaid diagrams"

"Create board-ready workflow visualizations for operations review"

"Generate interactive HTML workflow documentation from our process descriptions"

"Build delegation-ready process documentation with bottleneck analysis"

"Create multi-language workflow documentation for international teams"
```

---

### Workflow Coordination & Orchestration

**Skill:** `skill-orchestrator`

```
"Coordinate a multi-step workflow using research and design skills"

"Orchestrate cross-domain operations with Asana, Gmail, and Drive"

"Route this complex request to the appropriate specialist skills"

"Manage this sequential workflow with context preservation"
```

**Skill:** `workflow-debugging`

```
"Debug this failing multi-stage evaluation workflow"

"Troubleshoot Asana webhook integration issues"

"Diagnose cross-system integration failures in our pipeline"

"Resolve multi-geography workflow errors with timezone issues"
```

---

### Project Management & Executive Intelligence

**Skill:** `360-executive-project-tracker`

```
"Build a project status tracker consolidating Gmail, Calendar, Drive, and Asana"

"Create an executive dashboard for project visibility and blockers"

"Generate weekly status reports across all workstreams"

"Monitor team workload and capacity with automated updates"
```

---

### Legal Intelligence & Risk Management

**Skill:** `contract-redlining-tool`

```
"Review this partner contract and generate attorney-quality redlines"

"Analyze this agreement for IP, payment, and liability risks"

"Prepare negotiation strategy and talking points for this contract"

"Identify misalignment with our standard contract positions"

"Generate tracked changes with margin comments for legal review"
```

---

### Client Showcasing & Business Development

**Skill:** `360-client-portfolio-builder`

```
"Create a professional portfolio page for this client venture"

"Generate an investor-ready showcase from Vianeo sprint data"

"Build a client portfolio section for the 360 website"

"Prepare partnership development materials from validation outputs"
```

**Skill:** `360-proposal-builder`

```
"Generate a customized proposal for innovation assessment services"

"Create a venture building proposal with proper GenIP attribution"

"Build a leadership development proposal with cultural considerations"

"Prepare service-specific pricing and deliverables documentation"
```

---

### Strategic Leadership & Decision Support

**Skill:** `ceo-advisor`

```
"Generate my daily intelligence brief with critical issues and strategic insights"

"Prepare board meeting materials with individual member analysis"

"Activate crisis response protocol with immediate action plan"

"Run a strategic planning session with scenario modeling"

"Optimize my schedule with delegation recommendations"

"Analyze stakeholder relationships and engagement trajectory"
```

---

### Sales & Business Development

**Skill:** `sales-automator`

```
"Generate a 5-touch cold outreach sequence with research-backed personalization"

"Create warm lead follow-up emails using past conversation context"

"Re-engage stalled deals with context-aware messaging"

"Build a comprehensive partnership proposal with case studies"

"Run weekly pipeline health review with conversion tracking"

"Research and position against competitive alternatives"
```

---

### Financial Analysis & Investment Intelligence

**Skill:** `financial-modeling-skills`

```
"Perform multi-scenario investment evaluation modeling"

"Generate portfolio performance analytics with allocation optimization"

"Calculate social return on investment (SROI) for this program"

"Assess technology transfer valuation for our IP portfolio"
```

**Skill:** `990-ez-preparation`

```
"Prepare IRS Form 990-EZ with automated eligibility verification"

"Run multi-level validation on our nonprofit tax filing"

"Generate complete filing package with Schedules A, B, and O"

"Create board-ready presentation with pre-filing checklist"
```

---

### Tips for Effective AI Execution

1. **Be Specific**: Include relevant context like "for our healthcare AI startup" or "targeting Series A investors"
2. **Reference Data Sources**: Mention where your data lives (e.g., "from our Asana projects and Gmail threads")
3. **Specify Output Format**: Request "HTML dashboard," "Mermaid diagram," or "executive summary" as needed
4. **Chain Skills**: For complex workflows, mention multiple needs and the skill-orchestrator will coordinate

Each skill has detailed documentation in its respective directory with quick-start guides, implementation details, and example outputs.

---

**Version:** 2.8.0
**Last Updated:** 2025-11-25

### Recent Updates
- **NEW: Slash Commands** - 31 shortcuts for invoking skills (21 single-skill + 10 workflow templates)
- **NEW: Workflow Templates** - Pre-built multi-skill sequences for common routines (`/morning`, `/weekly-review`, `/meeting-wrap`, etc.)
- Improved 990-ez-preparation test coverage from 51% to 99% (73 comprehensive tests)
- Reorganized documentation into structured directories (pr-descriptions/, summaries/)
- Added comprehensive testing infrastructure for Python and TypeScript
- Enhanced repository organization and documentation structure
