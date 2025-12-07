---
name: financial-modeling-skills
description: Comprehensive financial analysis suite including investment evaluation, portfolio intelligence, SROI calculation, technology transfer valuation, and cross-border analysis. Use for investment decisions, portfolio management, impact measurement, and financial modeling requiring institutional-grade outputs. (project)
---

# Financial Modeling Skills - Master Skill

## Purpose

This is a comprehensive financial modeling suite containing multiple specialized skills for investment analysis, portfolio management, and impact measurement. This master skill routes requests to the appropriate sub-skill based on the user's needs.

## Sub-Skill Catalog

### 1. Investment Analysis
**Use when:** Evaluating equity investments, growth capital opportunities, acquisition targets, portfolio companies

**Capabilities:**
- Multi-scenario financial modeling (base, upside, downside)
- Returns analysis (IRR, MOIC, DPI, TVPI)
- Comparable company benchmarking
- Risk assessment frameworks
- Sensitivity analysis and stress testing
- Exit strategy evaluation
- Investment committee documentation

**Typical outputs:** Excel financial model, IC memo, executive summary
**Time investment:** 50-70 minutes comprehensive analysis

---

### 2. Portfolio Intelligence
**Use when:** Analyzing portfolio performance, creating LP reports, optimizing allocation, assessing risk correlations

**Capabilities:**
- Cross-portfolio performance analytics
- Strategic allocation optimization
- Risk correlation analysis
- Impact measurement aggregation
- Quarterly reporting automation
- Interactive dashboard generation
- LP communication packages

**Typical outputs:** Portfolio dashboard (Excel/HTML), quarterly reports, performance attribution
**Time investment:** 40-60 minutes

---

### 3. Impact Modeling
**Use when:** Quantifying social impact, calculating SROI, structuring blended finance, measuring SDG contributions

**Capabilities:**
- Social Return on Investment (SROI) calculation
- Blended finance structuring
- Impact-weighted accounting
- Sustainability metrics integration
- Theory of change financial modeling
- SDG contribution mapping
- Impact attribution analysis

**Typical outputs:** SROI report, impact dashboard, blended finance structure model
**Time investment:** 60-90 minutes

---

## Routing Logic

When user request is received, determine which sub-skill to use:

### Investment Analysis Triggers:
- "evaluate [company] as an investment"
- "build a financial model for [company]"
- "analyze this acquisition opportunity"
- "create IC memo for [deal]"
- "perform due diligence on [investment]"
- Keywords: IRR, MOIC, returns, valuation, investment, equity, growth capital

**Action:** Execute investment analysis workflow

---

### Portfolio Intelligence Triggers:
- "portfolio performance analysis"
- "quarterly portfolio report"
- "LP update"
- "portfolio risk analysis"
- "allocation optimization"
- Keywords: portfolio, LP, fund performance, risk correlation, allocation

**Action:** Execute portfolio intelligence workflow

---

### Impact Modeling Triggers:
- "calculate SROI for [program/investment]"
- "measure social impact"
- "blended finance structure"
- "SDG contribution"
- "theory of change financial model"
- Keywords: SROI, impact, social return, blended finance, SDG, sustainability

**Action:** Execute impact modeling workflow

---

### Multiple Sub-Skills Needed:
If request requires multiple sub-skills (e.g., "evaluate this impact investment"):
1. Start with investment-analysis for financial modeling
2. Then use impact-modeling for SROI calculation
3. Integrate outputs into comprehensive report

---

## Quality Standards

All sub-skills adhere to institutional investment standards:

**Accuracy:**
- Validated calculations with sourced assumptions
- Cross-checked market data
- Documented methodology

**Clarity:**
- Clear logic flow throughout models
- Color-coded inputs, calculations, outputs
- Executive summaries for non-technical stakeholders

**Flexibility:**
- Scenario testing (base, upside, downside)
- Sensitivity analysis on key variables
- Adjustable assumptions for different contexts

