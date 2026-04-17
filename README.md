
CHRONOS BY MYND & BODI INSTITUTE


Future State
Product Vision
& Brand System

A comprehensive reference document covering the Chronos brand identity, UI/UX design system, screen architecture, feature roadmap, risk intelligence layer, health education framework, and allostatic load model — from current Phase 1.5 through the full market-ready vision.



DOCUMENT	Chronos Future State — Product Vision & Brand System
VERSION	1.0 — April 2026
CLASSIFICATION	Internal / Confidential
PREPARED BY	Claude (Technical Co-Founder) & Founder
STATUS	Living document — updated each phase
PHASE	1.5 Active / Vision through Phase 4+



This document is the single source of truth for Chronos brand and product vision. It should be referenced in every design, engineering, and partnership conversation. Nothing in this document supersedes the Phase 1 PRD for current build decisions.
 
01 — Brand Identity

1.1 Naming Architecture
The product operates under a two-tier naming system. The parent institution is Mynd & Bodi Institute (MBI). The consumer-facing product is Chronos. This structure provides credibility through the institute while giving the product a distinct, memorable identity that can stand alone.

Parent Entity	Mynd & Bodi Institute (MBI)
Product Name	Chronos
Full Mark	Chronos by Mynd & Bodi Institute
Short Form	Chronos by MBI
Domain	chronos.mbi / chronosbymbi.com (TBD)

1.2 Naming Philosophy
'Mynd & Bodi' is intentionally unconventional — a deliberate brand asset signaling that MBI challenges conventional healthcare thinking. The unconventional spelling is not an error; it is a statement that mind and body are distinct yet inseparable.

'Chronos' is the Greek personification of time — chosen deliberately. The body operates on cycles: circadian rhythms, HRV oscillation, sleep architecture, recovery waves. Time is MBI's best biomarker. The name signals precision, depth, and a long-range view rather than a moment-in-time snapshot.

1.3 Tagline & Core Beliefs

Primary Tagline	Know your body. Own your health. Live better.
Core Product Belief	Chronos explains your day. It does not score your body.
Brand Posture	Rebellion with credibility. Healthcare reimagined around the individual.

1.4 Brand Voice
Chronos speaks with calm authority. It never shouts. It never induces anxiety. It knows things and shares them plainly — the way a trusted physician would speak to a friend, not a patient.

Chronos Sounds Like	Chronos Never Says
Your body is working harder than normal.	✗  Your autonomic dysfunction risk is elevated.
One good sleep changes this trajectory.	✗  You may be experiencing systemic inflammation.
You're trending down — let's stabilize.	✗  Consult a physician immediately.
Your baseline, not anyone else's.	✗  You scored below average today.
Keep things measured today.	✗  Your biometric data suggests clinical concern.

1.5 Color System
The Chronos color system is built on deep navy-blacks with a single warm gold accent. The palette is deliberately anti-health-app — no teal, no green gradients, no white-on-purple. The gold signals precision and value. The parchment white is warm, never clinical.

Name	Hex	Usage
Void Black	#04040C	Primary background. The foundation of the entire visual system.
Surface	#0E0E1E	Card and panel backgrounds. Subtle lift from void.
Panel	#141428	Inner cards, elevated surfaces.
Chronos Gold	#B8946A	Primary accent. Labels, icons, score band text.
Gold Light	#D4AB82	Score numbers, key data values, nudge text.
Parchment	#F6F3EE	Primary body text. Warm white — never pure white.
Muted	#8A8070	Secondary text, placeholders, timestamps.
Redline	#B85A5A	Critical state only. Never decorative.
Thriving	#7AAA8A	Positive state. Used only when score is genuinely high.
Amber	#C4965A	Warning state. Drift mode, caution signals.

1.6 Typography

Display / Hero	Cormorant Garamond — Light 300, Light Italic
Usage	Score numbers, screen titles, brand wordmark, expressive headings
UI / Body	Jost — Light 300, Regular 400
Usage	All body copy, labels, navigation, buttons, data values
Label Style	Jost 8–9px, letter-spacing 0.3–0.4em, ALL CAPS
Rationale	Cormorant brings old-world precision and warmth. Jost brings modern clarity without coldness. The pairing creates the 'simple complexity' aesthetic.

1.7 Brand Manifesto Principles

