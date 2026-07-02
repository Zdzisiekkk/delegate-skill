# Example 2: Market Entry Strategy (Business Context)

## Scenario

Your SaaS product is popular in the US. Now you're considering Europe.

This is NOT a coding task, but `/delegate` works great for business too:
- Multi-step decision (market selection, pricing, partnerships, go-to-market)
- High cost of mistakes (wasted marketing budget, wrong partnerships, failed launches)
- Requires research and strategic thinking
- Ambiguous requirements (no "right" answer, need to weigh tradeoffs)

Perfect for Fable to think through deeply, then... you need to decide which way to go.

## The Ask

```
/delegate

We're expanding our project management SaaS to Europe. 
I need a go-to-market strategy covering:

1. Which European markets to enter first (and in what order)
2. Pricing strategy (adapt from US or tier differently)
3. Go-to-market approach (direct sales, partnerships, self-serve)
4. Key market-entry risks and how to mitigate

Context:
- US: $2M ARR, 500 SMB customers, self-serve + sales hybrid
- Product: Slack-first project management, no vertical specificity
- Constraints: $200k budget for EU launch, 2-person team
- Timeline: Want to launch in first market in 6 months

I need actionable recommendations, not just analysis.
```

## Step 1: Fable Analyzes

Fable thinks deeply and returns:

```
## Understanding

European expansion requires balancing market size, competition, 
regulatory complexity, and team capacity. Wrong market choice could 
waste budget; right one could 2x revenue in 18 months.

This is a strategic decision with competing frameworks:
- Market size argument: go for UK/Germany (big, English-speaking)
- Risk argument: start with smaller, simpler market (Poland, Czechia)
- Regulatory argument: GDPR/DPA complexity varies by country

## Research & Analysis

Will examine:
- European market size and SaaS adoption by country
- Competitive landscape (Asana, Monday, Notion footprint)
- Regulatory complexity (GDPR, data residency)
- Pricing precedent in each market
- Channel viability (your 2-person constraint)

Findings inform recommendations on tradeoffs.

## Strategic Framework

**Market Selection Criteria:**
1. Market size (ARR potential)
2. Competition intensity
3. Channel fit (partnerships vs direct)
4. Regulatory simplicity
5. Language/market maturity for SaaS

**Recommendation Structure:**
- Tier 1 (first market): best tradeoff of size vs feasibility
- Tier 2 (second market): next best, following same go-to-market
- Tier 3 (expansion markets): after team growth

**Go-to-Market by Market Type:**
- If partnership-heavy: VARs, consultants, agencies
- If direct-heavy: content, PPC, sales
- Your constraint: likely partnership + content (cheapest at scale)

## Success Criteria

- Recommendations rank markets with reasoning
- Pricing strategy includes: floor, ceiling, how it adapts from US
- Go-to-market details: channel, budget allocation, timeline
- Risk register: regulatory, competitive, execution risks + mitigations
- All grounded in actual market data, not speculation

## Risks & Mitigation

- **Risk:** Market data outdated or incomplete
  → **Mitigation:** Use 2024+ sources, triangulate multiple data points

- **Risk:** Recommendations assume wrong go-to-market channel
  → **Mitigation:** Provide channel analysis; you decide based on your strengths

- **Risk:** GDPR/regulatory complexity underestimated
  → **Mitigation:** Research actual data residency requirements by country

## Model Recommendation

**Opus 4.8** — This task requires:
- Synthesizing competing market theories (market size vs. risk vs. regulation)
- Making strategic judgment calls with incomplete information
- Balancing tradeoffs that have no "objectively best" answer
- Creative thinking about go-to-market channels
- Recommending a path despite inherent ambiguity

This isn't mechanical execution—it's strategic thinking.
```

## Step 2: You Review & Evaluate

Claude summarizes:

