---
name: contract-redlining-tool
description: Automated contract review and redlining tool that analyzes incoming contracts against 360's standard positions and produces attorney-quality redlines with tracked changes, margin comments, and negotiation guidance. (project)
---

# Contract Redlining Tool Skill

## Purpose

This skill enables Claude to perform attorney-quality contract reviews by analyzing incoming contracts against 360 Social Impact Studios' standard contract positions, identifying risks, and generating professional redlines with tracked changes, margin comments, and comprehensive negotiation guidance.

## Core Capabilities

**Risk Detection**: Automatically identify critical risks (deal-breakers), high-priority issues, and standard improvements across multiple contract types including client services, partnerships, MoUs, and joint ventures.

**Intelligent Redlining**: Generate tracked-changes documents with specific protective language drawn from 360's clause library, tailored to deal type, power dynamics, and strategic importance.

**Business Impact Analysis**: Provide margin comments explaining not just the legal issue, but the business impact, negotiation approach, and compromise options for each redline.

**Cultural Intelligence**: Apply cultural negotiation considerations for international deals, particularly Brazilian partnerships with appropriate governing law and arbitration provisions.

## When to Use This Skill

Use this skill when asked to:
- Review and redline incoming contracts from partners, clients, or collaborators
- Analyze contract terms for risks and misalignment with 360's standard positions
- Prepare negotiation guidance and talking points for contract discussions
- Compare contract terms across similar deal types
- Generate executive summaries of contract risks and recommendations

Do NOT use this skill for:
- Drafting new contracts from scratch (use templates instead)
- Simple contract questions that don't require full review
- Non-contract legal questions
- Contracts outside 360's typical deal types without proper context

## Operating Principles

### Context-Aware Analysis

Every contract review must begin by gathering critical context:

1. **Deal Type Classification**
   - Client Services Contract (ConnectMyVariant model)
   - Partnership/Distribution Agreement (Ecosystem Partner model)
   - Memorandum of Understanding (Exploration)
   - Joint Venture/Equity Deal
   - University Partnership
   - Other (requires specification)

2. **Strategic Assessment**
   - Strategic importance (Critical / High / Medium / Standard)
   - Power dynamics (We need them / Balanced / They need us)
   - Geographic context (Domestic / Brazil / Latin America / Europe / Other)
   - Timeline urgency (Rush / Normal / Patient)

3. **Key Concerns**
   - Payment terms
   - IP ownership
   - Liability exposure
   - Scope creep
   - Termination rights
   - Non-compete duration
   - Confidentiality scope

### Risk Prioritization Framework

Apply a three-tier risk classification system:

**🚨 CRITICAL (Deal-Breakers)**
- Unlimited liability
- IP assignment of methodologies/frameworks
- Payment contingent on subjective satisfaction
- One-sided termination without payment for work done
- Automatic renewal without escape rights
- Equity without governance/information rights

**⚠️ HIGH PRIORITY (Must Fix)**
- Payment terms over 45 days
- Unlimited revisions or scope
- One-way indemnification
- Immediate exclusivity without performance requirements
- Commission due before payment received
- Broad non-compete (>12 months or wide geography)

**📋 STANDARD (Best Practice)**
- Missing termination for convenience
- No limitation of consequential damages
- Vague scope language
- Missing change order process
- Weak confidentiality protections
- Assignment without consent

### Standard Positions by Deal Type

**Client Services Contracts**
- Payment: 50% upfront, 50% at milestone | Net 30 terms
- Scope: Specific deliverables with 1-2 revision rounds
- IP: Client owns deliverables, 360 retains methodologies
- Liability: Cap at fees paid, no consequential damages
- Termination: 30-60 days notice, payment for work completed

**Partnership Agreements**
- Commission: 25-30% (30% software, 25% services)
- Payment: Only after 360 receives customer payment
- Exclusivity: Conditional on first sale + performance minimums
- Prospect Protection: 6 months (renewable if active)
- Non-Compete: 12 months post-termination, narrowly defined
- Term: 12 months with 30-day renewal notice

**Memoranda of Understanding**
- Nature: Non-binding, no financial commitments
- Confidentiality: Mutual, survives termination
- Publicity: General announcement okay, deal terms need approval
- Term: 1 year auto-renew with 30-day notice
- Governing Law: Brazil for Brazilian partners (CCBC arbitration), Washington for U.S.

