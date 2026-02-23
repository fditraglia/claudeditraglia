# Nairobi Digital Futures — Research Design & Progress

*This is a synthetic example showing what a living research design document looks like after several weeks of `/weekly-review` updates. The project, team, and data are entirely fictional — names, institutions, and details do not correspond to any real study. The structure and level of detail are realistic.*

---

## Project State

| Field | Value |
|-------|-------|
| Last updated | 2026-02-14 |
| Updated by | Claude Code /weekly-review |
| Primary owner | Sarah Okonkwo |
| Co-PI | James Mwangi (University of Nairobi) |
| Research Manager | Lisa Park (IPA Kenya) |
| Review cadence | Weekly (Wednesdays) |

### Change Log (Recent)

| Date | Change | Source |
|------|--------|--------|
| 2026-02-14 | Added list experiment design for midline; updated power calcs with actual ICC | Weekly review |
| 2026-02-07 | Updated Cohort 2 screening progress; flagged trainer fidelity issue | Weekly review |
| 2026-01-31 | Added Cohort 1 baseline balance table; confirmed IDRC supplemental | Weekly review |
| 2026-01-17 | Initial document creation from project setup + historical materials | /setup-project-management |

---

## Section 0: Strategic Orientation

### North Star
Estimate the causal impact of a digital financial literacy + mobile savings program ("Jipange") on savings behavior, income, and economic empowerment among women market vendors in Nairobi, Kenya — and identify which program components drive the effects.

### Why This Matters
Kenya has one of the highest mobile money penetration rates in the world, yet women in informal markets remain largely excluded from formal financial services. Over 60% of women market vendors in Nairobi rely on informal lenders with predatory interest rates. Existing financial inclusion programs focus on access (opening accounts); evidence on comprehensive digital literacy + behavioral savings interventions for informal-sector women is limited. This study fills a critical gap: can an integrated program that combines digital skills, financial management training, and commitment savings devices shift women from informal to formal financial tools — and does that translate to higher savings and income? The staggered rollout and component analysis aim to answer not just "does it work" but "what works and for whom."

### Critical Success Factors
1. Market association trust and cooperation (especially across competing vendor groups)
2. Training fidelity — trainer quality determines whether the program is delivered as designed
3. Measurement of sensitive financial outcomes (income, savings, informal borrowing) with minimal bias
4. Cohort enrollment and retention across all three waves
5. Timely funding disbursements to prevent operational gaps

---

## Section 1: Executive Snapshot

### Study Design at a Glance

| Element | Detail |
|---------|--------|
| Design | Cluster RCT, market-cluster randomization, staggered rollout |
| Location | Nairobi, Kenya (Gikomba Market, Eastleigh, Kawangware) |
| Sample | ~1,200 women market vendors, 18 market clusters, 3 cohorts of ~400 |
| Intervention | "Jipange" — 12-week program: 4 weeks digital literacy, 4 weeks financial management, 4 weeks M-Pesa savings commitment device |
| Control | Waitlist (receives program in subsequent cohort phase) |
| Randomization | Market-cluster level, stratified by market area and baseline savings rates |
| Primary outcomes | Savings index, income index, financial empowerment index |
| Secondary outcomes | Financial stress (PSS-F adapted), digital skills proficiency, borrowing composition, business investment |
| Measurement | Baseline, midline (4 months post-randomization), endline (12 months), long-run follow-up (24 months, funding dependent) |
| Pre-registration | AEA Registry #AEARCTR-0000000 (registered Jan 2026, update pending for midline changes) |

### Current Status by Phase

| Phase | Status | Key Metric |
|-------|--------|------------|
| Cohort 1 enrollment | Complete | 380/400 (95%) |
| Cohort 1 baseline | Complete | 97% response rate |
| Cohort 1 program | In progress (week 9/12) | 76% avg attendance |
| Cohort 1 midline | Planned Apr 2026 | Instrument in revision |
| Cohort 2 screening | In progress | 290/~400 screened (73%) |
| Cohort 2 randomization | Planned Mar 15 | Protocol drafted |
| Cohort 3 | Planning | Market mapping underway |

### Team

| Role | Name | Affiliation | Focus |
|------|------|-------------|-------|
| PI | Sarah Okonkwo | Georgetown McCourt School | Design, analysis, donor relations |
| Co-PI | James Mwangi | University of Nairobi | Program design, qualitative component, trainer supervision |
| Research Manager | Lisa Park | IPA Kenya | Field operations, data management, screening |
| Field Researcher | Faith Wambui | IPA Kenya | Market relations, logistics, Cohort 3 mapping |
| RA (Survey) | Priya Sharma | Georgetown | Survey design, SurveyCTO programming, midline pilot |
| RA (Data) | Daniel Ochieng | Georgetown | Attendance tracking, data cleaning, trainer analysis |
| RA (Qualitative) | Grace Njeri | University of Nairobi | Qualitative interviews, transcript processing |

