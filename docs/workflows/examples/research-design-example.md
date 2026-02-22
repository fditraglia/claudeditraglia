# Kingston Youth Futures — Research Design & Progress

*This is a synthetic example showing what a living research design document looks like after several weeks of `/weekly-review` updates. The project, team, and data are fictional. The structure and level of detail are realistic.*

---

## Project State

| Field | Value |
|-------|-------|
| Last updated | 2026-02-14 |
| Updated by | Claude Code /weekly-review |
| Primary owner | Chris Blattman |
| Co-PI | Karen Thompson (UWI Mona) |
| Research Manager | Marcus Chen (IPA Jamaica) |
| Review cadence | Weekly (Wednesdays) |

### Change Log (Recent)

| Date | Change | Source |
|------|--------|--------|
| 2026-02-14 | Added list experiment design for midline; updated power calcs with actual ICC | Weekly review |
| 2026-02-07 | Updated Cohort 2 screening progress; flagged facilitator fidelity issue | Weekly review |
| 2026-01-31 | Added Cohort 1 baseline balance table; confirmed J-PAL supplemental | Weekly review |
| 2026-01-17 | Initial document creation from project setup + historical materials | /setup-project-management |

---

## Section 0: Strategic Orientation

### North Star
Estimate the causal impact of an adapted CBT + life skills + mentorship intervention ("Pathways") on youth violence, criminal involvement, and economic outcomes among high-risk adolescents in Kingston, Jamaica — and identify which components drive the effects.

### Why This Matters
Jamaica has one of the highest youth homicide rates in the Western Hemisphere. Kingston accounts for over 40% of national violent crime. Existing interventions focus on enforcement and community policing; evidence on behavioral interventions for at-risk youth in Caribbean contexts is nearly nonexistent. This study fills a critical gap: can an adapted version of interventions shown to work in Liberia (Blattman et al. 2017) and Chicago (Heller et al. 2017) reduce violence in a Caribbean urban context? The staggered rollout and component analysis aim to answer not just "does it work" but "what works and for whom."

### Critical Success Factors
1. Community trust and cooperation (especially across politically divided neighborhoods)
2. Treatment fidelity — facilitator quality determines whether the intervention is delivered as designed
3. Measurement of sensitive outcomes (violence, gang involvement) with minimal bias
4. Cohort enrollment and retention across all three waves
5. Timely funding disbursements to prevent operational gaps

---

## Section 1: Executive Snapshot

### Study Design at a Glance

| Element | Detail |
|---------|--------|
| Design | Cluster RCT, community-level randomization, staggered rollout |
| Location | Kingston, Jamaica (Trench Town, Tivoli Gardens, August Town) |
| Sample | ~1,200 adolescents (14-19), 18 communities, 3 cohorts of ~400 |
| Intervention | "Pathways" — 16-week program: 8 weeks group CBT, 4 weeks life skills workshops, 4 weeks one-on-one mentorship |
| Control | Waitlist (receives intervention in subsequent cohort phase) |
| Randomization | Community-level, stratified by neighborhood and baseline violence rates |
| Primary outcomes | Violence involvement index, criminal behavior index, economic self-sufficiency index |
| Secondary outcomes | Mental health (K10), prosocial attitudes, social network composition, gang affiliation |
| Measurement | Baseline, midline (4 months post-randomization), endline (12 months), long-run follow-up (24 months, funding dependent) |
| Pre-registration | AEA Registry #AEARCTR-0012847 (registered Jan 2026, update pending for midline changes) |

### Current Status by Phase

| Phase | Status | Key Metric |
|-------|--------|------------|
| Cohort 1 enrollment | Complete | 380/400 (95%) |
| Cohort 1 baseline | Complete | 97% response rate |
| Cohort 1 intervention | In progress (week 9/16) | 76% avg attendance |
| Cohort 1 midline | Planned Apr 2026 | Instrument in revision |
| Cohort 2 screening | In progress | 290/~400 screened (73%) |
| Cohort 2 randomization | Planned Mar 15 | Protocol drafted |
| Cohort 3 | Planning | Community mapping underway |

### Team

| Role | Name | Affiliation | Focus |
|------|------|-------------|-------|
| PI | Chris Blattman | UChicago Harris | Design, analysis, donor relations |
| Co-PI | Karen Thompson | UWI Mona | Intervention design, qualitative component, facilitator training |
| Research Manager | Marcus Chen | IPA Jamaica | Field operations, data management, screening |
| Field Researcher | Andre Campbell | IPA Jamaica | Community relations, logistics, Cohort 3 mapping |
| RA (Survey) | Keisha Williams | UChicago | Survey design, SurveyCTO programming, midline pilot |
| RA (Data) | Devon Brown | UChicago | Attendance tracking, data cleaning, facilitator analysis |
| RA (Qualitative) | Tamara Mitchell | UWI Mona | Qualitative interviews, transcript processing |

