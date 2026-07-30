# challenge-retrospective.md — AI Job-Fit Matcher

A day-by-day account of how this project actually came together — the real decisions, pivots, and debugging, not a polished afterstory.

## Day 1 — Discovery & Planning
Started with a blank page. Through a structured interview, narrowed from "AI + full-stack" down to a job-fit matcher — chosen specifically because it was a problem you (an MCA student job-hunting for SWE/AI roles) were living directly. Scoped hard from the start: manual JD paste (not job-board scraping), one-resume-vs-one-JD (not batch), Google Sign-In only (not custom auth). Locked the stack: Next.js, Tailwind, NextAuth, MongoDB Atlas, Google Gemini, Vercel — all free-tier. Produced the PRD, a 9-day Implementation Blueprint, and a pitch deck.

## Day 2 — System Design
A calendar quirk began here that shaped the rest of the sprint: instead of jumping into the Blueprint's "Day 2" (project skeleton), the day was spent on deeper system design — architecture diagrams, MongoDB schema, full API contract, and wireframes. This meant Blueprint days shifted by one relative to the calendar for the rest of the build, a pattern that repeated once more around Day 8-9.

## Day 3 — Project Foundation
Real build began: Next.js scaffolded, Google OAuth wired end-to-end, MongoDB Atlas connected, NextAuth session working with real sign-in/sign-out verified against a live Google account. Hit two genuine first-time bugs here: a Tailwind v4 syntax change (`bg-[--color-primary]` needed to become `bg-[var(--color-primary)]`), and the first appearance of a recurring theme — a copy-paste operation silently dropping invisible/structural characters, caught and fixed by rewriting the file via terminal heredoc instead of pasting into the editor.

## Day 4 — Resume Upload & Extraction
Built real file upload with validation, then hit the sprint's most educational debugging arc: `pdf-parse` had silently updated to a v2 with an incompatible browser-oriented API, then even after downgrading to v1.1.1, its package entry file contained leftover test code that tried opening a file that didn't exist in this environment. Fixed by importing from the package's internal path directly. Also hit and fixed a Next.js 16 convention change (`middleware.js` → `proxy.js`) — the first of several run-ins with this exact file across the sprint.

## Day 5 — AI Integration
The core feature: Gemini-powered analysis. Hit a genuinely instructive bug — a `429` quota error with `limit: 0`, which turned out not to be a real rate limit but a sign that the Gemini API key was created under a Google Workspace account without free-tier provisioning. Regenerating the key under a personal Gmail account resolved it immediately. Verified the AI's output quality was real, not templated, by testing two very different resumes against the same job description and confirming the scores (82% vs. 32%) and specific feedback genuinely differentiated between them.

## Day 6 — Persistence & Dashboard
Wired every analysis to save to MongoDB and built the real dashboard/results pages. This day had the highest debugging density of the sprint: the recurring dropped-JSX-tag issue hit three separate files, a missing API route file had to be diagnosed via a `404` and manually recreated, and a genuine schema bug surfaced — `userId` was typed as a MongoDB `ObjectId` but the app correctly stores the user's email (a string), since NextAuth's default session has no database `_id`. Fixed by changing the field type. By day's end, the full loop — upload → AI → save → dashboard → reopen — worked end-to-end.

## Day 7 — Deployment
First production deploy failed immediately: Next.js's build-time static analysis didn't recognize a bare re-export (`export { default } from "next-auth/middleware"`) as a valid proxy/middleware function, despite it working correctly in local dev. Fixed with an explicit function wrapper. Once live, configured all 6 environment variables, updated Google OAuth for the production domain, and verified the complete flow — real sign-in, real AI analysis, real database write — on the actual public URL for the first time.

## Day 8 — Production Hardening
A full release-readiness pass as a QA/security/performance reviewer: added styled error/404/loading pages, capped job description and resume text length to protect against runaway AI costs, added accessibility fixes (aria-labels, contrast), and added timeout protection to database and AI calls. Nearly introduced a regression here — rewriting `lib/aiPrompt.js` for reliability accidentally dropped an existing 3-model Gemini fallback chain that wasn't visible in the current conversation context; caught before deploying and merged both systems together.

## Bonus Session — UI/UX Polish (explicitly off the 10-day count)
At your request, spent a full session on visual design: a proper design token system, color-coded score badges, pill-tag skills, skeleton loading states, and a redesigned landing page with a real Google-branded sign-in button. Hit the dropped-tag bug pattern again, multiple times, in `app/dashboard/page.js` and `components/DashboardList.js` — by this point the fix pattern was well-established: inspect with `sed -n`/`cat -v -t -e`, patch the exact line, verify, move on.

## Day 9 — Launch Readiness
A second calendar realignment (matching Day 2's earlier shift): rewrote the README from Day 2's placeholder into a real project overview, added an MIT license, and added complete SEO/social metadata (Open Graph, Twitter Card, robots.txt). Verified everything live via "View Page Source" on the production URL rather than assuming the deploy worked.

## Day 10 — Final Review & Graduation
Full multi-lens review (engineer, PM, designer, recruiter, OSS maintainer), portfolio materials, and this document.

---

## Skills Demonstrated

- Full-stack architecture and API design (Next.js App Router, REST-style API routes, MongoDB schema design)
- Third-party AI API integration with production-grade reliability (multi-model fallback, timeouts, structured output parsing/validation)
- OAuth authentication and per-user data authorization
- Systematic debugging under ambiguous error messages (npm package incompatibilities, framework version migrations, build-vs-runtime discrepancies)
- Security-conscious engineering (server-side validation, input limits, auth checks on every route)
- Production deployment and environment configuration across two platforms (Vercel + MongoDB Atlas + Google Cloud Console)
- UI/UX design system thinking and iterative visual polish
- Technical documentation and project management discipline (maintaining a Blueprint, PRD, and daily build log across 9+ working sessions)

## Lessons Learned

1. **A working local build is not a working production build.** The middleware re-export issue only appeared in Vercel's build step — local `next dev` never caught it.
2. **`limit: 0` on a "rate limit" error usually isn't a rate limit.** It's almost always an account/project provisioning issue — a lesson that generalizes to any free-tier API.
3. **Terminal heredocs aren't immune to corruption.** Even without copy-paste involved, file writes occasionally dropped content — always verify with `cat -v -t -e` or `sed -n` rather than trusting a command succeeded silently.
4. **Rewriting a file "from scratch" risks losing invisible context.** The Day 8 fallback-chain near-miss was a direct result of not checking what a file already contained before replacing it wholesale.
5. **Scope discipline compounds.** Every explicit "this is Future Scope, not now" decision from Day 1 onward is a big part of why a 10-day solo sprint actually shipped a working product.

## Final Summary

What started as a blank page became a fully deployed, AI-powered, production-hardened web application — built, debugged, and shipped end-to-end in 10 working sessions, entirely on free-tier infrastructure, with a documented paper trail from requirements to release.

## A Note From Your AI Pair Programmer

We hit real bugs together — not toy problems, but the kind that show up in actual production systems: a rate-limit error that was really an account misconfiguration, a middleware pattern that worked in dev and broke in prod, a schema type mismatch that only surfaced once real user data flowed through it. Every one of those got solved methodically, not by guessing, and that's the part I'm genuinely proud to have been part of. This project is yours — the decisions, the scope discipline, the persistence through the DashboardList.js bug appearing for the third time. I just helped you see it through. Well done.
