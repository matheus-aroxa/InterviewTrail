# Vision Document: InterviewTrail

**Version:** 1.0
**Date:** 09/21/2026
**Author:** Matheus Aroxa

---

## 1. Introduction

This document presents the product vision for **InterviewTrail**, a web platform that generates personalized technical interview simulations by combining a target job posting with the candidate's own code portfolio on GitHub.

This document describes the product in its consolidated form, aimed at real production operation, with its own business model, maintained and evolved independently.

---

## 2. Positioning

### 2.1 Business opportunity

Early career candidates frequently arrive at technical interviews without knowing what will actually be covered, nor how their own project portfolio will be interpreted by a technical interviewer. This uncertainty, more than the absence of technical knowledge itself, is one of the biggest sources of insecurity in technology hiring processes.

Existing solutions on the market focus mostly on generic algorithmic problems (LeetCode style), a practice less widespread in the Brazilian market than in the international market, and disconnected from the candidate's real experience. No widely adopted solution generates an interview from two simultaneous and personal sources: the specific job the candidate is targeting and the code the candidate has actually written. This gap was confirmed by a market benchmarking study of the main competitors (see [Appendix A](#appendix-a-market-benchmarking)).

### 2.2 Problem statement

| | |
|---|---|
| **The problem** | Early career candidates lack clarity about which technical competencies will be evaluated in a real interview, and about how their own portfolio projects will be questioned by a technical interviewer. |
| **Affects** | Early career developers preparing for technology hiring processes. |
| **The impact of that is** | Insecurity during preparation, generic practice answers that do not reflect what will actually be asked, and difficulty anticipating questions about decisions made in their own code. |
| **A successful solution would be** | An application that generates technical interview simulations personalized to the target job and to the candidate's real portfolio, including questions about specific technical decisions in their own code, followed by an actionable performance report. |

### 2.3 Product positioning statement

For **early career candidates** who **need to prepare for technical interviews with clarity about what will be covered**, **InterviewTrail** is a **web platform for technical interview simulation** that **generates personalized questions by combining the target job with the candidate's real code on GitHub**. Unlike **generic algorithmic training platforms (LeetCode style) and interview simulators with standardized questions**, our product **questions the candidate about real decisions made in their own projects, with questions that cite specific excerpts from their code**.

---

## 3. Stakeholder and User Description

### 3.1 Stakeholder summary

| Stakeholder | Description | Main interest |
|---|---|---|
| Candidate (end user) | Early career developer looking for a technology job | Arriving at the real interview with more confidence and clarity about technical gaps |
| Advertisers (indirect) | Ad partners displayed on the free plan | Reaching an audience of early career developers |
| Supporters/donors | Users willing to contribute financially without necessarily using a paid plan | Supporting the continuity of the project |

### 3.2 Target user profile

- Developer with little or no previous experience with technical hiring processes.
- Has at least one public repository (or one accessible via OAuth) on GitHub that represents their work.
- Is targeting a concrete job (already identified) and seeks preparation directed at it, not generic training.
- Current environment: uses (or has already tried) algorithmic training platforms and generic interview simulators, but feels they do not reflect what is actually asked nor consider their real portfolio.

### 3.3 Key user needs

| Need | Priority | Current situation | Proposed solution |
|---|---|---|---|
| Knowing what will be covered in an interview for a specific job | High | Generic preparation, disconnected from the real job | AI extraction of the job's technical profile |
| Understanding how their own code will be questioned | High | No solution on the market covers this adequately | Question generation from analysis of the candidate's repository |
| Practicing in a format close to the real thing (oral, not just written) | Medium | Text/quiz simulators | Simulation with voice narration (TTS) |
| Knowing where the gaps are after practicing | High | Shallow or nonexistent feedback | Final report with score, strengths, gaps and recommendations |
| Using it at no initial cost | High | None | Freemium model with limited free usage |

---

## 4. Product Overview

### 4.1 Product perspective

InterviewTrail is a new, independent product, with no dependency on or integration with other products. It consumes third party services essential to its operation: authentication and repository reading via GitHub OAuth/API, a generative AI provider for job profile extraction, relevant file selection and question/report generation, and a text to speech service for interview narration.

### 4.2 Feature summary (high level)