---

## Section 2: Paper Plan

### Track A: Predictive / Descriptive Papers

#### Paper A1: "Predicting Youth Violence Risk in Urban Jamaica: Validation of an Adapted Screening Tool"

**Status:** Data collection complete (Cohort 1 baseline + screening data). Analysis planned for Q3 2026.

**Research question:** How well does an adapted SAVRY/YLS-CMI screening tool predict violent behavior among Kingston adolescents, and which risk factors are most predictive in this context?

**Design:** Predictive validity study using Cohort 1 screening scores (pre-randomization) to predict baseline self-reported violence and administrative records. Compare performance to the original instruments validated in North American samples.

**Key data:**
- Screening scores for 380 Cohort 1 participants (adapted SAVRY/YLS-CMI, 28 items)
- Baseline self-reported violence (5-item index, with caveats about response rates)
- Jamaica Constabulary Force administrative records (pending data sharing agreement — Marcus following up)
- Community-level violence data from the Citizen Security and Justice Programme

**Identification:** Predictive validity (AUC, sensitivity, specificity). Machine learning comparison (LASSO, random forest) to assess whether the full instrument outperforms a reduced-form version.

**Target journals:** Journal of Quantitative Criminology, Journal of Youth and Adolescence

**Collaborators:** Karen Thompson (lead author), Chris Blattman, Marcus Chen

---

#### Paper A2: "Who Joins Gangs in Kingston? Risk Factors, Social Networks, and the Role of Community Context"

**Status:** Descriptive analysis pending. Awaiting Cohort 1 midline data for social network module.

**Research question:** What individual, household, and community-level factors predict gang affiliation among adolescents in Kingston? How do social network structures differ between gang-affiliated and non-affiliated youth?

**Design:** Cross-sectional descriptive analysis using baseline + midline data. Social network analysis using the name generator module (midline instrument). Community-level analysis using neighborhood-level covariates.

