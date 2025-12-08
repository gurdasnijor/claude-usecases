---
name: 990-ez-preparation
description: Automated IRS Form 990-EZ preparation and review system that streamlines nonprofit tax compliance through intelligent data collection, multi-level validation, and expert guidance. (project)
---

# IRS Form 990-EZ Preparation Skill

## Skill Identity

**Name**: 990-ez-preparation
**Version**: 1.0
**Created**: November 2025
**For**: 360 Social Impact Studios and nonprofit organizations

## Skill Purpose

This skill transforms the complex 990-EZ tax preparation process into an automated, intelligent workflow. It guides organizations through eligibility verification, data collection, form population, compliance validation, and filing package generation—reducing preparation time from 40+ hours to under 10 hours while ensuring regulatory compliance.

## When to Activate This Skill

Trigger this skill when the user requests:
- "Prepare our 990-EZ for [year]"
- "Help with our annual tax filing"
- "Generate Form 990-EZ"
- "Start nonprofit tax return preparation"
- "Check 990-EZ eligibility"
- Any variation requesting IRS Form 990-EZ preparation

Also trigger proactively:
- 60 days before the filing deadline (May 15 for calendar year orgs)
- When user mentions "990" or "nonprofit tax return"
- During annual compliance planning discussions

## Core Capabilities

1. **Automated Eligibility Verification**: Checks gross receipts, total assets, and special conditions
2. **Multi-Source Data Collection**: Guides extraction from QuickBooks, Asana, Google Drive, and other sources
3. **Intelligent Form Population**: Maps collected data to all 990-EZ form sections
4. **Multi-Level Validation**: Mathematical, regulatory, narrative, and strategic compliance checks
5. **Schedule Generation**: Automatically creates required Schedules A, B, and O
6. **Expert Guidance**: Tax compliance, governance, and strategic reporting perspectives
7. **Filing Package Creation**: Complete package with all schedules and documentation

## 5-Phase Workflow

### Phase 1: Eligibility Verification & Initial Assessment

**Step 1.1: Gather Organization Information**

Ask user:
1. What is your organization's legal name and EIN?
2. What tax year are you preparing? (e.g., 2024)
3. What is your fiscal year end date? (usually 12/31 for calendar year)
4. What is your 501(c) classification? (typically 501(c)(3))
5. Do you have QuickBooks data available, or will you provide financial summaries?

**Step 1.2: Check 990-EZ Eligibility**

Verify the organization qualifies for Form 990-EZ (not full 990):

```python
eligibility_criteria = {
    'gross_receipts': {
        'threshold': 200000,
        'current_year': None,  # To be collected
        'question': 'What were your gross receipts for the tax year?'
    },
    'total_assets': {
        'threshold': 500000,
        'end_of_year': None,  # To be collected
        'question': 'What were your total assets at year end?'
    },
    'disqualifying_conditions': [
        'Are you a donor advised fund sponsor?',
        'Do you operate hospital facilities?',
        'Are you a supporting organization (509(a)(3))?'
    ]
}
```

**Eligibility Decision Tree:**
- If gross receipts >= $200,000: "You must file Form 990, not 990-EZ"
- If total assets >= $500,000: "You must file Form 990, not 990-EZ"
- If donor advised fund sponsor: "You must file Form 990"
- If hospital operator: "You must file Form 990"
- Otherwise: "You qualify for Form 990-EZ ✓"

**Step 1.3: Set Up Data Collection Plan**

Based on available data sources, create collection plan:

**Option A: QuickBooks Integration** (if available)
- Connect to QuickBooks via MCP or export
- Pull Profit & Loss Statement (full year)
- Pull Balance Sheet (beginning and end of year)
- Pull Transaction Detail by Account
- Pull Donor/Revenue Detail

**Option B: Manual Data Entry** (fallback)
- Provide structured data collection template
- Request financial statements
- Request program documentation
- Request governance documents

Say: "I'll guide you through collecting the necessary data. We'll need:
1. Financial data (revenue, expenses, assets, liabilities)
2. Program accomplishment information
3. Governance information (officers, directors, policies)
4. Grant and donor information (for Schedule B)

Do you have QuickBooks, or would you prefer to provide financial summaries manually?"

---

### Phase 2: Data Collection & Organization

**Step 2.1: Financial Data Collection**

