# AI Career Operating System

An AI-powered operating system that automates and scales the modern job search while keeping a human in the loop for strategic decisions.

Instead of treating ChatGPT, Claude, and Codex as separate tools, this project combines them into a coordinated workflow for job discovery, resume customization, application tracking, and interview preparation.

---

## Overview

This system was built to solve a simple problem:

Traditional job searching requires hours of repetitive work every day:
- Searching dozens of job boards
- Checking duplicate postings
- Tailoring resumes manually
- Tracking applications
- Preparing for interviews

This project turns those repetitive tasks into an AI-assisted workflow so that time can be spent on higher-value work instead.

---

## Architecture

```text
                    AI Career Operating System

                ┌───────────────────────────────┐
                │      Job Criteria (MD)        │
                └──────────────┬────────────────┘
                               │
                               ▼
                    Daily Job Discovery on LinkedIn
                         (Codex)
                               │
                               ▼
                  Curated Job Recommendations
                               │
                               ▼
                  Human Selects Target Roles
                               │
                               ▼
                 Resume Tailoring (Claude)
                               │                               │
                               ▼
              Application Tracking (Email API)
```

---

# Components

## 1. Job Discovery

Responsible AI:
- Codex

Responsibilities:

- Reads job criteria
- Searches official company career pages
- Searches authenticated LinkedIn Jobs
- Removes duplicates
- Filters by work authorization
- Produces daily job recommendations

---

## 2. Resume Tailoring

Responsible AI:
- Claude

Responsibilities:

- Reads Master Resume
- Tailors resume for each job
- Generates Word document
- Produces Delta Report
- Generates tracking log

---

## 3. Application Tracking

Responsibilities:

- Updates application tracker
- Reads confirmation emails
- Tracks application status
- Prevents duplicate applications

---


# Repository Structure

AI-Career-Operating-System/

README.md

criteria/
    job_criteria.md

prompts/
    codex-job-search.md
    claude-resume.md
    chatgpt-review.md

skills/
    Claude/

tracker/
    job_tracker.xlsx

templates/
    Master_Resume_Template.docx

docs/
    workflow.md
    architecture.md

examples/
    sample-job-report.md
    sample-resume.md
```

---

# Design Principles

- Human-in-the-loop decision making
- AI handles repetitive work
- Single source of truth for resume content
- No fabricated experience
- Reproducible workflow
- Modular AI agents
- Transparent outputs

---

# Tech Stack

- ChatGPT
- Claude
- Codex
- GitHub
- LinkedIn
- Microsoft Excel
- Microsoft Word
- Markdown
- Email Connector
- Git

---

# Current Features

- Daily AI-powered job discovery
- Resume customization
- Job matching workflow
- Application tracking
- Prompt engineering
- Claude Skills
- Modular architecture

---

# Roadmap

- [ ] Automatic application submission
- [ ] ATS compatibility scoring
- [ ] Cover letter generation
- [ ] Portfolio optimization
- [ ] AI career strategy planner
- [ ] Multi-agent orchestration

---

# Philosophy

AI should not replace career decisions.

It should eliminate repetitive work so that people can spend more time making better career decisions.

The goal of this project is not to automate job searching entirely, but to build an AI operating system that augments human judgment throughout the process.

---

# License

MIT License