---

## Section 2: Paper Plan

### Track A: Predictive / Descriptive Papers

#### Paper A1: "Measuring Financial Capability Among Informal-Sector Women: Validating an Adapted Assessment Tool"

**Status:** Data collection complete (Cohort 1 baseline + screening data). Analysis planned for Q3 2026.

**Research question:** How well does an adapted FINDEX-based financial capability assessment predict savings behavior and financial resilience among women market vendors in Nairobi, and which capability dimensions are most predictive?

**Design:** Predictive validity study using Cohort 1 screening scores (pre-randomization) to predict baseline savings behavior and M-Pesa transaction patterns. Compare performance to the original instruments validated in nationally representative samples.

**Key data:**
- Screening scores for 380 Cohort 1 participants (adapted FINDEX assessment, 28 items)
- Baseline self-reported savings and income (5-item index, with caveats about response rates)
- Safaricom M-Pesa transaction summaries (pending data sharing agreement — Lisa following up)
- Market-level economic data from the Kenya National Bureau of Statistics

**Identification:** Predictive validity (AUC, sensitivity, specificity). Machine learning comparison (LASSO, random forest) to assess whether the full instrument outperforms a reduced-form version.

**Target journals:** World Development, Journal of Development Economics

**Collaborators:** James Mwangi (lead author), Sarah Okonkwo, Lisa Park

---

#### Paper A2: "Who Saves? Financial Behavior, Social Networks, and Market Context Among Nairobi's Women Vendors"

**Status:** Descriptive analysis pending. Awaiting Cohort 1 midline data for social network module.

**Research question:** What individual, household, and market-level factors predict savings behavior among women market vendors in Nairobi? How do social network structures differ between high-saving and low-saving vendors?

**Design:** Cross-sectional descriptive analysis using baseline + midline data. Social network analysis using the name generator module (midline instrument). Market-level analysis using cluster-level covariates.

