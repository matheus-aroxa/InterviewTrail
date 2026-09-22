# Requirements Document: InterviewTrail

**Version:** 1.0
**Date:** 09/21/2026
**Author:** Matheus Aroxa

---

## 1. Introduction

This document lists the functional and non functional requirements for InterviewTrail, derived from the Vision Document. Requirements are numbered sequentially (RF for functional, RNF for non functional) to support traceability into future use case documents and architecture decisions. Numbering is stable and independent of priority: the **Release** column indicates when each requirement is planned to be delivered, following the phases defined in the Vision Document (Precedence and Prioritization).

Each requirement is written as a single, atomic, testable statement. A requirement that depends on another is marked in the **Depends on** column.

---

## 2. Functional Requirements

| ID | Description | Release | Depends on |
|---|---|---|---|
| RF01 | The system shall allow the user to authenticate using GitHub OAuth. | Release 1 (MVP) | None |
| RF02 | The system shall not require the user to create or store a password. | Release 1 (MVP) | RF01 |
| RF03 | The system shall create a user account automatically on first successful GitHub authentication. | Release 1 (MVP) | RF01 |
| RF04 | The system shall allow the authenticated user to view their own profile information. | Release 1 (MVP) | RF03 |
| RF05 | The system shall allow the user to log out, invalidating the active session. | Release 1 (MVP) | RF01 |
| RF06 | The system shall allow the user to paste the text of a target job posting. | Release 1 (MVP) | RF03 |
| RF07 | The system shall use AI to extract a structured technical profile from the pasted job posting, including technologies, seniority level and key competencies. | Release 1 (MVP) | RF06 |
| RF08 | The system shall persist the registered job posting and its extracted technical profile, associated with the user. | Release 1 (MVP) | RF07 |
| RF09 | The system shall allow the user to list the repositories accessible through their GitHub account. | Release 1 (MVP) | RF01 |
| RF10 | The system shall allow the user to select one repository to be used as the basis for an interview session. | Release 1 (MVP) | RF09 |
| RF11 | The system shall use AI to select, from the chosen repository, a limited subset of the files most relevant to the registered job (between 5 and 20 files). | Release 1 (MVP) | RF08, RF10 |
| RF12 | The system shall not send the entire content of a repository to the AI provider in a single request. | Release 1 (MVP) | RF11 |
| RF13 | The system shall allow the user to start an interview session after a job posting and a repository have been registered. | Release 1 (MVP) | RF08, RF10 |
| RF14 | The system shall generate logic type questions, focused on general technical reasoning in the language of the target job. | Release 1 (MVP) | RF13 |
| RF15 | The system shall generate scenario type questions, describing a hypothetical work situation related to the target job. | Release 1 (MVP) | RF13 |
| RF16 | The system shall generate project type questions, based on real decisions identifiable in the selected repository. | Release 1 (MVP) | RF11, RF13 |
| RF17 | The system shall generate code analysis type questions that reference a specific excerpt of code from the selected repository. | Release 1 (MVP) | RF11, RF13 |
| RF18 | The system shall present interview questions to the user through voice narration (text to speech). | Release 1 (MVP) | RF13 |
| RF19 | The system shall fall back to a browser based voice synthesis mechanism when the primary text to speech service is unavailable or misconfigured. | Release 1 (MVP) | RF18 |
| RF20 | The system shall notify the user, within the interview interface, when voice narration is running in fallback mode. | Release 1 (MVP) | RF19 |
| RF21 | The system shall allow the user to submit an answer to each interview question. | Release 1 (MVP) | RF13 |
| RF22 | The system shall record every question and answer of a session in the order they occurred. | Release 1 (MVP) | RF21 |
| RF23 | The system shall generate a final report at the end of a completed interview session. | Release 1 (MVP) | RF22 |
| RF24 | The final report shall include an overall performance score. | Release 1 (MVP) | RF23 |
| RF25 | The final report shall include a per dimension rating (at minimum, one rating per question type used in the session). | Release 1 (MVP) | RF23 |
| RF26 | The final report shall include an assessment of the candidate's fit to the registered job. | Release 1 (MVP) | RF23 |
| RF27 | The final report shall include identified strengths. | Release 1 (MVP) | RF23 |
| RF28 | The final report shall include identified gaps. | Release 1 (MVP) | RF23 |
| RF29 | The final report shall include actionable recommendations. | Release 1 (MVP) | RF23 |
| RF30 | The system shall track, for each interview session, the number of input and output tokens consumed by AI calls. | Release 1 (MVP) | RF13 |
| RF31 | The system shall calculate and store an estimated AI cost for each interview session, based on token consumption. | Release 1 (MVP) | RF30 |
| RF32 | The system shall enforce a monthly limit on the number of interview sessions available to a free tier user. | Release 1 (MVP) | RF13 |
| RF33 | The system shall enforce a monthly limit on the number of questions generated for a free tier user. | Release 1 (MVP) | RF14, RF15, RF16, RF17 |
| RF34 | The system shall prevent a free tier user from starting a new interview session after their monthly limit has been reached. | Release 1 (MVP) | RF32 |
| RF35 | The system shall inform the user, before or during the interview flow, when a usage limit has been reached. | Release 1 (MVP) | RF34 |
| RF36 | The system shall encrypt the user's GitHub access token before persisting it. | Release 1 (MVP) | RF01 |
| RF37 | The system shall never persist the user's GitHub access token in plain text. | Release 1 (MVP) | RF36 |
| RF38 | The system shall allow the user to view a list of their previous interview sessions. | Release 1 (MVP) | RF23 |
| RF39 | The system shall allow the user to open the final report of a previous interview session. | Release 1 (MVP) | RF38 |
| RF40 | The system shall offer at least two subscription plans: a free plan and a paid plan. | Release 2 (Monetization) | RF32 |
| RF41 | The system shall allow a user on the free plan to upgrade to a paid plan. | Release 2 (Monetization) | RF40 |
| RF42 | The system shall allow a user on a paid plan to cancel their subscription. | Release 2 (Monetization) | RF40 |
| RF43 | The system shall process subscription payments through a third party payment provider. | Release 2 (Monetization) | RF41 |
| RF44 | The system shall update the user's plan status automatically upon receiving a payment confirmation from the payment provider. | Release 2 (Monetization) | RF43 |
| RF45 | The system shall update the user's plan status automatically upon receiving a payment cancellation or failure notification from the payment provider. | Release 2 (Monetization) | RF43 |
| RF46 | The system shall remove the monthly usage limits described in RF32 and RF33 for users on a paid plan. | Release 2 (Monetization) | RF40 |
| RF47 | The system shall display advertisements to users on the free plan. | Release 2 (Monetization) | RF40 |
| RF48 | The system shall not display advertisements to users on a paid plan. | Release 2 (Monetization) | RF47 |
| RF49 | The system shall allow any user, regardless of plan, to make a one time donation to support the project. | Release 2 (Monetization) | RF03 |
| RF50 | The system shall not require a donation in order to access the free plan's functionality. | Release 2 (Monetization) | RF49 |
| RF51 | The system shall issue a payment confirmation to the user after a successful donation. | Release 2 (Monetization) | RF49 |
| RF52 | The system shall allow the user to configure notification preferences for their account. | Release 3 (Evolution) | RF03 |
| RF53 | The system shall support additional interview question types beyond the four defined for Release 1, to be prioritized based on real usage and candidate feedback. | Release 3 (Evolution) | RF14, RF15, RF16, RF17 |
| RF54 | The system shall allow the user to select the seniority level targeted in an interview session, refining question generation accordingly. | Release 3 (Evolution) | RF13 |