•	Data doesn't save lives — action does. Chronos exists to close the gap between knowing and doing.
•	Health doesn't start in the clinic. It starts in every daily decision, years before a diagnosis.
•	AI is your assistant, not your doctor. Chronos interprets. You decide. We never forget that distinction.
•	Prevention is the new standard. Reactive healthcare is a design flaw. We're building the correction.
•	We earn trust by breaking rules that don't serve you. Everything Chronos does, it can explain.
 
 
02 — Product Architecture

2.1 What Chronos Is
Chronos is a daily physiological intelligence system. It reads Apple Watch data overnight, calculates a resilience score anchored to the user's personal baseline, identifies the two signals that deviated most, generates a plain-language explanation of what happened and why, and delivers one single action to take. That loop — sense, score, explain, nudge — repeats every morning.

The design principle behind every decision: Chronos explains your day. It does not score your body. Every number is comparative to the user's own history, never to population norms. Every explanation names its sources. Every output is traceable.

2.2 The Six-Layer Architecture

Layer 1 — iOS Client	SwiftUI presentation, navigation, local session state, HealthKit permissions and reads, sync triggers. Zero scoring logic.
Layer 2 — Ingestion	Receives raw HealthKit payloads. Validates, normalizes units and timestamps, deduplicates, marks data quality, stores versioned daily aggregates.
Layer 3 — Domain Layer	TypeScript package. Scoring engine, baseline computation, deviation detection, dynamic alpha, eligibility rules, top-2 driver selection. Fully deterministic. Fully versioned.
Layer 4 — Narrative Layer	Claude API (claude-sonnet-4-6). Receives structured domain outputs. Generates plain-language explanation and single nudge. Never influences scores.
Layer 5 — Application Layer	Auth, client-facing endpoints, orchestration, audit logging, admin tools. Supabase + Edge Functions.
Layer 6 — Data Layer	Supabase Postgres. Canonical system of record for scores, baselines, raw inputs, flags, feedback, audit history, version lineage.

2.3 The Scoring System

Three concepts are strictly separated:
•	Baseline Range — what is normal for this specific user, calculated as 7-day rolling average (90-day bootstrap on onboarding).
•	Guardrail Range — evidence-backed absolute safety bounds regardless of baseline.
•	Behavioral Goal — adjustable targets for steps and activity. Not physiological signals.

Formula	Chronos Score = Health Score − (Risk Score × α)
Alpha — Mild	α = 0.6 (single signal flagged)
Alpha — Moderate	α = 0.8 (two signals flagged)
Alpha — Severe	α = 1.0 (three or more signals stacked)
Delta Override	If score drops >15 points from 3-day average, tone of explanation overridden regardless of band
HRV Weight	2× — autonomic nervous system primary signal
Resting HR Weight	2× — stress load and recovery
Respiratory Rate Weight	2× — strongest early illness indicator
Sleep Duration Weight	1.5× — cellular repair window
Sleep Efficiency Weight	1.5×
Steps Weight	1× — behavioral, not physiological
Active Minutes Weight	1×

2.4 Score Bands

Range	Band	Meaning
80–100	Thriving	Autonomic system flexible. Recovery high. Body primed for effort or challenge.
60–79	Recovering	System under moderate load. Functional but asking for support. Common baseline.
40–59	Drifting	Risk accumulating. Adherence or recovery declining. System needs intervention.
0–39	Redline	Multiple systems flagged. Rest is the only intervention. Full tone shift.

2.5 Five Domain Scores

D1 — Autonomic Recovery	HRV + Resting HR. Nervous system balance. Available from Day 1.
D2 — Sleep Recovery	Sleep Duration + Sleep Efficiency. Cellular repair. Available from Day 1.
D3 — Activity Load	Steps + Active Minutes + Distance. Metabolic engagement. Available from Day 1.
D4 — Inferred Stress	HRV trend + RHR trend + sleep pattern disruption over 7-day window. Active after 7 days.
D5 — Allostatic Trend	30-day rolling composite. Where the user is heading, not just where they are today. Active after 30 days.

2.6 Adaptive Fail States