**Professionalism:**
- Consistent formatting across all outputs
- Publication-ready quality
- Board and IC presentation standards

**Auditability:**
- Transparent formulas (no hidden calculations)
- Traceable inputs with sources
- Documented assumptions and logic

---

## Data Integration

### Supported Data Sources:
- **Financial Platforms**: S&P Capital IQ, Daloopa, PitchBook, FactSet
- **Internal Systems**: Asana (pipeline), Google Drive (documents), Box (templates)
- **Market Data**: Web search for real-time metrics, SEC filings, regulatory documents
- **Portfolio Tools**: GenIP (IP valuation), Vianeo (business validation)

### Data Gathering Protocol:
1. Use automated collection when available
2. Fallback to manual web search for missing data
3. Document all sources in model assumptions tab
4. Flag low-confidence data for user verification

---

## Output Formats

### Excel Models (Investment Analysis, Impact Modeling):
- Working formulas throughout
- Multiple worksheets (assumptions, model, scenarios, sensitivity, returns)
- Institutional formatting standards
- Print-optimized layouts

### Dashboards (Portfolio Intelligence):
- Interactive HTML with charts
- Excel pivot tables and charts
- Real-time data connections (if available)
- Mobile-responsive layouts

### Documents (All Skills):
- Investment committee memos
- Executive summaries
- Board presentations
- LP reports

---

## Usage Examples

### Example 1: Growth Equity Investment Evaluation
```
User: "Evaluate MediTech Solutions as a $75M Series C investment.
      They're a healthcare SaaS company with $15M ARR growing 80% YoY."

System: Routes to investment-analysis workflow
Output: Complete Excel model + IC memo (50-70 minutes)
```

### Example 2: Quarterly Portfolio Review
```
User: "Generate Q4 2024 portfolio performance report with risk analysis"

System: Routes to portfolio-intelligence workflow
Output: Portfolio dashboard (Excel/HTML) + quarterly report (40-60 minutes)
```

### Example 3: Impact Measurement
```
User: "Calculate SROI for our education program that served 10,000 students
      with $2M budget over 3 years"

System: Routes to impact-modeling workflow
Output: SROI report with impact dashboard (60-90 minutes)
```

### Example 4: Combined Analysis
```
User: "Evaluate this $50M impact investment in affordable housing.
      Need both financial returns and social impact analysis."

System:
  Step 1: Routes to investment-analysis workflow (financial model + IC memo)
  Step 2: Routes to impact-modeling workflow (SROI calculation)
  Step 3: Integrates outputs into comprehensive impact investment analysis
Output: Integrated financial + impact report (110-160 minutes total)
```

---

## Getting Started

### Quick Start:
- For investment evaluation → Use investment-analysis sub-skill
- For portfolio reporting → Use portfolio-intelligence sub-skill
- For impact measurement → Use impact-modeling sub-skill

### Advanced Usage:
- Combine multiple sub-skills for comprehensive analyses
- Customize templates for specific investment theses
- Extend with custom scripts for data collection

---

## Architecture Principles

### Progressive Disclosure:
- **Level 1**: Master skill routes to appropriate sub-skill
- **Level 2**: Sub-skill loads core workflow
- **Level 3**: Detailed models and references load as needed

### Reusability First:
- Standardized model templates across sub-skills
- Consistent formatting protocols
- Modular calculation components
- Shareable validation frameworks

### Executive Readiness:
- Publication-quality outputs by default
- Board-ready visualizations
- Strategic context integration
- Decision-focused narratives

---

## Time Investment Guidelines

| Sub-Skill | Complexity | Time Estimate |
|-----------|------------|---------------|
| Investment Analysis | High | 50-70 minutes |
| Portfolio Intelligence | Medium | 40-60 minutes |
| Impact Modeling | High | 60-90 minutes |
| Combined Analyses | Very High | 110-160 minutes |

**Note:** Times assume data is readily available. Add 15-30 minutes if extensive data gathering required.