**Revenue Sources** (Part I, Lines 1-4):
- Contributions, gifts, grants (Line 1)
- Program service revenue (Line 2)
- Investment income (Line 3)
- Other revenue (Line 4)

For each revenue source, ask:
- "What were your total contributions/grants received?"
- "Did you receive any program service revenue (fees for services)?"
- "Did you earn investment income (interest, dividends)?"
- "Any other revenue sources?"

**Expense Categories** (Part I, Lines 10-16):
- Program service expenses (Line 10)
- Management and general expenses (Line 13)
- Fundraising expenses (Line 14)

Guide functional allocation:
"Expenses must be allocated to program services, management/general, and fundraising. Best practice: Aim for 65%+ program services.

- Program services: Direct costs of mission activities
- Management & general: Overhead, governance, administration
- Fundraising: Solicitation costs, donor stewardship

What were your expenses in each category?"

**Balance Sheet Data** (Part II):
- Cash and savings (beginning and end of year)
- Accounts receivable
- Other assets
- Accounts payable
- Other liabilities

**Step 2.2: Program Accomplishment Data Collection**

For Part III (Program Service Accomplishments), gather:

"Form 990-EZ requires description of your program accomplishments. For up to 3 major programs, I need:
1. Program description (what you do, who you serve)
2. Expenses allocated to this program
3. Revenue generated by this program (if any)
4. Measurable accomplishments (beneficiaries served, outcomes achieved)

Example: 'Technology validation services for life science startups: Served 15 ventures, validated 8 technologies, leveraged $2.4M in follow-on funding. Expenses: $45,000. Revenue: $12,000.'"

**Step 2.3: Governance & Compliance Data Collection**

**Officers, Directors, and Key Employees** (Part IV):
For each person, collect:
- Name
- Title/Position
- Hours per week devoted to position
- Compensation (if any - most small nonprofit boards are unpaid)
- Are they related to other officers/directors?

**Other Information** (Part V - 47 questions):
The skill will ask targeted questions from the Part V matrix, such as:
- "Did you engage in direct/indirect political campaign activities?"
- "Did you engage in lobbying activities?"
- "Do you have a written conflict of interest policy?"
- "Do you have a written whistleblower policy?"
- "Did you make grants or assistance to individuals in the U.S.?"

**Step 2.4: Donor/Grant Information for Schedule B**

If contributions from any single source >= $5,000:
"You'll need to file Schedule B listing contributors of $5,000+. I'll need:
- Donor/grantor name and address
- Contribution amount
- Type (cash, noncash, or both)

Note: Schedule B is NOT public - it's only submitted to the IRS."

**Step 2.5: Data Organization & Gap Identification**

Organize all collected data into structured format:

```yaml
organization:
  name: "360 Social Impact Studios"
  ein: "XX-XXXXXXX"
  tax_year: 2024
  fiscal_year_end: "12/31/2024"

financial:
  revenue:
    contributions: 75000
    program_service_revenue: 45000
    investment_income: 1200
    other_revenue: 0
    total: 121200

  expenses:
    program_services: 85000
    management_general: 25000
    fundraising: 8000
    total: 118000

  balance_sheet:
    beginning_of_year:
      cash: 15000
      assets: 18000
    end_of_year:
      cash: 18200
      assets: 21200

programs:
  - description: "Technology validation for life science ventures"
    expenses: 65000
    revenue: 35000
    accomplishments: "Served 15 ventures..."
```

Flag any missing data:
"⚠️ I need the following information to complete the form:
- [List gaps]

Can you provide these details?"

---

### Phase 3: Form Population & Calculation

**Step 3.1: Generate Part I - Revenue, Expenses, and Changes in Net Assets**

Calculate all totals and net income:

```python
# Part I Calculations
total_revenue = sum(all_revenue_sources)  # Line 9
total_expenses = sum(all_expense_categories)  # Line 17
excess_or_deficit = total_revenue - total_expenses  # Line 18
net_assets_beginning = prior_year_net_assets  # Line 19
net_assets_ending = net_assets_beginning + excess_or_deficit  # Line 21
```

**Step 3.2: Generate Part II - Balance Sheet**

```python
# Part II Calculations
total_assets = cash + receivables + other_assets  # Line 25
total_liabilities = payables + other_liabilities  # Line 27
net_assets = total_assets - total_liabilities  # Line 28
```

Validate: Does Line 28 (Part II net assets) = Line 21 (Part I ending net assets)?

**Step 3.3: Generate Part III - Program Service Accomplishments**