Redline	Triggered if: HRV drops >30% from baseline, OR resting HR rises >10 bpm, OR respiratory rate exceeds 20 rpm, OR sleep under 5.5 hrs, OR 2+ mild deviations stack simultaneously. Full UI tone shift to red.
Drift Mode	Triggered when risk is rising and adherence is below 30% over 5 days. System simplifies output.
Ghost Mode (Healthy)	3+ days no engagement with score stable or improving. System goes quiet. Does not intervene.
Ghost Mode (At-Risk)	3+ days no engagement with score declining. Soft intervention surface. NEVER silence during deterioration. This is a non-negotiable architectural constraint.
 
 
03 — Screen Architecture

Chronos organizes its product surface into four primary navigation tabs, each with a clear job, plus supporting screens for onboarding, states, and profile. The navigation structure is designed to be additive — each tab unlocks depth as the user's baseline matures.

Today (◈)	The Morning Brief. Daily score, two drivers, plain-language explanation, one nudge. Primary daily surface.
Trend (⌇)	Weekly Narrative. 7-day score ribbon, editorial story of the week's arc, what's improving vs. what needs attention.
Domains (⬡)	Five Domain Intelligence. D1–D3 active from Day 1. D4 active after 7 days. D5 active after 30 days.
Horizon (◎)	Risk Horizon + Health Intelligence + Allostatic Portrait. The long-range prevention intelligence layer.

3.1 Navigation & Progression
The Horizon tab is the most strategically important surface in the product. It is where the Chronic Disease Ontology Engine becomes visible to the user — upstream pathway activation, contextual health education, and the 90-day allostatic portrait. This tab progressively deepens as the user's baseline matures.
 
3.2 Screen Wireframes
The following wireframes represent the target UI architecture. These are structural references — actual visual design follows the brand system in Section 01.

SCREEN 01 — TODAY / MORNING BRIEF

Today — Morning Brief
PRIMARY DAILY SURFACE
9:41  ●●●  WiFi  Battery
THURSDAY · APRIL 17
7:08 AM — Score delivery time
SCORE
74
Recovering  ·  ↓ 6 from yesterday  ·  Day 24
⬡  Animated arc ring around score. Sparkline beneath showing 7-day history.
DRIVERS
Driver 1: HRV  ↓18%  |  Driver 2: Sleep  −1.2h
The two metrics that deviated most from personal baseline today
⬡  Two inset chips side by side. Recessed shadow treatment.
WHAT HAPPENED
Your recovery dipped overnight — driven by lower HRV and shorter sleep than your baseline. Your body is working harder than usual. Keep things measured today.
⬡  Claude-generated. 2–4 sentences. References top 2 drivers by name. No clinical language.
TODAY'S FOCUS
Aim for bed 45 minutes earlier. One good sleep changes this trajectory.
Single nudge — always one action, never a list
⬡  Gold-tinted nudge card with left pip. Most visually distinct element on screen.
[ Today ]  [ Trend ]  [ Domains ]  [ Horizon ]

SCREEN 02 — TREND / WEEKLY NARRATIVE

Trend — Weekly Narrative
TAB 2 — UNLOCKED FROM DAY 1
9:41  ●●●  WiFi  Battery
Your week in signal.
Seven days of data, one coherent story.
7-DAY SCORE RIBBON
M  T  W  T  F  S  T
Bar chart: Mon 62, Tue 78, Wed 84, Thu 70, Fri 38 (low), Sat 75, Today 74
⬡  Score bars rendered as minimal height-proportional bars. Today bar highlighted in lighter gold. Low day in muted red.
WEEK OF APRIL 11 — NARRATIVE
Strong through Wednesday, dip Friday still processing. Accumulated fatigue pattern — not illness.
HRV 14% below 30-day average for 4 consecutive days — a consistent recovery signal, not an alarm.
⬡  Claude-generated weekly narrative. Editorial tone. Pattern detection, not just summary.
WHAT'S WORKING
Activity Load consistently above baseline all week — 86 avg. Movement is not the problem. Recovery is.
⬡  Green-tinted card. Appears when a domain is genuinely performing well.
[ Today ]  [ Trend ]  [ Domains ]  [ Horizon ]

SCREEN 03 — DOMAINS / FIVE SYSTEM INTELLIGENCE