**Key data:**
- Baseline survey (demographics, household, risk factors) — n=380
- Midline social network module (collecting Apr 2026)
- Community mapping data (Andre's Cohort 3 prep work will generate neighborhood profiles)
- Endorsement experiment item on gang attitudes (midline)

**Identification:** Descriptive — conditional correlations, network statistics, neighborhood variation. Not causal.

**Target journals:** Criminology, British Journal of Criminology

**Collaborators:** Karen Thompson, Andre Campbell, Chris Blattman

---

### Track B: Experimental Papers

#### Paper B1 (Main Paper): "Reducing Youth Violence in Kingston: Experimental Evidence on CBT, Life Skills, and Mentorship"

**Status:** Pre-registered. Cohort 1 intervention in progress. First results expected Q4 2026 (midline) with full results Q2 2027 (all cohorts, endline).

**Research question:** Does the Pathways intervention reduce violence, criminal involvement, and improve economic outcomes among high-risk adolescents in Kingston?

**Design:** Cluster RCT with staggered rollout across 3 cohorts. Community-level randomization (18 communities: 9 treatment, 9 control per cohort pair). Intent-to-treat analysis with complier average causal effect estimates.

**Primary outcome indices:**
1. Violence involvement index (physical fights, weapon carrying, gang-related activity) — measured via combined direct report + list experiment at midline/endline
2. Criminal behavior index (theft, vandalism, drug selling, arrests) — self-report + administrative records
3. Economic self-sufficiency index (employment, income, school enrollment, vocational training)

**Secondary outcomes:**
- Mental health (K10 psychological distress scale)
- Prosocial attitudes and behaviors (adapted from Blattman et al. 2017)
- Social network composition (share of prosocial vs. antisocial ties)
- Gang affiliation (endorsement experiment)

**Power calculations (updated Feb 14, 2026):**
Using actual Cohort 1 ICC = 0.048 (baseline violence index):
- 18 communities, ~67 individuals per community
- MDE = 0.17 SD on violence index (80% power, 5% significance)
- MDE = 0.15 SD with baseline covariate adjustment (R-squared ~0.25)
- If Cohort 2+3 each reach 360 (minimum threshold), total N = 1,100 → MDE = 0.16 SD
- Power adequate for main effects. Heterogeneity analysis (by risk level, gender, neighborhood) will be underpowered — pre-registered as exploratory.

**Estimation strategy:**

Primary specification:
  Y_ic = alpha + beta * Treatment_c + gamma * X_i + delta * Stratification_s + epsilon_ic

Where:
- Y_ic is outcome for individual i in community c
- Treatment_c is community-level treatment assignment
- X_i is a vector of baseline covariates (pre-registered: age, gender, risk score, household income, school enrollment)
- Stratification_s are randomization strata fixed effects (neighborhood x baseline violence rate)
- Standard errors clustered at community level

Robustness:
- Lee bounds for attrition
- Randomization inference (exact p-values given 18 clusters)
- LASSO-selected controls (Belloni et al. 2014)
- Cohort-specific estimates + pooled estimate with cohort fixed effects

**Key threats to identification:**
1. Spillover between treatment and control communities (mitigation: community-level randomization with geographic buffers; monitoring via control group survey items)
2. Differential attrition (mitigation: intensive tracking, incentives, community liaison network)
3. Measurement bias on sensitive outcomes (mitigation: list experiments, endorsement experiments, administrative data)
4. Small number of clusters (mitigation: randomization inference, wild cluster bootstrap)

**Target journals:** American Economic Review, Quarterly Journal of Economics

**Collaborators:** Chris Blattman (lead), Karen Thompson, Marcus Chen

**Timeline:**
- Apr 2026: Cohort 1 midline → preliminary experimental results
- Aug 2026: Cohort 1 endline
- Dec 2026: Cohort 2 endline
- Mar 2027: Cohort 3 endline
- Q2 2027: Full pooled analysis
- Q3 2027: Paper draft
- Q4 2027: Circulate working paper

---

#### Paper B2: "What Works? Unpacking the Components of a Youth Violence Intervention"

**Status:** Design phase. Depends on Paper B1 data + additional qualitative data.

**Research question:** Which components of the Pathways intervention (CBT, life skills, mentorship) drive the effects on violence and economic outcomes? Do effects vary by participant characteristics?

**Design:** Mediation analysis using the structured intervention components and intermediate outcomes. The 16-week intervention has three distinct phases:
- Weeks 1-8: Group CBT (cognitive behavioral therapy adapted for youth)
- Weeks 9-12: Life skills workshops (financial literacy, conflict resolution, job readiness)
- Weeks 13-16: One-on-one mentorship with trained community adults

The midline survey (administered at week 16) includes module-specific measures:
- CBT-related: cognitive distortion scale, emotional regulation, impulsivity
- Life skills-related: financial knowledge, conflict resolution strategies, job search behavior
- Mentorship-related: adult mentor relationship quality, help-seeking behavior

**Identification:** Causal mediation analysis (Imai et al. 2011). Cross-randomized design not feasible (components are sequential by design), so mediation estimates are suggestive, not definitive. Will use baseline-by-treatment interactions to identify who benefits most from which component (heterogeneous treatment effects).

**Complementary qualitative evidence:** Karen's qualitative interviews (n=40 treatment participants, purposive sampling across facilitator groups and risk levels) will provide process evidence on which components participants found most valuable.

**Target journals:** Journal of Political Economy, Review of Economics and Statistics

**Collaborators:** Chris Blattman (lead), Karen Thompson

---

### Data and Measurement Notes

**Administrative data status:**
- Jamaica Constabulary Force: Data sharing agreement in negotiation. Marcus in contact with JCF Statistics Unit. Would provide arrest records, charges, and geographic incident data. Expected timeline: 2-3 months.
- Ministry of Education: School enrollment data for sample participants. Agreement signed. Data expected quarterly.
- Ministry of Labour: Employment records (formal sector only). Inquiry sent, no response yet.

**Survey instruments:**
- Baseline: 45 minutes. Fielded Dec 2025. Response rate 97%.
- Midline: ~45 minutes (revised). Includes list experiments (new), endorsement experiment (new), social network module (new). Drops detailed time-use module.
- Endline: ~50 minutes (planned). Full battery including all baseline items + experimental items from midline.

**Measurement concerns (tracked):**
1. Self-reported violence response rates (65-78% on sensitive items at baseline) → addressed via list experiments at midline
2. Item 14 refusal rate on screening tool → flagged for Cohort 3 revision
3. Item 22 possible social desirability bias → adding bogus pipeline validity check at midline
4. Control group attrition (1.6% at 4-week check — early but worth monitoring)

---

### Ethical Considerations

**Adverse events protocol:** Any participant reporting immediate safety concerns is referred to the Violence Prevention Alliance crisis line. Facilitators trained in mandatory reporting for minors. Monthly adverse events review by Karen and the UWI Mona ethics committee liaison.

**Community consent:** In addition to individual informed consent (and parental consent for minors under 16), community-level consent obtained through community leader meetings in all 18 neighborhoods. Process documented with signed agreements.

**Data security:** All personally identifiable information stored on encrypted IPA servers. Analysis datasets de-identified. SurveyCTO submissions encrypted in transit and at rest. Field tablets have remote wipe capability.

**Waitlist control ethics:** Control communities receive the intervention in the subsequent cohort phase (6-month delay). No community permanently excluded. Staggered rollout justified by operational capacity constraints (cannot serve all 18 communities simultaneously) and reviewed/approved by both IRBs.