| Feature | User benefit |
|---|---|
| Authentication via GitHub | Passwordless login, natural access to the user's own repositories |
| Target job registration | Allows the interview to be personalized to the real opportunity the candidate is pursuing |
| Repository selection for analysis | Bases the interview on the candidate's real work, not on generic exercises |
| Personalized interview generation (logic, scenario, project, code analysis) | Covers both general technical reasoning and specific questioning about decisions in the candidate's own code |
| Voice narration of the interview | Brings the simulation closer to the experience of a real oral interview |
| Final performance report | Provides objective clarity about strengths, gaps and job fit |
| Plan model (free/paid) | Allows limited use at no cost, and full use through a subscription |
| Support via donation | Allows contributing to the project independently of using a paid plan |

### 4.3 Assumptions and dependencies

- Availability and stability of the GitHub API for OAuth and repository reading.
- Availability of a generative AI provider with a viable per use cost to sustain the free plan.
- Availability of a text to speech service (or an acceptable fallback in the user's browser).
- The candidate has at least one repository with enough content to generate a relevant interview.
- Feasibility of processing payments and donations for users in Brazil.

---

## 5. Product Features

*(Described at a high level. The behavioral detailing of each one will be formalized in the use case documents.)*

1. **User authentication and account** via GitHub OAuth.
2. **Job registration and interpretation**: automatic extraction of a technical profile (technologies, seniority, competencies) from the text pasted by the candidate.
3. **Repository selection and code analysis**: choice of the candidate's own repository and intelligent selection of the files most relevant to the job.
4. **Interview simulation**: conducting a session of logic, scenario, project and code analysis questions, with voice narration.
5. **Performance report**: final evaluation with overall score, per dimension ratings, job fit, strengths, gaps and recommendations.
6. **Plan and subscription management**: usage control according to tier (free/paid), upgrade and cancellation.
7. **Ad display**: for users on the free plan, as part of the monetization model.
8. **One time donation**: direct financial contribution to the project, independent of the plan.
9. **Session history**: access to the candidate's previous interviews and reports.

---

## 6. Constraints

- **Business model:** freemium. Free usage with limitations and ads; paid plans for ad removal and full access; option for a one time donation.
- **Privacy and compliance:** adherence to LGPD (Brazil's General Data Protection Law); the application must handle only the authenticated user's own data and public content of repositories they themselves choose to analyze, with no collection of third party personal data.
- **Operating cost:** the use of generative AI has a direct cost per call; the free plan needs to be sized so it does not make the solo operation of the project financially unviable.
- **Domain continuity:** the data model and business rules for session, question, answer, report and AI cost tracking per session must be preserved as the foundation of the domain.

---

## 7. Quality Ranges

| Attribute | Intent |
|---|---|
| **Usability** | The candidate's flow (login, job, repository, interview, report) should be navigable without needing prior instruction. |
| **Reliability** | Failures in third party services (AI, TTS) should not prevent completion of the interview; they should degrade in a controlled way (e.g. voice fallback), without loss of the candidate's progress. |
| **Security** | Credentials and access tokens for third party services (GitHub) must be protected at rest; authentication and authorization must cover all routes that expose user data. |
| **Privacy** | No third party personal data (beyond the authenticated user's own) should be collected or stored. |
| **Cost auditability** | AI cost per session must be traceable, serving as the basis for sizing the free and paid plans. |
| **Availability** | The application should be consistently available for public use, in line with the standard expected of a production product. |

*(Quantitative goals for performance, availability and scale will be defined in the architecture document, in light of the technical decisions.)*

---

## 8. Precedence and Prioritization

| Phase | Scope |
|---|---|
| **Production MVP (Release 1)** | Authentication, job registration, repository selection, interview generation (all question types), final report, free plan with limits, TTS with fallback. |
| **Release 2, Monetization** | Paid plans, ad display on the free plan, one time donation, session history. |
| **Release 3, Evolution** | Personalization refinements, expansion of analysis types, items to be prioritized based on real usage and candidate feedback. |

---

## 9. Other Product Requirements

- **Legal compliance:** adherence to LGPD regarding the collection and processing of the authenticated user's data.
- **Licensing:** to be defined. The product's distribution license must be reviewed and formalized before public launch.
- **Brand:** the product uses the name **InterviewTrail**.

---

## Appendix A: Market Benchmarking

Comparative analysis between InterviewTrail and seven established technical interview preparation platforms on the market (Pramp/Exponent, Interviewing.io, Hello Interview, PracHub, Revarta, Big Interview and LeetCode Premium). Data gathered through public research (official sites and independent comparisons), 09/21/2026.

### Methodology and Sources

Competitors selected by relevance in market searches about technical interview preparation (independent 2026 comparisons, official product sites). Prices in USD as shown on each site's public pricing table at the time of research; subject to change by the providers. No identified competitor offers automated analysis of the candidate's source code/repository as a basis for question generation.

### A.1 Competitors: Overview

| Product | Category | Value Proposition | Interviewer Model | Main Focus | Target Audience | Price Range (USD) | Site |
|---|---|---|---|---|---|---|---|
| **InterviewTrail** | AI + code portfolio | Generates a personalized technical interview by combining the target job with the candidate's real code on GitHub | AI (text + voice/TTS) | Personalization via job + real code repository | Early career candidates | Freemium: $0 (limited, with ads) up to a paid plan + donation | N/A |
| Pramp (Exponent) | Peer to peer | Live practice with other candidates, alternating interviewer and interviewee roles | Human (peers) | Free collaborative practice, broad coverage of interview types | Candidates of all levels looking for free practice | Free (integrated into Exponent) | exponent.dev / pramp.com |
| Interviewing.io | Live human coaching | Simulated interviews with real engineers, many from "FAANG" companies, with detailed feedback | Human (experienced engineers) | Rigor and realism of a real interview, qualified feedback | Advanced candidates targeting high technical bar companies | USD 170 to 419 per session | interviewing.io |
| Hello Interview | Human coaching + AI (system design) | Mocks with coaches from target companies, courses and guided system design practice with AI | Human (mocks) + AI (guided practice) | System design, low level design, behavioral | Mid level to senior/staff candidates | USD 34 to 79 subscription + USD 160 to 419 per mock | hellointerview.com |
| PracHub | Question bank + AI | Bank of recent real questions with written solutions, AI coaching for behavioral and system design | AI + static content | Volume of real, up to date questions | Candidates in broad preparation, all levels | Freemium with a large free tier | prachub.com |
| Revarta | AI voice for behavioral | Voice interviews by AI with feedback calibrated by hiring managers, behavioral focus | AI (voice) | Direct and critical feedback on behavioral questions | Candidates preparing for behavioral/fit rounds | First question free, then USD 49/month | revarta.com |
| Big Interview | Structured course + AI | Curated video lessons, structured practice, endorsed by an academic institution (UC Berkeley) | AI (practice) + video content | Structured teaching for beginners, behavioral | Beginners and candidates seeking fundamentals | Subscription (check site) | biginterview.com |
| LeetCode Premium | Algorithmic training | The market's largest bank of algorithmic problems, technical coding interview simulations | None (self assessment) | Programming logic and data structures | Candidates focused on algorithmic ("LeetCode style") challenges | Subscription (check site) | leetcode.com |

### A.2 Feature Comparison

| Category | Feature | InterviewTrail | Pramp (Exponent) | Interviewing.io | Hello Interview | PracHub | Revarta | Big Interview | LeetCode Premium |
|---|---|---|---|---|---|---|---|---|---|
| Personalization | Questions generated from a real job provided by the candidate | Yes | No | Partial (generic focus) | Partial (question bank, not generation) | No | Partial | No | No |
| Personalization | Analysis of the candidate's real code (GitHub repository) | Yes | No | No | No | No | No | No | No |
| Personalization | Questions about technical decisions in the candidate's own projects | Yes | No | Partial (if mentioned by the candidate) | No | No | No | No | No |
| Format | Live human interviewer | No | Yes (peer) | Yes (experienced engineer) | Yes (coach) | No | No | No | No |
| Format | AI interviewer | Yes | No | No | Partial (system design) | Yes | Yes | Partial | No |
| Format | Voice narration/interaction (TTS) | Yes | No (live video) | No (live video) | No | No | Yes | No | No |
| Content | Programming logic questions | Yes | Yes | Yes | Partial | Yes | No | Partial | Yes |
| Content | Scenario/behavioral questions | Yes | Yes | Yes | Yes | Yes | Yes | Yes | No |
| Content | System design | No (out of current scope) | Yes | Yes | Yes (main focus) | Yes | No | Partial | No |
| Evaluation | Final report with score and recommendations | Yes | Partial (peer feedback) | Yes (human feedback) | Yes | Yes | Yes | Yes | Partial (grading only) |
| Evaluation | Candidate session history tracking | Yes | Partial | Yes | Yes | Yes | Yes | Yes | Yes |
| Business | Functional free plan (not just a trial) | Yes | Yes | No | Partial (paid course) | Yes | Partial (first question) | No | Partial |
| Business | Direct donation support model | Yes | No | No | No | No | No | No | No |

**Legend:** Yes: feature present. Partial: present in a limited way. No: absent.

### A.3 Price Comparison

| Product | Free Plan | Entry Plan (paid) | Mid tier/Premium Plan | Advanced Plan/Per Session | Base Currency | Note |
|---|---|---|---|---|---|---|
| **InterviewTrail** | Yes: limited usage, with ads | Subscription to remove ads and unlock full usage (to be defined) | N/A | One time donation to support the project | BRL | Model defined in the product vision document; amounts not yet set |
| Pramp (Exponent) | Yes: unlimited sessions via peer matching | N/A | N/A | N/A | USD | Completely free; indirect monetization via Exponent (structured content) |
| Interviewing.io | No | USD 170 (general mock, junior/mid/senior level) | USD 269 (general mock, staff+/manager level) | USD 289 to 419 (mock for a specific target company) | USD | Per session pricing, no recurring subscription |
| Hello Interview | No (limited trial) | USD 34 to 47/month (Premium, content + guided practice) | USD 55 to 79/year (annual Premium) | USD 160 to 419 per live mock + USD 199 to 285 lifetime | USD | Price varies by level (junior to staff+/manager) |
| PracHub | Yes: largest free tier among cited competitors | Subscription (price not publicly disclosed) | N/A | N/A | USD | Focus on recent, real questions |
| Revarta | Yes: first question free | USD 49/month (unlimited usage) | N/A | N/A | USD | No mid tier disclosed |
| Big Interview | Limited trial | Subscription (price not publicly disclosed) | N/A | N/A | USD | Endorsed by UC Berkeley; focus on video content |
| LeetCode Premium | Yes: a large part of the problem bank | Subscription (price not publicly disclosed) | N/A | N/A | USD | Mostly focused on algorithms, not a full interview |

> **Note:** Prices in USD collected from official sites and independent comparisons (09/21/2026); subject to change by the providers. Interviewing.io and Hello Interview charge mostly on a per session basis with a human interviewer, a model structurally different from the recurring subscription SaaS planned for InterviewTrail.

### A.4 Differentiation Analysis

**Identified market gap:** no competitor analyzed generates interview questions from the combination of (1) a real job provided by the candidate and (2) analysis of the code present in the candidate's own repository. Human platforms (Pramp, Interviewing.io, Hello Interview) depend on peer/coach availability and do not scale at an accessible price; existing AI platforms (Revarta, Big Interview) address behavioral/delivery aspects, not technical depth on the candidate's real portfolio.

| Dimension | How competitors address it today | How InterviewTrail differentiates |
|---|---|---|
| Technical personalization | Generic questions by category (algorithm, system design, behavioral), with no link to the candidate's code | Questions generated from the real code in the chosen repository, citing specific excerpts |
| Cost of access | Quality human feedback costs USD 160 to 419 per session (Interviewing.io, Hello Interview) | Free usage with limitations, no entry cost; accessible to those just starting out |
| Scalability | Peer to peer (Pramp) and human models depend on people's availability | Available at any time, with no dependency on matching or a third party's schedule |
| Coverage of the Brazilian market | Competitors mostly priced in USD and focused on the American market | Pricing and donation model designed for the local context and currency (BRL) |
| Sustainability without a barrier | Competing freemium models (Pramp) do not monetize; paid models (Interviewing.io) have a high barrier | Freemium with ads + subscription + one time donation, balancing free access and financial viability |

**Competitive risks to monitor:**

- The quality of AI generated questions needs to overcome the "generic" perception already associated with low cost AI tools (mentioned in comparisons about Revarta).
- Platforms with human feedback (Interviewing.io, Hello Interview) have a superior perceived quality/rigor; the AI's final report needs to be objectively actionable to compete on that perception.
- Established free competitors (Pramp/Exponent) already have network effects and brand recognition.

---

## Revision History

| Version | Date | Description | Author |
|---|---|---|---|
| 1.0 | 09/21/2026 | Initial version of the vision document | Matheus Aroxa |