Domains — Five System Intelligence
TAB 3 — PROGRESSIVELY ACTIVATES
9:41  ●●●  WiFi  Battery
Five systems. One picture.
How each system performed today relative to your baseline.
D1 — AUTONOMIC RECOVERY
61  ↓14
HRV + Resting HR  —  Stressed today. Primary driver of low score.
⬡  Score bar below metric names. Low scores shown in muted red gradient.
D2 — SLEEP RECOVERY
72  ↓8
Duration + Quality  —  Below baseline but not critical.
D3 — ACTIVITY LOAD
86  ↑3
Steps + Active Minutes  —  Above baseline. Protective.
D4 — INFERRED STRESS
58  — Loading
7-day HRV + RHR + Sleep trend  —  Active after 7 days of history
⬡  Unlocks after 7 days. Shows inferred stress pattern from trend data.
D5 — Allostatic Trend  🔒
30-day rolling composite — Active in 6 days
⬡  Grayed out until 30 days. Unlocking is a product moment — should be acknowledged.
[ Today ]  [ Trend ]  [ Domains ]  [ Horizon ]

SCREEN 04 — HORIZON / RISK HORIZON (NEW)

Horizon — Risk Intelligence
TAB 4 — NEW SURFACE · PHASE 2
9:41  ●●●  WiFi  Battery
What's building upstream.
Patterns today that become conditions tomorrow — surfaced early, while still reversible.
AUTONOMIC PATHWAY — ACTIVE SIGNALS
NODE GRAPH: Poor Sleep + Stress → Low HRV (active) → Autonomic Dysfunction (watch)
Three-tier visualization: Behavior (root causes) → Biology (response nodes) → Risk (downstream)
⬡  The Chronic Disease Ontology Engine made visible. Shows active propagation paths. NOT clinical language — pathway visibility only.
WATCH
Sympathetic Dominance — Building
4 consecutive days of suppressed HRV activating an autonomic stress pattern. Still early and fully reversible.
⬡  Amber warning card. Always framed as early and reversible. Never alarmist.
PROTECTIVE
Activity Load — Countering Risk
Consistent movement above baseline actively countering metabolic risk accumulation.
⬡  Green card for protective nodes. Balances the risk signal — shows what the user is doing right.
[ Today ]  [ Trend ]  [ Domains ]  [ Horizon ]

SCREEN 05 — HEALTH INTELLIGENCE / CONTEXTUAL EDUCATION (NEW)

Health Intelligence — Contextual Education
NEW SURFACE · PHASE 2
9:41  ●●●  WiFi  Battery
CONTEXTUAL TRIGGER — APPEARS INLINE
HRV has been your top driver 4 days in a row. Here's what that means. →
Triggered automatically when a driver repeats. Arrives in context, not in a library.
CHRONOS · HEALTH INTELLIGENCE
What HRV is actually measuring
Heart Rate Variability measures the variation in time between your heartbeats. A higher number means your autonomic nervous system is flexible and responsive...
⬡  Plain language. No clinical framing. Ends with a practical takeaway relevant to the user's current state.
YOUR STATS
Your avg: 47ms  |  Today: 38ms  |  Delta: ↓19%
⬡  Inline stats contextualizing the education. Makes it personal, not generic.
KEY TAKEAWAY
Sleep, alcohol, late meals, and psychological stress suppress HRV fastest. Recovery, breathwork, and consistent sleep restore it.
⬡  Gold-tinted card. The one thing to remember from this article.
[ Today ]  [ Trend ]  [ Domains ]  [ Horizon ]

SCREEN 06 — ALLOSTATIC PORTRAIT / D5 EVOLVED (NEW)

Allostatic Portrait — 90-Day Load
NEW SURFACE · UNLOCKS AT DAY 30
9:41  ●●●  WiFi  Battery
Your body's cumulative load.
Where you are now versus where you were 90 days ago.
ALLOSTATIC LOAD · 90-DAY PORTRAIT
CHART: Descending line from Day 1 to Today. Lower = better. Load decreasing over time.
90 days ago: 72  →  Today: 48  (↓33% improvement)
⬡  The key insight: lower allostatic load means less cumulative stress burden. Descending line = progress. This is what prevention looks like visually.
SYSTEM HEALTH — TODAY
Autonomic 68  |  Metabolic 82  |  Sleep 74  |  Inflammatory 88
2×2 grid showing four system scores with mini progress bars
⬡  Progressive unlocking: metabolic and inflammatory scores require lab data (Phase 3). Wearable-only shows autonomic and sleep.
TRAJECTORY
Your body is carrying significantly less cumulative stress than when you started. This is what prevention looks like.
⬡  Green trajectory card. The emotional payoff of 30+ days of engagement. This is the retention surface.
[ Today ]  [ Trend ]  [ Domains ]  [ Horizon ]

