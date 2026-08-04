# AI Career Operating System

A human-in-the-loop framework for running a more consistent, evidence-based job search with Codex and Claude.

This repository provides reusable Markdown instructions, prompts, and AI skills for job discovery, resume tailoring, cover-letter writing, and application tracking. It is designed to reduce repetitive work while keeping the user responsible for choosing roles, reviewing materials, submitting applications, and confirming tracker updates.

> **Project status:** Early-stage template. This repository contains AI instructions rather than a standalone application. It does not automatically submit applications, contact employers, or include the user's private resume and application tracker.

## What the framework supports

- Define target roles, locations, compensation requirements, experience levels, and work-authorization constraints.
- Search official employer career pages and authenticated LinkedIn Jobs.
- Verify posting freshness, active status, source quality, and direct application links.
- Compare recommendations with a user-provided tracker to reduce duplicates and reposts.
- Tailor resumes to individual job descriptions without inventing experience or metrics.
- Generate ATS-conscious resume content and a strict one-page Word layout specification.
- Draft concise, role-specific cover letters grounded in the master resume.
- Keep job discovery, application submission, and application status as separate states.

## How it works

```text
Job-search criteria + private application tracker
                      |
                      v
        Codex searches and verifies openings
                      |
                      v
          Ranked job recommendation report
                      |
                      v
             Human selects a target role
                      |
                      v
        Claude tailors the resume and letter
                      |
                      v
           Human reviews and applies directly
                      |
                      v
     Tracker is updated only with confirmation
```

The framework intentionally separates discovery from application. Finding or recommending a role never means that the user applied to it.

## Repository contents

```text
AI-Job-Search-Automation/
├── README.md
├── LICENSE
├── codex-instructions/
│   ├── AGENTS.md
│   └── job-search-criteria.md
├── prompts/
│   ├── job-discovery-codex.md
│   ├── job-tracker-codex.md
│   ├── resume-tailor-claude.md
│   └── weekly-summary.md
└── claude-skills/
    ├── cover-letter.md
    ├── resume-format.md
    ├── resume-toolkit.md
    └── old/
        ├── bullet-writer.md
        ├── resume-ats.md
        └── resume-tailor.md
```

### Codex instructions

- `codex-instructions/AGENTS.md` defines workspace-wide rules for discovery, tracker updates, and weekly reviews.
- `codex-instructions/job-search-criteria.md` is the authoritative search policy. It includes role tiers, location and compensation filters, work-authorization rules, allowed sources, duplicate detection, and active-listing verification.

### Prompts

- `prompts/job-discovery-codex.md` specifies the daily discovery workflow and report format.
- `prompts/job-tracker-codex.md` prevents unconfirmed or invented tracker updates.
- `prompts/resume-tailor-claude.md` defines the master-resume truthfulness rule, DELTA report, and tracking-log output.
- `prompts/weekly-summary.md` is currently an empty placeholder for a future weekly-review workflow.

### Claude skills

- `claude-skills/resume-toolkit.md` combines resume tailoring, achievement-focused bullet writing, and ATS analysis.
- `claude-skills/resume-format.md` defines the approved one-page Word layout and file-naming contract.
- `claude-skills/cover-letter.md` defines evidence, structure, tone, and plain-text output rules for cover letters.
- `claude-skills/old/` preserves the three earlier resume skills that were consolidated into `resume-toolkit.md`. New workflows should use the consolidated skill.

## Before you use it

The public repository intentionally does not include personal career data. Create or supply the following in your private working environment:

1. A completed `job-search-criteria.md`. The repository version contains blank fields for job families, preferred locations, compensation ranges, and target companies.
2. A private `job_tracker.xlsx` used as the application record and duplicate-checking source.
3. A private master resume containing only verified experience, responsibilities, achievements, skills, and metrics.
4. Optional `daily_searches/` and `weekly_reviews/` folders if you want to retain generated reports.
5. A Word-document generation method if you want `.docx` output. The current resume-format skill references `scripts/build_resume.js`, but that script is not included in this repository.

Do not commit resumes, contact details, application histories, email content, or other personal information to a public fork.

## Quick start

### 1. Clone the repository

```bash
git clone https://github.com/ElvaWang-06/AI-Job-Search-Automation.git
cd AI-Job-Search-Automation
```

### 2. Personalize the search policy

Complete the blank sections in `codex-instructions/job-search-criteria.md`. Review every exclusion and source rule before using the discovery prompt.

### 3. Add private working files

Add your master resume and application tracker to a private workspace. Keep them out of the public repository.

### 4. Configure the AI tools

Make the Codex instruction files and relevant prompts available to your Codex project. Add the active files under `claude-skills/` to the Claude environment used for resume and cover-letter work.

### 5. Run the workflow

1. Start job discovery after signing in to LinkedIn when LinkedIn results are required.
2. Review the verified recommendation report.
3. Select a role yourself.
4. Provide the job description and master resume for tailoring.
5. Review every generated claim and document before applying.
6. Update the tracker only after explicitly confirming what happened.

## Guardrails

The project is built around several non-negotiable rules:

- Never fabricate a job, URL, posting date, salary, sponsorship detail, skill, experience, achievement, or metric.
- Never treat a discovered job as an application.
- Never modify the tracker or mark a role as applied without explicit confirmation.
- Never apply, upload a resume, or contact an employer without the user's direct action or authorization.
- Exclude expired, inaccessible, unverifiable, and duplicate listings.
- Use the master resume as the sole source of truth for application materials.
- Report unsupported job requirements as gaps instead of hiding them.

AI output can still be incomplete or incorrect. Verify every posting and review every application document before using it.

## Current limitations

- There is no executable orchestration layer or scheduled automation in the repository.
- The private tracker, master resume, generated reports, and resume template are not included.
- The Word-generation script referenced by `resume-format.md` is not included.
- The weekly-summary prompt has not yet been implemented.
- The discovery files contain conflicting quota language: some require exactly 15 recommendations, while the criteria file says quality must never be lowered to meet a fixed count. Resolve this before production use; verified quality should take priority.
- Interview preparation and email-based status tracking are not implemented in the current files.

## Roadmap

- [ ] Complete the weekly-review prompt.
- [ ] Add a privacy-safe tracker template and schema documentation.
- [ ] Add the Word resume build and visual-verification workflow.
- [ ] Validate file references and rules automatically across prompts and skills.
- [ ] Add sample outputs using fictional data.
- [ ] Add interview-preparation instructions.
- [ ] Add optional, human-approved email status tracking.

## Design principles

- Human judgment remains in control.
- Quality matters more than recommendation volume.
- Private career data stays private.
- Source-of-truth files govern all generated output.
- AI-generated claims must be traceable to evidence.
- Workflows should be modular, reviewable, and easy to revise.

## License

Released under the [MIT License](LICENSE).