**Joint Ventures**
- Equity Alignment: Board rights for >15% ownership
- Deadlock Resolution: Mediation, buy-sell, or designated tie-breaker
- Tag-Along Rights: For all equity holders in sales >25%
- IP Ownership: Background IP retained, jointly-developed IP negotiated
- Information Rights: Quarterly financials, board meeting notices

### International Deal Considerations

**Brazilian Partnerships**
- Governing Law: Federal Republic of Brazil
- Dispute Resolution: CCBC arbitration in São Paulo
- Payment: USD with currency fluctuation protection (PTAX rate from Banco Central)
- Compliance: Brazilian Anti-Corruption Law (Lei 12.846/2013)
- Cultural: Longer relationship-building, senior leader approval, formal communication

**European Partnerships**
- Data Privacy: GDPR compliance required
- Payment: Net 60 common, build in buffer
- Legal: May prefer their country's law, arbitration as compromise
- Cultural: Formal communication, detailed documentation, consensus-oriented

## Quality Standards

Every contract review must deliver:

**1. Redlined Document (.docx)**
- Tracked changes: Deletions in strikethrough red, additions in underlined blue
- Margin comments for each cluster of edits
- Comment categories: 🚨 CRITICAL, ⚠️ HIGH PRIORITY, 📋 STANDARD, 💡 OPPORTUNITY, 🤝 NEGOTIATION
- Professional formatting preserved from original