SCREEN 07 — ADAPTIVE STATES

State	UI Behavior
Thriving	Deep green tints on score card and nudge card. Score number in green. Nudge reframed as opportunity: 'Your body is primed — use this window.' Ascending sparkline.
Recovering	Default gold treatment. Score number in gold. Standard morning brief structure. Most common state.
Drifting	Amber accents. Nudge simplified. System enters Drift Mode if adherence below 30% for 5 days.
Redline	Full UI shift to deep red. Entire screen reframes around rest as the only intervention. Descending sparkline in red. Tab bar still visible — user can still navigate.
Ghost — At-Risk	Full-screen soft intervention surface. Clock icon pulsing. Score surfaced without requiring navigation. One CTA: See what happened. NEVER goes silent when score is declining.
 
 
04 — Risk Intelligence & Health Education

4.1 The Chronic Disease Ontology Engine
The most technically substantial and defensible asset in the entire MBI vault. A four-tier causal graph model mapping the progression from modifiable lifestyle behaviors through to chronic disease endpoints. This is the core IP that separates Chronos from every other wearable or health app on the market.

Tier 1 — Root Causes	10 behavioral/environmental input nodes: Poor Diet, Physical Inactivity, Chronic Psychological Stress, Poor Sleep Quality, Gut Dysbiosis, Social Isolation, Environmental Toxins, Substance Use, Circadian Disruption, Ultra-processed Food Intake
Tier 2 — Biological Response	14 measurable intermediary nodes including Insulin Resistance, Systemic Inflammation, Autonomic Dysfunction, Low HRV, Sympathetic Dominance, Elevated Resting Heart Rate, Oxidative Stress, Hormonal Imbalance
Tier 3 — Intermediate Dysfunction	14 pre-disease states including Glucose Intolerance, Visceral Obesity, Sleep Fragmentation, Hypertension, Chronic Fatigue, Depressive Symptoms
Tier 4 — Chronic Endpoints	11 disease nodes including Type 2 Diabetes, Cardiovascular Disease, Alzheimer's, Autoimmune Disease, Depression (MDD), Obstructive Sleep Apnea, Cancer
Protective Nodes	11 nodes including Daily Exercise, Quality Sleep, High HRV, Breathwork, Circadian Rhythm Alignment, Fasting State, Social Connection
Propagation Coefficients	Each node has defined beta values (e.g., Systemic Inflammation → CVD: β=0.9 exponential), decay half-lives, and activation thresholds

4.2 Risk Horizon Design Principles
The Risk Horizon surface brings the ontology engine into the user's daily experience. Three design principles govern everything shown on this surface:

•	Early and reversible framing only. Every risk signal is presented as something that can be changed. No fatalistic language. No predictions. Pathway visibility — not prognosis.
•	Protective nodes always shown alongside risk nodes. For every watch signal, show what the user is doing right. The surface must never feel like an accumulation of problems.
•	Wellness framing always. SaMD never. Chronos makes no clinical claims, diagnoses, or treatment recommendations. This is a non-negotiable constraint through Phase 3.

4.3 Wearable-to-Node Mapping
The current wearable data maps directly to ontology nodes as follows:

Wearable Signal	Activated Node	Threshold
HRV < 40ms	Sympathetic Dominance	Baseline flag: <25ms guardrail
HRV < baseline −30%	Autonomic Dysfunction (risk)	Hard deviation threshold
Resting HR > 70bpm	Elevated Resting Heart Rate	Stress/overtraining node
Sleep < 6.5hrs	Sleep Fragmentation	Protective node not firing
Sleep efficiency < 85%	Sleep Fragmentation	Quality component
Steps < 5,000/day	Physical Inactivity	Root cause node activates
Steps > 8,000/day	Daily Exercise (protective)	Protective node fires
Resp rate > 20rpm	Illness signal / stress	Hard guardrail flag

4.4 Health Intelligence — Education Layer
Contextual health education is embedded inline — it arrives when relevant, not in a library the user has to navigate. The trigger logic is as follows:

•	Repeat driver trigger: When the same metric is the top driver for 3+ consecutive days, Chronos surfaces a contextual education card explaining what that metric measures, why it matters, and what influences it.
•	Domain activation trigger: When D4 or D5 activates for the first time, Chronos explains what the domain measures and what the first reading means.
•	Risk signal trigger: When the Risk Horizon surfaces a watch or caution signal, an education link is embedded in the signal card.
•	Milestone trigger: At Day 7, Day 30, and Day 90, Chronos surfaces a reflection card on what the user's baseline reveals about their patterns.

The Intelligence Library organizes all content by relevance to the user's current state — not by category. Articles unlock progressively: wearable-based content available from Day 1, lab-based content unlocks when lab integration is added (Phase 3), D5 allostatic content unlocks at Day 30.

4.5 The Allostatic Portrait — Design Intent
The Allostatic Portrait is the emotional payoff of long-term engagement. It answers the question every user eventually asks: is any of this actually working? A descending allostatic load line over 90 days is the most powerful retention surface in the product because it makes progress visible in a way that a daily score cannot.

The portrait visualization renders the user's cumulative stress burden as a single continuous line over time. Lower is better. The direction of the line matters more than any individual data point. This reframes the user's relationship with the product from daily check-in to long-range investment.
 
 
05 — Feature Roadmap

Every feature in this roadmap has a phase assignment. Nothing gets built before its phase gate is met. The exit criteria for each phase are defined in the Phase 1 PRD. This document extends that roadmap through Phase 4+.

5.1 Current State — Phase 1.5

Feature	Phase	Status
Auth (single user)	Phase 1	In Progress
Onboarding flow	Phase 1	In Progress
90-day baseline bootstrap	Phase 1.5	Complete
HealthKit daily sync	Phase 1	Live
Chronos score calculation	Phase 1	Needs Testing
Two driver identification	Phase 1	Needs Testing
Claude explanation generation	Phase 1	Live
Nudge generation	Phase 1	Needs Prompt Fix
Domain breakdown (D1–D3)	Phase 1	In Progress
D4 Inferred Stress	Phase 1	In Progress
D5 Allostatic Trend	Phase 1	Pending Day 30
7-day sparkline	Phase 1	In Progress
Feedback mechanism	Phase 1	Live
Fail states (Redline, Drift, Ghost)	Phase 1	In Progress
Admin view	Phase 1	In Progress

5.2 Phase 2 — Prove the Value (2–5 Users)

Feature	Phase	Status
Multi-user auth + access control	Phase 2	Phase 2
Push notifications — morning brief delivery	Phase 2	Phase 2
Evening reflection prompt	Phase 2	Phase 2
Weekly narrative screen (Trend tab)	Phase 2	Phase 2
Risk Horizon screen (Horizon tab)	Phase 2	Phase 2
Contextual Health Intelligence cards	Phase 2	Phase 2
Intelligence Library	Phase 2	Phase 2
Single-tap context markers (workout, travel, etc.)	Phase 2	Phase 2
Thriving state UI variant	Phase 2	Phase 2
Ghost Mode — At-Risk intervention screen	Phase 2	Phase 2
Allostatic Portrait (D5 visualization)	Phase 2	Phase 2
Chronos brand treatment applied to all screens	Phase 2	Phase 2
TestFlight distribution	Phase 2	Phase 2

5.3 Phase 3 — Prove the Market (App Store)

Feature	Phase	Status
App Store submission	Phase 3	Phase 3
Subscription model (pricing TBD)	Phase 3	Phase 3
Lab integration — Function Health / Everlywell	Phase 3	Phase 3
Manual biomarker entry	Phase 3	Phase 3
Garmin / Oura / Whoop support	Phase 3	Phase 3
Metabolic + inflammatory system scores (D5 expanded)	Phase 3	Phase 3
Cohort mode — founder-controlled groups	Phase 3	Phase 3
Waitlist conversion flow	Phase 3	Phase 3
Android client	Phase 3+	Phase 3+

5.4 Phase 4+ — The Platform

Feature	Phase	Status
cDPC provider dashboard — Chronos companion	Phase 4	Phase 4+
Pre-visit AI triage for physicians	Phase 4	Phase 4+
Behavior-responsive insurance data layer	Phase 4	Phase 4+
Employer B2B cohort platform	Phase 4	Phase 4+
MBI University	Phase 5+	Phase 5+
Licensed health insurer pathway	Phase 5+	2029+