**Key data:**
- Baseline survey (demographics, household, financial behavior) — n=380
- Midline social network module (collecting Apr 2026)
- Market mapping data (Faith's Cohort 3 prep work will generate cluster profiles)
- Endorsement experiment item on attitudes toward formal financial services (midline)

**Identification:** Descriptive — conditional correlations, network statistics, market-cluster variation. Not causal.

**Target journals:** World Development, Economic Development and Cultural Change

**Collaborators:** James Mwangi, Faith Wambui, Sarah Okonkwo

---

### Track B: Experimental Papers

#### Paper B1 (Main Paper): "Digital Literacy, Savings, and Economic Empowerment: Experimental Evidence from Nairobi's Markets"

**Status:** Pre-registered. Cohort 1 program in progress. First results expected Q4 2026 (midline) with full results Q2 2027 (all cohorts, endline).

**Research question:** Does the Jipange program increase savings, income, and economic empowerment among women market vendors in Nairobi?

**Design:** Cluster RCT with staggered rollout across 3 cohorts. Market-cluster randomization (18 clusters: 9 treatment, 9 control per cohort pair). Intent-to-treat analysis with complier average causal effect estimates.

**Primary outcome indices:**
1. Savings index (M-Pesa balance, formal savings account, savings frequency) — measured via combined direct report + M-Pesa records + list experiment at midline/endline
2. Income index (weekly revenue, profit margin, business investment) — self-report + M-Pesa transaction volumes
3. Financial empowerment index (financial decision-making autonomy, reduced reliance on informal lenders, business planning)

**Secondary outcomes:**
- Financial stress (adapted Perceived Stress Scale — Financial)
- Digital skills proficiency (practical assessment)
- Borrowing composition (formal vs. informal lending share)
- Business investment (inventory, equipment, new product lines)

**Power calculations (updated Feb 14, 2026):**
Using actual Cohort 1 ICC = 0.048 (baseline savings index):
- 18 market clusters, ~67 individuals per cluster
- MDE = 0.17 SD on savings index (80% power, 5% significance)
- MDE = 0.15 SD with baseline covariate adjustment (R-squared ~0.25)
- If Cohort 2+3 each reach 360 (minimum threshold), total N = 1,100 → MDE = 0.16 SD
- Power adequate for main effects. Heterogeneity analysis (by financial capability level, age, market area) will be underpowered — pre-registered as exploratory.

**Estimation strategy:**

Primary specification:
  Y_ic = alpha + beta * Treatment_c + gamma * X_i + delta * Stratification_s + epsilon_ic

Where:
- Y_ic is outcome for individual i in market cluster c
- Treatment_c is cluster-level treatment assignment
- X_i is a vector of baseline covariates (pre-registered: age, education, financial capability score, household size, years as vendor)
- Stratification_s are randomization strata fixed effects (market area x baseline savings rate)
- Standard errors clustered at market-cluster level

Robustness:
- Lee bounds for attrition
- Randomization inference (exact p-values given 18 clusters)
- LASSO-selected controls (Belloni et al. 2014)
- Cohort-specific estimates + pooled estimate with cohort fixed effects

**Key threats to identification:**
1. Spillover between treatment and control clusters (mitigation: market-cluster randomization with geographic buffers; monitoring via control group survey items)
2. Differential attrition (mitigation: intensive tracking, incentives, market association liaison network)
3. Measurement bias on sensitive financial outcomes (mitigation: list experiments, M-Pesa records, endorsement experiments)
4. Small number of clusters (mitigation: randomization inference, wild cluster bootstrap)

**Target journals:** American Economic Review, Quarterly Journal of Economics

**Collaborators:** Sarah Okonkwo (lead), James Mwangi, Lisa Park

**Timeline:**
- Apr 2026: Cohort 1 midline → preliminary experimental results
- Aug 2026: Cohort 1 endline
- Dec 2026: Cohort 2 endline
- Mar 2027: Cohort 3 endline
- Q2 2027: Full pooled analysis
- Q3 2027: Paper draft
- Q4 2027: Circulate working paper

---

#### Paper B2: "What Works? Unpacking the Components of a Financial Inclusion Program"

**Status:** Design phase. Depends on Paper B1 data + additional qualitative data.

**Research question:** Which components of the Jipange program (digital literacy, financial management training, M-Pesa savings commitment device) drive the effects on savings and income? Do effects vary by participant characteristics?

**Design:** Mediation analysis using the structured program components and intermediate outcomes. The 12-week program has three distinct phases:
- Weeks 1-4: Digital literacy (smartphone skills, M-Pesa features, online price comparison)
- Weeks 5-8: Financial management workshops (budgeting, profit calculation, savings goals, loan evaluation)
- Weeks 9-12: M-Pesa savings commitment device (automated weekly transfers, goal-based savings, peer accountability groups)

The midline survey (administered at week 12) includes module-specific measures:
- Digital literacy-related: smartphone proficiency test, M-Pesa feature usage, digital transaction frequency
- Financial management-related: budgeting knowledge, profit margin calculation, savings goal specificity
- Commitment device-related: savings consistency, peer group engagement, self-reported discipline

**Identification:** Causal mediation analysis (Imai et al. 2011). Cross-randomized design not feasible (components are sequential by design), so mediation estimates are suggestive, not definitive. Will use baseline-by-treatment interactions to identify who benefits most from which component (heterogeneous treatment effects).

**Complementary qualitative evidence:** James's qualitative interviews (n=40 treatment participants, purposive sampling across trainer groups and financial capability levels) will provide process evidence on which components participants found most valuable.

**Target journals:** Journal of Political Economy, Review of Economics and Statistics

**Collaborators:** Sarah Okonkwo (lead), James Mwangi

---

### Data and Measurement Notes

**Administrative data status:**
- Safaricom (M-Pesa records): Data sharing agreement in negotiation. Lisa in contact with Safaricom's research partnerships team. Would provide anonymized transaction volumes, savings balances, and transfer patterns. Expected timeline: 2-3 months.
- Kenya Revenue Authority: Formal business registration data for sample participants. Agreement signed. Data expected quarterly.
- Kenya National Social Security Fund: Employment records (formal sector only). Inquiry sent, no response yet.

**Survey instruments:**
- Baseline: 45 minutes. Fielded Dec 2025. Response rate 97%.
- Midline: ~45 minutes (revised). Includes list experiments (new), endorsement experiment (new), social network module (new). Drops detailed time-use module.
- Endline: ~50 minutes (planned). Full battery including all baseline items + experimental items from midline.

**Measurement concerns (tracked):**
1. Self-reported income and savings response rates (65-78% on sensitive items at baseline) → addressed via list experiments at midline
2. Item 14 refusal rate on screening tool → flagged for Cohort 3 revision
3. Item 22 possible social desirability bias → adding M-Pesa record cross-validation at midline
4. Control group attrition (1.6% at 4-week check — early but worth monitoring)

---

### Ethical Considerations

**Adverse events protocol:** Any participant reporting financial exploitation or coercion is referred to the Kenya Women's Enterprise Fund support line. Trainers trained in recognizing financial abuse indicators. Monthly adverse events review by James and the University of Nairobi ethics committee liaison.

**Market association consent:** In addition to individual informed consent, market-cluster consent obtained through association leader meetings in all 18 clusters. Process documented with signed agreements.

**Data security:** All personally identifiable information stored on encrypted IPA servers. Analysis datasets de-identified. SurveyCTO submissions encrypted in transit and at rest. Field tablets have remote wipe capability.

**Waitlist control ethics:** Control clusters receive the program in the subsequent cohort phase (4-month delay). No cluster permanently excluded. Staggered rollout justified by operational capacity constraints (cannot serve all 18 clusters simultaneously) and reviewed/approved by both IRBs.
