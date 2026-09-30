# ATS Resume Scorer

AI-powered resume-to-job-description matching platform with an actionable **Skill Gap Roadmap**.

Upload a resume + paste a job description. Get ATS compatibility, skill coverage,
a personalized learning roadmap for every missing skill, and PDF report export.

**Live:** _(coming soon)_
**Stack:** FastAPI · Streamlit · spaCy · Sentence Transformers · Groq · Supabase

## What Makes It Different

Most ATS scanners stop at "you're missing Kubernetes and AWS." This one goes one
step further — for every missing skill, it generates a concrete 3-step learning
plan grounded in the JD's seniority level.

## Architecture

    frontend/ (Streamlit) ──HTTP──► backend/ (FastAPI)
                                       ├─ services/parser.py            resume parsing
                                       ├─ services/skill_extractor.py   spaCy NER
                                       ├─ services/scorer.py            5-category scoring
                                       ├─ services/roadmap.py           Skill Gap Roadmap
                                       ├─ services/llm.py               Groq suggestions
                                       └─ services/report.py            WeasyPrint PDF
                                       │
                                       └──► Supabase (Postgres + Auth)

## Scoring Categories

| Category | Weight | Checks |
|----------|--------|--------|
| Keyword Coverage | 30% | JD keywords in resume |
| Semantic Match | 25% | Sentence Transformer cosine similarity |
| Skill Validation | 20% | Required vs. present skills |
| Content Quality | 15% | Action verbs, quantified impact, length |
| ATS Compatibility | 10% | Formatting, headers, parse-ability |

## Skill Gap Roadmap

For each missing skill, the roadmap service returns:

    {
      "skill": "Kubernetes",
      "priority": "high",
      "why": "Required in 4 of 6 JD bullets",
      "steps": [
        "Core concepts: pods, services, deployments (KodeKloud free tier)",
        "Deploy a 3-tier app locally with minikube, push manifests to GitHub",
        "Add Helm chart + CI deploy to your resume project"
      ],
      "estimated_time": "2-3 weeks"
    }

## Setup

_(coming soon)_