5.5 Non-Negotiable Architectural Constraints
These constraints apply to every phase and every feature. A feature that violates any of these is a failure regardless of how well it performs otherwise.

•	Within-User Primacy: Every comparison is the user versus their own baseline. Population norms are never used anywhere in the stack.
•	Explainability: Every score is traceable to its top 2 drivers and versioned inputs. No black box outputs. Ever.
•	Psychological Safety: The system never induces health anxiety, shame, or obsessive tracking. Wellness framing only.
•	Reality Anchoring: The system is designed for messy, incomplete real-world data. Missing metrics produce quality flags — they do not crash the experience.
•	Truth Before Velocity: A feature that ships fast but undermines trust is a failure. Determinism and reproducibility are non-negotiable.
•	One Nudge: Always singular. Never a list. One action per day.
•	Two Drivers: Exactly two, every time. Never more, never fewer.
•	Wellness Only (through Phase 3): No clinical language, no diagnostic framing, no physician referrals in any copy or output.
•	Never Silent During Deterioration: Ghost Mode (At-Risk) always surfaces a soft intervention. This is an architectural constraint, not a preference.
•	LLM Does Not Decide: Claude explains domain outputs. Claude never influences scores, flags, or drivers.
 
 
06 — Key Decisions Log

The following decisions were made during the April 2026 brand and product vision sessions. Each is recorded here so it does not need to be relitigated.

Decision	Rationale	Status
Product name: Chronos by MBI	Chronos is already the scoring engine name — naming the product after its core IP is coherent. MBI provides institutional credibility. Two-tier structure proven in market (Alphabet/Google model).	Locked
Logo: TBD — Three options explored (Signal wave, Arc & Mark, Monogram C)	Signal wave (Option A) strongest for brand expression moments. Monogram C (Option C) strongest at small scale / app icon. Hybrid approach possible.	In Review
Color system locked	Void black + Chronos Gold #B8946A + Parchment #F6F3EE. Anti-health-app palette. No teal, no green gradients. Shadow treatment with inset fields.	Locked
Typography locked	Cormorant Garamond (display) + Jost (UI). 'Simple complexity' aesthetic.	Locked
Fourth nav tab: Horizon	Today / Trend / Domains / Horizon. Horizon houses Risk Intelligence, Health Education, and Allostatic Portrait. Separates the long-range prevention layer from the daily loop.	Locked
Risk Horizon: pathway visibility, not clinical diagnosis	Shows upstream node activation from the ontology engine in plain language. Never predicts disease. Always framed as early and reversible. Wellness framing maintained.	Locked
Education: contextual, not library-first	Knowledge arrives inline when a metric repeats or a domain activates. More powerful than a library the user has to find.	Locked
Allostatic Portrait: descending line = progress	Lower load over time is the visual representation of prevention working. This is the retention payoff surface after 30 days.	Locked
Phase sequencing: Phase 0 concept proven, Phase 1 in progress, Phase 1.5 UX/UI polish	Three previous iterations failed by building too much before validating. Current approach is deliberately narrow. Phase gate discipline is non-negotiable.	Active
90-day baseline bootstrap on onboarding	Upgrade from original 7-day ramp. Pulls 90 days of Apple Health history immediately, giving users a meaningful baseline from Day 1.	Live

6.1 Open Questions
The following items require explicit decisions before Phase 2 begins:

•	Logo direction: Signal wave vs. Monogram C vs. hybrid. Needs founder decision.
•	Subscription pricing: Revenue Model shows $99/$199/$299 (original). FAQ shows $10–40/mo (later revision). Needs reconciliation before Phase 3.
•	FDA SaMD positioning: As the Risk Horizon surface deepens clinical inference, regulatory classification needs legal review. Must be resolved before Phase 3.
•	Medical advisory board: No named clinical advisors documented. Required before any external fundraising or clinical credibility conversations.
•	Technical co-founder: Build is accelerating. Solo founder carrying both product and engineering is a Phase 3 risk. Who Not How principle applies.



CHRONOS
Mynd & Bodi Institute  ·  Future State Document v1.0  ·  April 2026  ·  Confidential
