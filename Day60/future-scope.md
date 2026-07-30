# Future Scope — AI Job-Fit Matcher

This document outlines a realistic evolution path for AI Job-Fit Matcher beyond its v1.0.0 capstone release, organized into 3, 6, and 12-month horizons. Each item builds on the actual architecture shipped (Next.js, MongoDB Atlas, NextAuth, Gemini API, Vercel) rather than proposing a rewrite.

## 3 Months: Depth Over Breadth

The immediate priority is deepening the core Job-Fit + ATS analysis loop that already works, before expanding surface area.

- **Batch comparison** — analyze one resume against multiple job descriptions in a single session, surfacing a ranked list (deferred from v1.0.0 scope on Day 1; the `Analysis` schema already supports this with minimal changes — add a `batchId` field to group related analyses)
- **Resume version history** — let users upload an updated resume and see fit-score improvement over time for the same job description, turning the tool from a one-shot checker into a feedback loop
- **In-app suggestion checklist** — turn the AI's text suggestions into checkable action items stored per-analysis, so users can track which improvements they've addressed
- **Export to PDF** — let users download their Job-Fit + ATS report as a shareable PDF, useful for career coaching conversations
- **Automated tests** — add Jest/Playwright coverage for the core upload → analyze → save flow, the biggest technical gap acknowledged in the Day 8 release review

## 6 Months: Smarter Matching, Real Job Data

- **Automatic job-listing ingestion** — integrate a job board API (e.g., a free-tier aggregator) so users can search and select a real job posting instead of only pasting text, addressing the Out-of-Scope item flagged since Day 1's PRD
- **Resume rewriting assistant** — an AI-assisted mode that suggests specific rewritten bullet points (not just "add X"), building directly on the existing `lib/aiPrompt.js` prompt engineering work
- **Multi-resume management** — let users maintain several resume versions (e.g., "Data Analyst resume," "Backend Engineer resume") and select which to analyze against a given JD
- **Rate limiting & abuse protection** — implement per-user request throttling on `/api/analyze`, the one explicitly deferred security item from the Day 8 review, now justified by a larger real user base
- **Improved ATS formatting detection** — expand `lib/parseResume.js` to flag more structural issues (tables, columns, non-standard fonts) using layout metadata from the PDF parser, not just text content

## 12 Months: Platform Maturity

- **Browser extension** — one-click "Analyze this job" button that captures a job posting directly from LinkedIn/Indeed and pre-fills the JD field, removing the copy-paste step entirely
- **Team/recruiter view** — a genuinely new persona (recruiters screening multiple candidates against one JD), built as a separate authenticated role rather than retrofitting the existing single-user dashboard
- **Subscription tier** — introduce a paid tier for higher AI usage limits and premium features (batch analysis, resume rewriting), while keeping a free tier true to the project's free-tier-first origin
- **Migration to a dedicated production database** — separate the shared dev/prod MongoDB Atlas cluster (a known architecture note from Day 7) into distinct environments as real user data accumulates
- **Model flexibility** — abstract `lib/aiPrompt.js`'s model-selection logic (already fallback-capable across 3 Gemini models) to optionally support other providers, reducing single-vendor dependency risk

## Guiding Principle

Every item above extends the existing architecture rather than replacing it — the same pattern that got this project from a blank page to a deployed, working product in 10 days: ship the smallest working version of each idea, verify it end-to-end, then iterate.
