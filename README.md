# InterviewTrail

InterviewTrail is a web platform that generates personalized technical interview simulations by combining a target job posting with the candidate's own code portfolio on GitHub.

Instead of generic algorithmic drills, InterviewTrail asks the candidate about real decisions made in their own projects, citing specific excerpts from their code, and closes each session with an actionable performance report.

> **Status:** early development. The project is currently backend/frontend scaffolding with no implemented features yet. See the [product documentation](#documentation) for the full vision and scope.

## Why

Early career candidates often arrive at technical interviews without knowing what will actually be covered, or how their own portfolio will be read by a technical interviewer. InterviewTrail closes that gap by generating an interview from two personal sources at once: the job the candidate is targeting, and the code they have actually written.

## Core features (planned)

- **Authentication via GitHub OAuth** — passwordless login with natural access to the candidate's own repositories.
- **Target job registration** — AI extraction of a technical profile (technologies, seniority, competencies) from a pasted job posting.
- **Repository selection and code analysis** — intelligent selection of the files most relevant to the job.
- **Personalized interview simulation** — logic, scenario, project and code analysis questions, narrated by voice (TTS).
- **Performance report** — overall score, per-dimension ratings, job fit, strengths, gaps and recommendations.
- **Freemium plan model** — limited free usage with ads, paid plans for full access, and one-time donations.

Full scope and prioritization across releases are detailed in the [requirements document](documents/requirements-document.md).

## Tech stack

| Layer | Stack |
|---|---|
| Backend | Java 27, Spring Boot 4 (Maven) |
| Frontend | React 19, TypeScript, Vite |
| Tooling | Husky + lint-staged, commitlint (Conventional Commits), Spotless (Google Java Format), ESLint + Prettier |
| CI | GitHub Actions (style check, commitlint, SonarCloud, release-please) |

## Project structure

```
InterviewTrail/
├── backend/      Spring Boot application (Java 27, Maven)
├── frontend/     React + Vite + TypeScript application
└── documents/    Product vision and requirements documents
```

## Getting started

### Prerequisites

- Java 27 (JDK)
- Node.js 20+ and npm

### Backend

```bash
cd backend
./mvnw spring-boot:run
```

### Frontend

```bash
cd frontend
npm install
npm run dev
```

## Development workflow

This repository uses [Conventional Commits](https://www.conventionalcommits.org/), enforced via commitlint and a Husky `commit-msg` hook. Commit scopes are restricted to `backend`, `frontend`, `infra` and `repo`.

Install root-level tooling once to enable the git hooks:

```bash
npm install
```

Pre-commit runs `lint-staged`, which applies Spotless formatting to staged Java files and ESLint/Prettier to staged TypeScript files.

## Documentation

- [Vision document](documents/vision-document.md) — product positioning, target users, feature summary and market benchmarking.
- [Requirements document](documents/requirements-document.md) — functional and non-functional requirements, traceable across releases.

## License

To be defined.