```
📋 EUROPE GO-TO-MARKET STRATEGY

Objective: Identify entry market, pricing, and go-to-market approach 
for European expansion within $200k budget and 2-person team constraint.

Main Steps:
1. Research market size and SaaS adoption across key European countries
2. Analyze competition intensity and pricing precedent
3. Evaluate regulatory complexity (GDPR, data residency)
4. Define pricing strategy (adapt from US or tier differently)
5. Recommend go-to-market channel per market
6. Create 18-month roadmap: which markets in which order

Recommended Model: Opus 4.8
Reason: Strategic decision with competing tradeoffs. No single "right" 
answer. Needs judgment on market opportunity vs. execution risk vs. 
regulatory complexity. Requires synthesizing incomplete information.

⚠️ Risks:
- Market data may be 2023 (potentially stale)
- Go-to-market depends on your team's actual capabilities
- Regulatory complexity could change month-to-month
```

**You choose:** "Execute with Opus 4.8 — looking forward to seeing the analysis"

## Step 3: Opus Thinks & Researches

Opus receives full plan and works through it systematically:

```
### Researching European market size and adoption

Analyzing SaaS adoption rates by country (2024 data):
- UK: Highest (mature market, English-speaking, similar to US)
- Germany: Large market, strong tech sector, good SaaS adoption
- France: Sizeable, French-preferred language (small friction)
- Poland: Growing, lower price sensitivity, emerging SaaS market
- Nordics (Sweden, Denmark): Small but highest SaaS maturity

### Evaluating competitive landscape

UK/Germany: Heavy competition (Asana, Monday.com, Notion all localized)
Poland/Czech: Lower competition, less localized offerings
France: Competitive but fragmented (some local players)

### Regulatory analysis

GDPR: All countries equal (EU-wide regulation)
Data residency: 
  - Germany: Strong preference for German data centers (regulatory)
  - Nordics: Often German or Swedish data center acceptable
  - Poland/Czech: Less strict than Germany

### Market sizing by country

UK Market: ~£2B SaaS market, 8% growth
  → Your share potential: £5-10M by year 3 if successful
Germany: €1.8B SaaS, 6% growth
  → Lower growth than UK
Poland: €200M but 15% growth (faster growing)
  → Smaller market but momentum

### Strategic Analysis: Tradeoffs

**Market Size vs. Feasibility:**
UK (best size, highest competition, no special challenges)
Poland (smaller, lower competition, growing, simpler entry)

**Recommendation:** Start in UK for size, but...
**Caveat:** UK competition is intense. Consider Poland-first for easier traction.

[Opus continues detailed analysis of pricing, channels, risks...]
```

## Step 4: Output & Recommendations

Opus delivers something like:

```
EUROPEAN GO-TO-MARKET STRATEGY — OPUS ANALYSIS

## Primary Recommendation: UK-First Launch (with Poland as Tier 2)

**Tier 1: Launch UK (Month 1-6)**
- Market size: £2B+ SaaS market
- Competition: High (Asana, Monday, Notion dominant)
- Go-to-market: Content + strategic partnerships
- Pricing: Adapt from USD (~15-20% premium for local market)
- Budget allocation: 60% content/SEO, 30% partnership dev, 10% events
- Rationale: Size justifies competition; English language removes friction

**Tier 2: Launch Poland (Month 7-12)**
- Market size: €200M but 15% YoY growth (fastest in analysis)
- Competition: Lower (Asana has limited Polish presence)
- Go-to-market: Local partnerships + translation
- Pricing: 20% discount from UK (lower willingness to pay)
- Budget allocation: 40% partnerships, 40% translation/localization, 20% community
- Rationale: Momentum, lower competition, easier traction for 2-person team

**Tier 3: Germany (Month 13+)**
- After team grows to 3-4 people
- Market size: €1.8B but slower growth
- Go-to-market: Partner with German consultancies (GDPR expertise)
- Special requirement: German data residency (cost: ~15% infrastructure premium)

## Regulatory Considerations

- GDPR: All countries require full GDPR compliance (you already have)
- Data residency:
  - UK: No requirement (post-Brexit, but UK data standard acceptable)
  - Germany: Strong preference for data in Germany (±10% customers factor this in)
  - Poland: EU standard acceptable (any EU data center)
- Action: Plan German data center by Month 12 if Germany launch appears viable

## Pricing Strategy

**Base pricing (UK):** Adapt from USD
- Starter: $29 USD → £24 (vs. simple conversion)
- Pro: $99 USD → £79 (15% premium for local market + VAT considerations)
- Enterprise: Custom (same as US)

**Poland pricing:** 20% discount
- Reflects lower willingness-to-pay
- Matches Intercom, Slack local pricing patterns

**Germany pricing:** Same as UK (not lower than Poland despite size)

## Go-to-Market Channel Analysis

Given your 2-person constraint:

**UK:** Content-first (SEO, blog) + Partnership development
- Budget: £12k/month for freelance copywriter + agency retainer
- Timeline: 3 months to first meaningful traction
- Why: Scalable without more headcount

**Poland:** Partnership-first (SaaS agencies, consultancies)
- Budget: £6k/month for in-country partner vetting + onboarding
- Timeline: 1-2 months to first partner agreement
- Why: Easier with small team; partners handle sales

## Risk Register & Mitigations

| Risk | Impact | Probability | Mitigation |
|------|--------|------------|-----------|
| Competition steals share | Loss of Tier 1 investment | Medium | Focus on SMB segment (your strength) |
| UK acquisition costs higher than US | Burn through budget faster | Medium | Set customer acquisition limit; pivot to Poland earlier if needed |
| Regulations change (Brexit follow-up) | Compliance headache | Low | Monitor FCO guidance; get legal review Q1 2025 |
| Partner quality issues in Poland | Time waste, customer damage | Medium | Vet carefully; start with 1-2 pilots |
| Team burnout (2 people launching EU) | Execution fails | High | Hire contractor support Month 3; expect 60-hour weeks initially |

## Next Steps

**Month 1:** 
- Finalize UK pricing and messaging
- Hire freelance copywriter for UK content
- Begin partner research in Poland

**Month 2-3:**
- Launch UK content campaign
- First Poland partnership discussions
- Monitor UK CAC and adjust if > $300

**Month 4-6:**
- Evaluate UK traction; decide on Poland timing
- If UK slower than expected, accelerate Poland (lower CAC)
- If UK exceeds targets, stay focused; Poland follows

## Confidence Level

High confidence on market prioritization and competitive analysis.
Medium confidence on pricing (will need to validate with early customers).
Low confidence on go-to-market channel timing (depends on your sales skills/resources).

Recommend: Launch UK, measure for 2 months, pivot to Poland if CAC too high.
```

## Step 5: You Make the Decision

Unlike execution, this output is research + recommendation.

**Your next move:** You decide:
- ✅ Do we go UK-first as recommended?
- ✅ Or accelerate Poland (Opus made good case for lower competition)?
- ✅ Or do something else (third market, different channels)?

Opus did the strategic thinking. Now you decide based on your board, your risk appetite, your market sense.

---

## Why This Worked

✅ **Fable couldn't have executed this alone** (too much ambiguity)
✅ **Opus's strategic thinking** was necessary (you're not just following a plan)
✅ **Output is actionable** (specific markets, pricing, risks, timeline)
✅ **Cost-efficient** — research + thinking for a decision with $200k+ consequences

## Key Insight

`/delegate` isn't just for code. It works great for business strategy:
- Research-heavy tasks → Fable plans, cheaper model executes research
- Strategy tasks with ambiguity → Fable plans + Opus does strategic thinking
- Multi-stakeholder decisions → Use output to get buy-in from team

---

## Follow-Up Tasks

After launching UK, you might `/delegate`:

```
/delegate

UK launch is 3 months in. CAC is £450 (higher than expected $300).
Conversion rate is 2.1% (strong). But we're burning budget faster.

Should we:
A) Pivot to Poland launch earlier (lower CAC)
B) Double down on UK but optimize CAC
C) Pause UK, try Germany instead

Provide analysis of each option given: current metrics, budget remaining, 
team capacity, and market conditions.
```

Same pattern — research + strategic thinking for another decision.