---

## Troubleshooting

**"Which sub-skill should I use?"**
→ See routing logic section above
→ When in doubt, start with investment-analysis (most general)

**"Can I combine multiple sub-skills?"**
→ Yes! For complex analyses, use multiple sub-skills sequentially
→ Example: Investment analysis + impact modeling for impact investments

**"Data sources not accessible"**
→ Use web search as fallback
→ Document data limitations in assumptions
→ Flag for user verification

---

## Investment Analysis Workflow (Sub-Skill 1)

When investment analysis is triggered, execute this workflow:

### Phase 1: Context Gathering
Collect:
- Company name and industry
- Investment amount and structure
- Current metrics (revenue, growth rate, margins)
- Investment thesis
- Exit expectations

### Phase 2: Data Collection
Gather:
- Historical financials (3-5 years if available)
- Market size and growth rate
- Comparable companies
- Competitive landscape
- Unit economics

### Phase 3: Model Building
Create Excel model with:
- Revenue build-up (by product/segment)
- Expense projections (COGS, OpEx)
- Working capital modeling
- Capex requirements
- Three scenarios (base, upside, downside)

### Phase 4: Returns Analysis
Calculate:
- IRR (Internal Rate of Return)
- MOIC (Multiple on Invested Capital)
- DPI (Distributions to Paid-In)
- TVPI (Total Value to Paid-In)
- Sensitivity analysis on key assumptions

### Phase 5: Documentation
Produce:
- Excel financial model
- Investment committee memo
- Executive summary
- Key risks and mitigations

---

## Portfolio Intelligence Workflow (Sub-Skill 2)

When portfolio intelligence is triggered, execute this workflow:

### Phase 1: Portfolio Snapshot
Create overview of:
- Number of investments
- Total capital deployed
- Current portfolio value
- Realized vs. unrealized gains
- Geographic/sector distribution

### Phase 2: Performance Analytics
Analyze:
- Portfolio-level IRR and MOIC
- Performance by vintage year
- Performance by sector/geography
- Top/bottom performers
- Value creation drivers

### Phase 3: Risk Analysis
Assess:
- Concentration risk
- Correlation between investments
- Mark-to-market valuations
- Portfolio stress testing
- Liquidity timeline

### Phase 4: Reporting
Generate:
- Interactive dashboard (HTML/Excel)
- Quarterly LP report
- Performance attribution analysis
- Benchmark comparisons

---

## Impact Modeling Workflow (Sub-Skill 3)

When impact modeling is triggered, execute this workflow:

### Phase 1: Theory of Change
Map:
- Inputs (resources invested)
- Activities (what you do)
- Outputs (immediate results)
- Outcomes (changes for beneficiaries)
- Impact (long-term societal change)

### Phase 2: Impact Quantification
Measure:
- Number of beneficiaries
- Outcome indicators
- Deadweight (what would happen anyway)
- Attribution (your contribution vs. others)
- Duration of impact

### Phase 3: Financial Valuation
Calculate:
- Monetize outcomes (financial proxies)
- Discount future benefits
- Calculate net present social value
- Compute SROI ratio
- Sensitivity analysis

### Phase 4: Reporting
Deliver:
- SROI calculation report
- Impact dashboard
- SDG alignment mapping
- Stakeholder value breakdown
- Investment case for impact

---

## Success Metrics

**Quality Indicators**
- 100% formula accuracy in models
- >90% stakeholder satisfaction with outputs
- <5% revision rate after initial delivery

**Efficiency Indicators**
- Models delivered within time estimates
- 50% time savings vs. manual analysis
- Reusable templates reduce future work by 60%

**Business Impact**
- Better investment decisions
- Improved portfolio performance
- Enhanced LP communication
- Stronger impact measurement

---

**Ready to start?** Provide an investment opportunity, portfolio update request, or impact measurement need, and I'll route you to the appropriate workflow.