Format program descriptions:
- Clear, concise narrative
- Quantifiable outcomes
- Alignment with mission
- Professional tone suitable for public disclosure

**Step 3.4: Generate Part IV - Officers, Directors, Key Employees**

Format officer table with:
- Name and title
- Average hours per week
- Reportable compensation
- Proper classification (officer, director, trustee, key employee)

**Step 3.5: Complete Part V - Other Information**

Process all 47 yes/no questions with intelligent defaults:
- Most small nonprofits answer "No" to political activity
- Most should answer "Yes" to conflict of interest policy
- Determine Schedule A requirement (always "Yes" for 501(c)(3))
- Determine Schedule B requirement (if any contributor >= $5,000)

---

### Phase 4: Multi-Level Validation

**Step 4.1: Level 1 - Mathematical Accuracy**

Verify all calculations:
- Revenue line items sum to total revenue
- Expense line items sum to total expenses
- Balance sheet equation balances (Assets = Liabilities + Net Assets)
- Net assets reconcile between Part I and Part II
- Beginning net assets + excess/deficit = ending net assets

**Step 4.2: Level 2 - Regulatory Compliance**

Check IRS requirements:

```yaml
compliance_checks:
  public_support_test:  # For 501(c)(3) organizations
    threshold: 0.333  # 33.33% public support required
    status: "Check Schedule A calculation"

  expense_allocation:
    program_minimum: 0.65  # Recommended 65%+ for charity ratings
    fundraising_maximum: 0.35  # Should not exceed 35%

  compensation_reasonableness:
    key_employee_threshold: 150000
    documentation_required: "Comparability data for compensation >$150K"

  governance_policies:
    required:
      - conflict_of_interest
      - whistleblower  # Recommended
      - document_retention  # Recommended
```

Flag warnings:
- "⚠️ Program expense ratio is 52%, below recommended 65%"
- "⚠️ No conflict of interest policy documented"
- "✓ All mathematical validations passed"

**Step 4.3: Level 3 - Narrative Quality**

Review program descriptions for:
- Clarity and specificity
- Quantifiable accomplishments
- Alignment with mission
- Public disclosure appropriateness
- Professional tone

Suggest improvements:
"Consider strengthening the program description by adding specific metrics:
- Number of beneficiaries served
- Measurable outcomes achieved
- Geographic reach or impact scope"

**Step 4.4: Level 4 - Strategic Alignment**

Check for:
- Expense allocation aligns with strategic priorities
- Revenue diversification (not overly dependent on one source)
- Financial sustainability indicators
- Governance best practices
- Donor transparency considerations

**Step 4.5: Generate Validation Report**

```markdown
## 990-EZ Validation Report

### Mathematical Accuracy ✓
- All calculations verified
- Balance sheet balances
- Net assets reconcile

### Regulatory Compliance
✓ Eligible for 990-EZ (receipts: $121,200 < $200,000)
✓ Public support test (pending Schedule A calculation)
⚠️ Program expense ratio: 72% (target: 65%+) ✓
⚠️ Missing whistleblower policy (recommended)

### Narrative Quality
✓ Program descriptions are clear and specific
✓ Accomplishments are quantified
→ Consider adding beneficiary testimonial data

### Strategic Indicators
✓ Revenue diversification: 62% contributions, 37% earned, 1% investment
✓ Financial sustainability: Positive net income ($3,200)
✓ Governance: Board independence maintained

### Action Items
1. Develop whistleblower policy before filing
2. Consider highlighting revenue diversification to donors
3. Document decision-making process for Schedule A calculation
```

---

### Phase 5: Schedule Generation & Filing Package

**Step 5.1: Generate Schedule A (Public Charity Status)**

For 501(c)(3) organizations, Schedule A is required to demonstrate public charity status.

Calculate public support percentage:
```python
# 5-year public support test
public_support = sum_5_years(contributions + grants + program_revenue)
total_support = public_support + sum_5_years(investment_income + other_income)
public_support_percentage = public_support / total_support

if public_support_percentage >= 0.3333:
    status = "Passes public support test"
else:
    status = "May need facts and circumstances test"
```

**Step 5.2: Generate Schedule B (Contributors)**

If any contributor gave >= $5,000:

```markdown
### Schedule B - Schedule of Contributors

**Contributor 1**
Name: [REDACTED FOR PUBLIC COPY]
Address: [REDACTED FOR PUBLIC COPY]
Amount: $25,000
Type: Cash

**Contributor 2**
Name: [REDACTED FOR PUBLIC COPY]
Address: [REDACTED FOR PUBLIC COPY]
Amount: $15,000
Type: Cash
```

Note: Schedule B is submitted to IRS but NOT made public.

**Step 5.3: Generate Schedule O (Supplemental Information)**

Use Schedule O for:
- Additional explanation of program accomplishments
- Governance policies and procedures
- Explanation of significant expenses
- Explanation of compensation methodology
- Any other supplemental information

**Step 5.4: Create Filing Package**

Assemble complete package:

```yaml
filing_package:
  primary_form:
    - Form_990-EZ_2024.pdf

  required_schedules:
    - Schedule_A_Public_Charity_Status.pdf
    - Schedule_B_Contributors.pdf  # IRS only, not public

  optional_schedules:
    - Schedule_O_Supplemental_Information.pdf

  supporting_documentation:
    - financial_statements.pdf
    - board_minutes_approving_filing.pdf
    - governance_policies.pdf

  public_disclosure_copy:
    - Form_990-EZ_Public_Disclosure.pdf  # Without Schedule B

  state_filings:  # If applicable
    - california:
        form: RRF-1
        deadline: "2025-05-15"
        fee: 25
```

**Step 5.5: Pre-Filing Checklist**

Present comprehensive checklist:

```markdown
## Pre-Filing Checklist for Form 990-EZ

### Form Completeness
- [ ] All required fields completed
- [ ] All schedules attached
- [ ] Officer signatures obtained (President/CEO and Treasurer)
- [ ] Form dated

### Accuracy Verification
- [ ] EIN is correct
- [ ] Organization name matches IRS records
- [ ] Tax year is correct
- [ ] All financial figures verified against source documents
- [ ] Mathematical accuracy confirmed

### Supporting Documentation
- [ ] Financial statements prepared
- [ ] Board minutes approving filing obtained
- [ ] Governance policies documented
- [ ] Prior year 990 reviewed for consistency

### Compliance Requirements
- [ ] Public support test documented (Schedule A)
- [ ] Contributors $5,000+ listed (Schedule B)
- [ ] Expense allocation methodology documented
- [ ] Compensation decisions documented

### Filing Logistics
- [ ] Filing deadline confirmed (typically May 15)
- [ ] Extension filed if needed (Form 8868)
- [ ] State filing requirements identified
- [ ] Public disclosure copy prepared (without Schedule B)

### Post-Filing
- [ ] Copy retained for organization's records
- [ ] Public disclosure copy available for inspection
- [ ] State filings completed
- [ ] 990 posted to GuideStar/Charity Navigator
```

**Step 5.6: Provide Final Deliverables**

Say: "Your Form 990-EZ filing package is complete!

**Filing Summary**:
- Tax Year: 2024
- Gross Receipts: $121,200
- Total Assets: $21,200
- Net Income: $3,200
- Filing Deadline: May 15, 2025

**Package Contents**:
1. Form 990-EZ (complete)
2. Schedule A (Public Charity Status)
3. Schedule B (Contributors - IRS only)
4. Schedule O (Supplemental Information)
5. Public Disclosure Copy (without Schedule B)
6. Supporting documentation
7. Pre-filing checklist
8. Validation report

**Next Steps**:
1. Review all documents for accuracy
2. Obtain board approval (recommended)
3. Obtain officer signatures
4. File electronically via IRS e-file system or authorized provider
5. Complete any required state filings
6. Retain copies for your records

**Key Findings**:
- ✓ Organization qualifies for 990-EZ
- ✓ Passes all mathematical validations
- ✓ Meets public support test
- ⚠️ Consider developing whistleblower policy

Would you like me to explain any section of the form or help with state filing requirements?"

---

## Success Metrics

A successful 990-EZ preparation achieves:
- ✓ Generated in <10 hours (vs. 40+ hours manual)
- ✓ 100% mathematical accuracy
- ✓ Zero IRS validation errors
- ✓ Passes all compliance checks
- ✓ Professional narrative quality
- ✓ Complete filing package ready
- ✓ Board-ready presentation of results
- ✓ Clear documentation of methodology
- ✓ Confidence in public disclosure
- ✓ Reduced professional fees (if applicable)

---

*Built for nonprofit excellence and regulatory compliance*
*Skill version 1.0 | November 2025*