**2. Executive Summary (1 page)**
- Deal snapshot (parties, value, term, deal type)
- Risk assessment (critical/high/standard issues identified)
- Strategic alignment (fit with 360's business model)
- Top 5 must-wins (non-negotiables)
- Top 5 flexible points (compromise areas)
- Overall recommendation (Sign / Negotiate / Walk Away)

**3. Negotiation Brief**
- Opening position on each issue
- Priority matrix (what to fight for vs. what to concede)
- Compromise framework with fallback positions
- Talking points for each major issue
- Cultural considerations (if international)
- BATNA analysis (Best Alternative To Negotiated Agreement)

## Protective Clause Library

### Payment Protection

**Net 15-30 Payment Terms**
```
Payment due within [15/30] days of invoice date. Invoices not disputed within
ten (10) days are deemed accepted. Late payments subject to interest at 1.5%
per month (18% annual).
```

**Milestone Payments**
```
Total compensation of $[amount] payable as follows:
- [50%] ($[amount]) due within fifteen (15) days of contract execution
- [50%] ($[amount]) due upon [milestone], but no later than [date]
```

**Commission Only After Payment Received**
```
Commission payments become due only after Company receives full payment from
Customer. If Customer fails to pay or pays only partially, commission shall be
proportionally reduced or eliminated.
```

### IP Protection

**Deliverable Ownership with Methodology Retention**
```
Client owns all right, title, and interest in final deliverables created
specifically for Client under this Agreement. Consultant retains all rights to:
(a) Pre-existing materials, methodologies, processes, and tools
(b) Generalizable knowledge, skills, and experience
(c) Templates and frameworks developed independently
Client receives a perpetual, non-exclusive license to use deliverables for
internal business purposes only.
```

**Portfolio Use Rights**
```
Consultant may use de-identified, anonymized examples of work product for
marketing, portfolio demonstration, and case studies, provided no confidential
information is disclosed.
```

### Liability Protection

**Liability Cap**
```
Consultant's total aggregate liability under this Agreement, whether in contract,
tort, or otherwise, shall not exceed the total fees paid by Client to Consultant
under this Agreement.
```

**No Consequential Damages**
```
Neither party shall be liable for any indirect, incidental, consequential, special,
or punitive damages, including lost profits, revenue, or business opportunities,
even if advised of the possibility of such damages.
```

**Mutual Indemnification**
```
Each party shall indemnify and hold harmless the other from claims arising from:
(a) Its own negligence or willful misconduct
(b) Its breach of this Agreement
(c) Its infringement of third-party intellectual property rights
```

### Scope Protection

**Defined Deliverables**
```
Consultant shall deliver the following specific deliverables:
1. [Specific deliverable] by [date]
2. [Specific deliverable] by [date]
Deliverables shall include [number] rounds of revisions based on Client feedback.
```

**Change Order Process**
```
Requests outside the defined scope shall be addressed through a written change
order specifying additional deliverables, timeline, and fees. No out-of-scope work
shall commence without executed change order.
```

**Revision Limits**
```
Client entitled to [1-2] rounds of revisions per deliverable. Additional revision
rounds billed at $[hourly rate]/hour or [fixed fee] per round.
```

### Termination Protection

**Termination for Convenience**
```
Either party may terminate this Agreement for any reason upon [30/60] days
written notice to the other party. Upon termination:
(a) Client shall pay for all work completed through termination date
(b) Consultant shall deliver all completed deliverables
(c) Neither party liable for damages arising from termination in accordance
    with this section
```

**Post-Termination Obligations**
```
Upon termination or expiration:
(a) All unpaid fees become immediately due
(b) Each party shall return or destroy confidential information
(c) Sections [specify: confidentiality, IP, liability] survive termination
```

### International Provisions

**Brazilian Governing Law & Arbitration**
```
This Agreement shall be governed by the laws of the Federal Republic of Brazil.
Any dispute shall be resolved through binding arbitration in São Paulo, Brazil,
administered by Câmara de Comércio Brasil-Canadá (CCBC) under its Streamlined
Arbitration Rules. The arbitrator shall apply Brazilian law.
```

**Currency Fluctuation (Brazilian Deals)**
```
All payments in U.S. Dollars. If payment must be converted to Brazilian Reais,
the exchange rate shall be the official rate published by Banco Central do Brasil
on the payment due date. Neither party liable for currency fluctuation.
```

## Workflow Process

When a user requests contract review, follow this systematic process:

### Phase 1: Context Gathering (2-3 minutes)

Ask the user to provide:
1. Contract document (upload or paste text)
2. Deal type classification
3. Strategic importance and power dynamics
4. Geographic context
5. Key concerns or known issues
6. Timeline urgency

If the user doesn't provide full context, ask targeted questions to gather critical information.

### Phase 2: Document Analysis (5-7 minutes)

1. **Section Identification**
   - Map contract sections (parties, term, payment, scope, IP, liability, termination, etc.)
   - Extract key data (amounts, dates, obligations, restrictions)
   - Identify unusual or non-standard sections

2. **Pattern Matching**
   - Compare each section against 360's standard positions for this deal type
   - Flag deviations from standard protective clauses
   - Note missing protections that should be added

3. **Risk Detection**
   - Run through critical risk patterns (deal-breakers)
   - Identify high-priority issues
   - Note standard improvements
   - Adjust severity based on deal context (power dynamics, strategic value)

### Phase 3: Redline Generation (8-12 minutes)

1. **Draft Tracked Changes**
   - Delete problematic language (strikethrough red)
   - Insert protective language from clause library (underlined blue)
   - Ensure changes are clear and specific (no vague terms)
   - Preserve formatting from original document

2. **Create Margin Comments**
   - Group related edits into clusters
   - Write margin comment for each cluster explaining:
     - What the issue is (technical legal problem)
     - Why it matters (business impact)
     - Proposed fix (specific language changes)
     - Compromise option (if negotiable)
   - Categorize by severity (🚨 CRITICAL, ⚠️ HIGH PRIORITY, 📋 STANDARD, etc.)

3. **Write Executive Summary**
   - Deal snapshot (1 paragraph)
   - Risk assessment by category
   - Top 5 must-wins
   - Top 5 flexible points
   - Overall recommendation with reasoning

4. **Prepare Negotiation Brief**
   - Opening position on each issue
   - Priority matrix
   - Compromise framework
   - Talking points
   - Cultural considerations (if international)
   - BATNA analysis

### Phase 4: Quality Assurance (3-5 minutes)

**Technical Quality Checklist**
- [ ] All track changes render correctly
- [ ] Comments anchored to correct text
- [ ] Formatting preserved from original
- [ ] All edits have explanatory comments
- [ ] No orphan comments or unexplained changes

**Substantive Quality Checklist**
- [ ] All critical risks addressed with redlines
- [ ] Proposed language is clear and specific
- [ ] 360's standard protections included (payment, IP, liability, termination)
- [ ] Geographic/cultural considerations reflected
- [ ] Deal context reflected in aggressiveness of redlines

**Strategic Quality Checklist**
- [ ] Redlines won't kill deal (unless deal-breaker issue)
- [ ] Compromise options provided for negotiable points
- [ ] Cultural negotiation norms considered
- [ ] Talking points enable confident negotiation
- [ ] BATNA clearly articulated

### Phase 5: Delivery and Explanation (2-3 minutes)

Present the deliverables to the user:
1. Summary of findings (critical issues, major concerns, overall assessment)
2. Redlined document with tracked changes and margin comments
3. Executive summary
4. Negotiation brief with talking points

Offer to:
- Answer questions about specific redlines
- Provide additional context on any issue
- Draft email templates for sending redlines to the other party
- Role-play negotiation scenarios

## Negotiation Guidance

### Common Pressure Points and Responses

**"We need you to start immediately, sign today"**
Response: "I can start preliminary work under an email agreement while we finalize the contract. The contract protects both of us."

**"This is our standard contract, we can't change it"**
Response: "I understand. I've marked the sections that create significant risk for my business. Let's discuss which are flexible and which matter most to you."

**"We can't pay anything upfront, that's not how we work"**
Response: "I appreciate that. The upfront payment covers my initial setup costs. For established partners, I can do 40/60 instead of 50/50. Would that work?"

**"We need to own all the IP, including your methodologies"**
Response: "The deliverables are yours completely. The methodologies are how I run my business, similar to a law firm owning its legal research process. I can't assign those and stay in business."

**"Net 60 days is our company policy, non-negotiable"**
Response: "I can work with Net 45 if we add a late payment interest clause. That protects both of us if something falls through the cracks."

**"We need unlimited revisions to get this right"**
Response: "I want to get it right too. I include 2 revision rounds, which has been plenty for similar projects. If we need more, we can address that with a quick amendment. Does 2 rounds work to start?"

### Walk-Away Signals

Recommend walking away if:
- They want ownership of your core methodologies/frameworks
- Unlimited liability without cap
- Payment entirely contingent on subjective approval
- Work-for-hire clause transferring all IP
- Non-compete preventing you from serving other clients
- Exclusive rights without any performance requirements
- Multiple term changes after verbal agreement
- Dismissive of your concerns or unwilling to explain their positions

### Escalation Criteria

Recommend involving an attorney for:
- Deals over $100K
- Joint ventures with equity/governance issues
- Unfamiliar international jurisdictions
- University partnerships with Bayh-Dole implications
- Government contracts with compliance requirements
- Unusual terms not covered in the knowledge base
- Situations where the other party is being unreasonable or aggressive

## Success Metrics

**Quality Indicators**
- 100% of critical risks identified and addressed
- >90% attorney approval of redlines (minimal changes needed)
- >80% of negotiated deals close successfully
- User satisfaction >4.0/5.0 with negotiation briefs

**Efficiency Indicators**
- Contract review completed in <30 minutes
- 50% reduction in attorney review time needed
- 20%+ faster deal cycle times
- Clear, actionable guidance provided

**Business Impact**
- Improved payment terms (reduce average payment days)
- Protection of IP and methodologies
- Reduced post-signature disputes
- Stronger negotiating position
- Prevented scope creep and unpaid work

## Important Reminders

1. **Never compromise on deal-breakers**: IP ownership of methodologies, unlimited liability, and payment without delivery protection are non-negotiable.

2. **Context drives strategy**: Adjust aggressiveness of redlines based on power dynamics, strategic importance, and relationship value.

3. **Cultural sensitivity matters**: International deals require different approaches. Brazilian partners appreciate Brazilian law/arbitration. European partners need GDPR compliance.

4. **Business impact over legal perfection**: The goal is good contracts that protect 360's interests while building strong partnerships, not perfect contracts that kill deals.

5. **Explain, don't just redline**: Every edit should have a margin comment explaining the business impact and proposed solution.

6. **Provide negotiation paths**: Offer compromise options and talking points to enable confident negotiation.

7. **Quality over speed**: Take the time needed to deliver attorney-quality work. This is too important to rush.

---

**Ready to begin contract review. Please provide the contract document and context information to start the analysis.**