---

## 3. Non Functional Requirements

| ID | Description | Category | Release |
|---|---|---|---|
| RNF01 | The candidate flow (login, job registration, repository selection, interview, report) shall be usable without requiring prior instruction or a tutorial. | Usability | Release 1 (MVP) |
| RNF02 | A failure in the AI provider shall not cause the loss of a candidate's in progress interview session. | Reliability | Release 1 (MVP) |
| RNF03 | A failure in the text to speech provider shall not prevent the completion of an interview session (see RF19, RF20). | Reliability | Release 1 (MVP) |
| RNF04 | GitHub access tokens shall be protected at rest using industry standard encryption (see RF36, RF37). | Security | Release 1 (MVP) |
| RNF05 | Every route that exposes user data shall require authentication. | Security | Release 1 (MVP) |
| RNF06 | Every route that exposes user data shall enforce authorization, ensuring a user can only access their own data. | Security | Release 1 (MVP) |
| RNF07 | Input validation shall be enforced on every endpoint that accepts user provided data. | Security | Release 1 (MVP) |
| RNF08 | The system shall not collect or store personal data belonging to third parties other than the authenticated user. | Privacy | Release 1 (MVP) |
| RNF09 | The system shall only access repository content that the authenticated user has explicitly selected for analysis. | Privacy | Release 1 (MVP) |
| RNF10 | The estimated AI cost per session (see RF31) shall be queryable for reporting and plan sizing purposes. | Cost auditability | Release 1 (MVP) |
| RNF11 | The system shall remain available for public use with a level of consistency appropriate for a production application. | Availability | Release 1 (MVP) |
| RNF12 | The system shall comply with Brazil's General Data Protection Law (LGPD) regarding the collection and processing of user data. | Legal compliance | Release 1 (MVP) |
| RNF13 | Payment data shall be handled through a PCI compliant third party provider; the system shall not store raw payment card data. | Security | Release 2 (Monetization) |
| RNF14 | Advertisement display (see RF47) shall not block or degrade the core interview flow. | Usability | Release 2 (Monetization) |
| RNF15 | Quantitative targets for response time, throughput and scalability shall be defined in the architecture document, once the technical decisions are made. | Performance | To be defined |

---

## 4. Traceability to the Vision Document

| Vision Document section | Related requirements |
|---|---|
| 4.2 Feature summary: Authentication via GitHub | RF01 to RF05 |
| 4.2 Feature summary: Target job registration | RF06 to RF08 |
| 4.2 Feature summary: Repository selection for analysis | RF09 to RF12 |
| 4.2 Feature summary: Personalized interview generation | RF13 to RF20 |
| 4.2 Feature summary: Final performance report | RF21 to RF29 |
| 4.2 Feature summary: Plan model (free/paid) | RF32 to RF35, RF40 to RF46 |
| 4.2 Feature summary: Support via donation | RF49 to RF51 |
| 6. Constraints: Operating cost | RF30, RF31, RNF10 |
| 6. Constraints: Privacy and compliance | RNF08, RNF09, RNF12 |
| 7. Quality Ranges | RNF01 to RNF15 |

---

## 5. Open Points for Future Refinement

- Exact numeric values for free tier limits (RF32, RF33) are not yet defined; they depend on AI cost modeling.
- The specific third party payment provider (RF43) is not yet selected.
- Additional question types for Release 3 (RF53) are not yet specified; they depend on usage data not yet available.
- Quantitative non functional targets (RNF15) are deferred to the architecture document.

---

## Revision History

| Version | Date | Description | Author |
|---|---|---|---|
| 1.0 | 09/21/2026 | Initial version of the requirements document | Matheus Aroxa |